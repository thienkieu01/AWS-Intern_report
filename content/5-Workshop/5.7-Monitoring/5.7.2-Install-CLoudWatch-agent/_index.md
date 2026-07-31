---
title : "Install CloudWatch Agent"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.7.2 </b> "
---

Once EC2 has an IAM Role with sufficient permissions (5.7.1), the next step is to install the **CloudWatch Agent** on the instance to collect Docker logs and system metrics, and send them to CloudWatch.

#### Step 1: Download and Install the CloudWatch Agent

Connect to EC2 via VS Code Remote-SSH (as done in 5.6.2), open a Terminal, and run:

1. Download the installer package:

```bash
wget https://s3.amazonaws.com/amazoncloudwatch-agent/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb
```

2. Install it:

```bash
sudo dpkg -i amazon-cloudwatch-agent.deb
```

#### Step 2: Create the Agent's Configuration File

Create a configuration file to tell the Agent to collect Docker logs and the system metrics to monitor:

```bash
sudo nano /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json
```

Paste in the following content:

```json
{
  "logs": {
    "logs_collected": {
      "files": {
        "collect_list": [
          {
            "file_path": "/var/lib/docker/containers/*/*.log",
            "log_group_name": "library-app-logs",
            "log_stream_name": "{instance_id}",
            "timestamp_format": "%Y-%m-%dT%H:%M:%S"
          }
        ]
      }
    }
  },
  "metrics": {
    "metrics_collected": {
      "mem": {
        "measurement": ["mem_used_percent"]
      },
      "disk": {
        "measurement": ["disk_used_percent"],
        "resources": ["/"]
      },
      "cpu": {
        "measurement": ["cpu_usage_active"]
      }
    }
  }
}
```

{{% notice note %}}
The `log_group_name` is `library-app-logs` — this log group will be **created automatically** in CloudWatch when the Agent sends its first log, with no need to create it manually beforehand.
{{% /notice %}}

#### Step 3: Start the Agent with the New Configuration

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl \
  -a fetch-config -m ec2 \
  -c file:/opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json -s
```

#### Step 4: Check the Agent's Status

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a status
```

If you see `"status": "running"`, the Agent is active.

![cloudwatch-agent-status](/images/5-Workshop/5.7-Monitoring/5.7.2-Install-CLoudWatch-agent/cloudwatch-agent-status.png)

#### Step 5: Verify Logs and Metrics in the CloudWatch Console

1. Go to **CloudWatch Console** → **Log groups**, find `library-app-logs` — if a new log stream appears, the Docker logs have been sent successfully.

![cloudwatch-log-group](/images/5-Workshop/5.7-Monitoring/5.7.2-Install-CLoudWatch-agent/cloudwatch-log-group.png)

2. Go to **CloudWatch Console** → **Metrics** → **All metrics**, find the `CWAgent` namespace to view the `mem_used_percent`, `disk_used_percent`, and `cpu_usage_active` metrics.

![cloudwatch-metrics](/images/5-Workshop/5.7-Monitoring/5.7.2-Install-CLoudWatch-agent/cloudwatch-metrics.png)

{{% notice warning %}}
If Docker + CloudWatch Agent + SSH are running simultaneously on a `t3.micro` (1GB RAM), the instance may run out of RAM, causing VS Code Remote-SSH to repeatedly show "Reconnecting". Consider adding a swap file or upgrading to `t3.small` if this happens.
{{% /notice %}}