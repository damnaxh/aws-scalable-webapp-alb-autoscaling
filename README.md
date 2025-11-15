# 🚀 Scalable Web Application on AWS (EC2 + ALB + Auto Scaling)

This project demonstrates how to deploy a highly available and scalable web application on AWS using EC2, Application Load Balancer (ALB), and Auto Scaling Group (ASG).

---

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
- <img width="1360" height="594" alt="image" src="https://github.com/user-attachments/assets/7caf5956-6d4b-4fd0-8333-d3bbf0af5964" />


### 2. Create Launch Template
Includes User Data:

bash
```#!/bin/bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
echo "<h1>Hello from $(hostname)</h1>" > /var/www/html/index.html
```
<img width="1358" height="634" alt="image" src="https://github.com/user-attachments/assets/ae513d79-15af-4df0-ac36-50c06b586c67" />

### 3. Create Target Group
   
- Target type: Instances
- Port: 80
- Health check: HTTP /
- <img width="1357" height="597" alt="image" src="https://github.com/user-attachments/assets/0ccb1522-ad18-4420-aff7-cccddb7fa69d" />


### 4. Create Application Load Balancer
   
- Scheme: Internet-facing
- Listener: HTTP : 80 → Forward to Target Group
-<img width="1361" height="601" alt="image" src="https://github.com/user-attachments/assets/afbfc0d1-5eeb-4f9f-817f-50989eec0772" />



### 5. Create Auto Scaling Group
- Min: 2
- Desired: 2
- Max: 4
- Scaling policy: CPU target tracking
- <img width="1364" height="594" alt="image" src="https://github.com/user-attachments/assets/87fc5171-3b70-474e-8245-0c5a58591075" />



```
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
```

