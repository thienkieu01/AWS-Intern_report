---
title : "Install Docker and Clone the Code"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.6.2 </b> "
---

Once EC2 has an Elastic IP, the next step is to connect to the instance via VS Code, install Docker, and download the application source code.

#### Step 1: Retrieve EC2's Elastic IP

1. Go to **EC2 Console** → **Elastic IPs**, select the IP address assigned to the instance.
2. Copy the **Allocated IPv4 address** value (e.g., `54.82.167.72`) — will be used to connect via SSH in a later step.

![get-elastic-ip](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/get-elastic-ip.png)

#### Step 2: Connect VS Code to EC2 via Remote-SSH

3. Open VS Code, press `Ctrl+Shift+P` (or `F1`) to open the **Command Palette**.

![open-command-palette](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/open-command-palette.png)

4. Type `Remote-SSH`, select **Remote-SSH: Connect to Host...**.

![select-remote-ssh-connect](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/select-remote-ssh-connect.png)

5. Select **+ Add New SSH Host...** (if you haven't connected to this host before).

![add-new-ssh-host](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/add-new-ssh-host.png)

6. Enter the full SSH command, including the path to the `.pem` file and the Elastic IP address: `ssh -i "C:\Users\Tran\Downloads\library-key.pem" ubuntu@54.82.167.72`

![enter-ssh-command](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/enter-ssh-command.png)

{{% notice note %}}
Replace the `.pem` path and IP address with the correct ones for your machine and your actual Elastic IP. On Windows, wrap the path in quotes if it contains spaces.
{{% /notice %}}

7. Select the SSH config file to save to (usually `C:\Users\<your-machine-name>\.ssh\config`).

![select-ssh-config-file](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/select-ssh-config-file.png)

8. Open **Remote-SSH: Connect to Host...** again — this time you'll see the saved IP address in the list — select it.

![select-saved-host](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/select-saved-host.png)

9. When asked **"Select the platform of the remote host"**, choose **Linux**.

![select-platform-linux](/images/5-Workshop/5.6-Application-deployment/5.6.2-Install-Docker-clone-code/select-platform-linux.png)

10. VS Code will open a new window and connect to EC2. When the bottom-left corner shows **"SSH: 54.82.167.72"**, the connection has succeeded.

#### Step 3: Install Docker and Docker Compose

Open a **Terminal** in VS Code (running on EC2), and run each of these in order:

1. Update the package list:

```bash
sudo apt update -y
```

2. Install Docker and Docker Compose:

```bash
sudo apt install -y docker.io docker-compose-v2
```

3. Start Docker:

```bash
sudo systemctl start docker
```

4. Enable Docker to start automatically with the system:

```bash
sudo systemctl enable docker
```

5. Add the `ubuntu` user to the `docker` group (to run docker without sudo):

```bash
sudo usermod -aG docker ubuntu
```

6. Apply the permission change immediately, without needing to log out/log back in:

```bash
newgrp docker
```

{{% notice note %}}
Since EC2 uses the **Ubuntu AMI**, the default user is `ubuntu` (not `ec2-user` like Amazon Linux), and it uses `apt` instead of `dnf`/`yum`.
{{% /notice %}}

#### Step 4: Install Git and Clone the Code

1. Install Git:

```bash
sudo apt install -y git
```

2. Clone the repository:

```bash
git clone https://github.com/BuiNgoc2005/library-management-system.git
```

3. Enter the project directory:

```bash
cd library-management-system
```

#### Step 5: Create and Configure the `.env` File

```bash
nano .env
```

Fill in the following variables:

```dotenv
# Django Settings
SECRET_KEY=very-secret-key
DEBUG=False
DJANGO_ALLOWED_HOSTS=*

# Database RDS PostgreSQL Settings
POSTGRES_DB=library_db
POSTGRES_USER=postgres
POSTGRES_PASSWORD=LibraryWorkshop2026!
POSTGRES_HOST=library-db.cep2gas62m70.us-east-1.rds.amazonaws.com
POSTGRES_PORT=5432

# AWS S3 Settings
AWS_ACCESS_KEY_ID=YOUR_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY=YOUR_SECRET_ACCESS_KEY
AWS_STORAGE_BUCKET_NAME=library-workshop-2026
AWS_S3_REGION_NAME=us-east-1
```

{{% notice warning %}}
The variable names (`DB_HOST`, `DB_NAME`...) must match exactly with the names the Django settings file (`config/settings/...`) reads via `os.environ.get(...)`. If the settings file uses different names (e.g., `POSTGRES_HOST` instead of `DB_HOST`), they must be updated to match — otherwise the application won't be able to connect to RDS even if `.env` is fully filled in.
{{% /notice %}}