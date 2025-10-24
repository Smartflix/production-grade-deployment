#  Production-Grade Automated Deployment Script

This repository contains a fully automated **Bash deployment script (`deploy.sh`)** designed to streamline end-to-end application deployment to a remote EC2 instance.  
It handles cloning the repository, setting up the server environment, building and deploying Dockerized applications, and configuring Nginx as a reverse proxy — **all in one go**.

---

## 🧩 Features

- ✅ Interactive user input (Git repo, branch, SSH details, etc.)
- ✅ Automated Git authentication using a Personal Access Token (PAT)
- ✅ Remote server preparation (Docker, Docker Compose, Nginx installation)
- ✅ Secure SSH connectivity checks
- ✅ Automatic Docker image build and container deployment
- ✅ Nginx reverse proxy setup (HTTP → app port)
- ✅ Health checks and validation after deployment
- ✅ Error handling and logging to timestamped files
- ✅ Idempotent (can re-run without breaking existing setup)
- ✅ Optional cleanup mode (`--cleanup` flag)

---

## ⚙️ Prerequisites

Before running the script, ensure you have:

1. **Git** installed on your local machine or EC2 instance:
   ```bash
   sudo apt update && sudo apt install -y git

2. A valid Personal Access Token (PAT) from GitHub with repo access permissions.

Generate it at: https://github.com/settings/tokens

Example format: ghp_xxxxxxxxxxxxxxxxxxxxxx

3. An EC2 server (Ubuntu or Amazon Linux recommended) with:

SSH access enabled

4. Docker and Nginx installed, or let the script install them automatically

  Your private key (.pem) file accessible to the system running the script.
🚀 How to Run
1️⃣ Make the script executable
chmod +x deploy.sh

2️⃣ Run the script
./deploy.sh

3️⃣ Follow the interactive prompts

The script will ask for:

GitHub repository URL

Personal Access Token (PAT)

Branch name (default: main)

SSH username (e.g., ec2-user for Amazon Linux or ubuntu for Ubuntu)

Server IP address

Path to SSH key file (e.g., /home/ubuntu/my-key.pem)

Application port (e.g., 3000 or 8080)

  Production Deployment Automation Script
  Version: 1.0.0

[INFO] Starting deployment process...
[INFO] Log file: deploy_20251023_053126.log

  STEP 1: Collecting Deployment Parameters
  
Enter Git Repository URL: https://github.com/Smartflix/production-grade-deployment.git
Enter Personal Access Token (PAT):
Enter branch name (default: main): main
Enter SSH username: 
Enter server IP address: 
Enter SSH key path: /home/ec2-user/keypair.pem
Enter application port (1-65535): 8080


  STEP 2: Cloning/Updating Repository
  
[SUCCESS] Repository updated successfully
...
[SUCCESS] Application deployed and accessible on port 8080

🧱 What the Script Does Internally
Step	Description
1️⃣	Collects parameters and validates input
2️⃣	Authenticates and clones Git repository using PAT
3️⃣	Validates Dockerfile or docker-compose.yml presence
4️⃣	Connects to the remote server via SSH
5️⃣	Installs Docker, Compose, and Nginx if missing
6️⃣	Transfers project files, builds image, and runs containers
7️⃣	Configures Nginx as a reverse proxy
8️⃣	Verifies app and container health
9️⃣	Logs actions with timestamps for debugging
🔟	Supports idempotent re-runs and cleanup mode

