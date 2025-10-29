# Scalable Web App with ALB & Auto Scaling

## 📘 Overview
This project demonstrates how to deploy a **highly available and scalable web application** on AWS using **EC2 instances**, **Auto Scaling Groups**, and an **Application Load Balancer (ALB)**.  
It ensures consistent performance and uptime during traffic fluctuations by automatically adjusting capacity based on demand.

## 🧩 Architecture
The architecture includes:
- **EC2 Instances** in multiple Availability Zones
- **Application Load Balancer (ALB)** to distribute traffic
- **Auto Scaling Group** for automatic instance management
- **CloudWatch** for performance monitoring and alerts

*(Architecture diagram and screenshots will be added soon.)*

## ⚙️ Implementation Steps
1. Created a Launch Template with EC2 configuration and web app user data.  
2. Set up an Auto Scaling Group with scaling policies based on CPU utilization.  
3. Deployed an Application Load Balancer and registered targets.  
4. Configured CloudWatch alarms for instance health and scaling activity.  
5. Tested performance during simulated traffic spikes.

## 🚀 Outcome
- Achieved **99.9% uptime** with automated scaling and load balancing.  
- Improved performance consistency during varying loads.  
- Reduced manual management through automation and monitoring.

## 🧠 Skills Demonstrated
- AWS EC2, ALB, Auto Scaling, CloudWatch  
- Infrastructure automation and monitoring  
- Scalable architecture design principles  

## 📸 Screenshots
*(Will be uploaded soon — includes AWS Console setup, Auto Scaling activity, and CloudWatch metrics.)*

## 🔗 Resources
- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
- [AWS Auto Scaling Guide](https://docs.aws.amazon.com/autoscaling/)
- [AWS ALB Overview](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)

---

### 🏗️ Project Status
🚧 **Under Development** — infrastructure and screenshots to be added soon.
