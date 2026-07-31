---
title : "Cài đặt CloudWatch Agent"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.7.2 </b> "
---

Sau khi EC2 đã có IAM Role đủ quyền (5.7.1), bước tiếp theo là cài **CloudWatch Agent** trên instance để thu thập log Docker và metrics hệ thống, gửi lên CloudWatch.

#### Bước 1: Tải và cài đặt CloudWatch Agent

Kết nối vào EC2 qua VS Code Remote-SSH (như đã làm ở 5.6.2), mở Terminal, chạy:

1. Tải gói cài đặt:

```bash
wget https://s3.amazonaws.com/amazoncloudwatch-agent/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb
```

2. Cài đặt:

```bash
sudo dpkg -i amazon-cloudwatch-agent.deb
```

#### Bước 2: Tạo file cấu hình cho Agent

Tạo file cấu hình để chỉ định Agent thu thập log Docker và các metrics hệ thống cần theo dõi:

```bash
sudo nano /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json
```

Dán nội dung sau:

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
`log_group_name` là `library-app-logs` — nhóm log này sẽ được **tự động tạo** trên CloudWatch khi Agent gửi log đầu tiên lên, không cần tạo trước thủ công.
{{% /notice %}}

#### Bước 3: Khởi động Agent với cấu hình vừa tạo

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl \
  -a fetch-config -m ec2 \
  -c file:/opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json -s
```

#### Bước 4: Kiểm tra trạng thái Agent

```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a status
```

Nếu thấy `"status": "running"` là Agent đã hoạt động.

![cloudwatch-agent-status](/images/5-Workshop/5.7-Monitoring/5.7.2-Install-CloudWatch-Agent/cloudwatch-agent-status.png)

#### Bước 5: Kiểm tra log và metrics trên CloudWatch Console

1. Vào **CloudWatch Console** → **Log groups**, tìm `library-app-logs` — nếu thấy log stream mới xuất hiện là log Docker đã được gửi lên thành công.

![cloudwatch-log-group](/images/5-Workshop/5.7-Monitoring/5.7.2-Install-CloudWatch-Agent/cloudwatch-log-group.png)

2. Vào **CloudWatch Console** → **Metrics** → **All metrics**, tìm namespace `CWAgent` để xem các chỉ số `mem_used_percent`, `disk_used_percent`, `cpu_usage_active`.

![cloudwatch-metrics](/images/5-Workshop/5.7-Monitoring/5.7.2-Install-CloudWatch-Agent/cloudwatch-metrics.png)

{{% notice warning %}}
Nếu chạy đồng thời Docker + CloudWatch Agent + SSH trên `t3.micro` (1GB RAM), instance có thể bị hết RAM dẫn tới VS Code Remote-SSH báo "Reconnecting" liên tục. Cân nhắc thêm swap file hoặc nâng cấp lên `t3.small` nếu gặp tình trạng này.
{{% /notice %}}