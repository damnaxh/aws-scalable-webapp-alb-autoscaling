# 🚀 Scalable Web Application on AWS (EC2 + ALB + Auto Scaling)

This project demonstrates how to deploy a highly available and scalable web application on AWS using EC2, Application Load Balancer (ALB), and Auto Scaling Group (ASG).

---

## 📌 Architecture Overview

- **Application Load Balancer** distributes incoming traffic.
- **Target Group** routes requests to EC2 instances.
- **Launch Template** defines configuration for EC2 provisioning.
- **Auto Scaling Group** ensures scalability and high availability.
- Health checks ensure only healthy EC2 instances receive traffic.

---

## 🏗 Technologies Used

- **Amazon EC2**
- **Application Load Balancer**
- **Auto Scaling Group**
- **Amazon VPC**
- **Security Groups**
- **Target Groups**
- **Amazon Linux 2**
- **User Data Script (Apache Web Server)**

---

## 🛠 Setup Steps

### 1. Create Security Groups
- `web-sg`: Allow HTTP(80), SSH(22)
- `alb-sg`: Allow HTTP(80)

 Create Launch Template
Includes User Data:

```bash
#!/bin/bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
echo "<h1>Hello from $(hostname)</h1>" > /var/www/html/index.html


### 4.Create Target Group
Target type: Instances

Port: 80

Health check: HTTP /

4. Create Application Load Balancer
Scheme: Internet-facing

Listener: HTTP : 80 → Forward to Target Group

5. Create Auto Scaling Group
Min: 2

Desired: 2

Max: 4

Scaling policy: CPU target tracking

✔ Testing Auto Scaling
SSH into an instance and run:

bash
Copy code
sudo yum install stress -y
stress --cpu 4 --timeout 200
Auto Scaling Group should launch new instances automatically.

📁 Project Benefits
Highly available

Fault tolerant

Automatically scalable

Flexible and cloud-ready

📷 Architecture Diagram
                 ┌────────────────────────────┐
                 │      Users / Clients       │
                 └──────────────┬─────────────┘
                                │  HTTP (80)
                                ▼
                    ┌────────────────────────┐
                    │  Application Load       │
                    │       Balancer          │
                    └─────────────┬───────────┘
                                  │
                   ┌──────────────┴──────────────┐
                   │     Target Group (web-tg)    │
                   └──────────────┬──────────────┘
                                  │
        ┌─────────────────────────┼─────────────────────────┐
        ▼                         ▼                         ▼
┌──────────────┐       ┌──────────────┐         ┌──────────────┐
│ EC2 Instance │       │ EC2 Instance │   ...   │ EC2 Instance │
│ (AutoScale)  │       │ (AutoScale)  │         │ (AutoScale)  │
└──────────────┘       └──────────────┘         └──────────────┘
        ▲                         ▲                         ▲
        └────────────── Auto Scaling Group ──────────────────┘
                          (Min=2, Max=4)
