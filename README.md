# 🚀 AWS ShopNest High Availability Architecture

A production-inspired AWS networking project that demonstrates how to build a **secure**, **highly available**, and **fault-tolerant** infrastructure for a fictional e-commerce platform called **ShopNest**.

This project was built to gain hands-on experience with Amazon VPC, networking, load balancing, secure access using a Bastion Host, and highly available application deployment across multiple Availability Zones.

---

# 📖 Project Scenario

Imagine ShopNest is an e-commerce company expecting thousands of users every day.

The infrastructure requirements are:

- Users should access the application through a single endpoint.
- Backend web servers must not be directly accessible from the Internet.
- Administrators should securely access private servers using SSH.
- Private instances should access the Internet only for updates.
- The application should continue working even if one web server fails.

To achieve this, I designed a highly available AWS infrastructure using multiple AWS networking services.

---

# 🏗️ Architecture

The architecture consists of:

- Amazon VPC
- 2 Public Subnets
- 2 Private Subnets
- Internet Gateway
- 2 NAT Gateways
- Public Route Table
- Private Route Table
- Bastion Host
- Application Load Balancer
- Target Group
- Two Ubuntu EC2 Web Servers
- Security Groups

Architecture diagram:

📂 **architecture/01. AWS Architecture Diagram.png**

---

# ☁️ AWS Services Used

- Amazon VPC
- Amazon EC2
- Application Load Balancer (ALB)
- Target Groups
- Internet Gateway
- NAT Gateway
- Route Tables
- Security Groups
- Elastic IP
- SSH
- Ubuntu Linux

---

# 🔄 Traffic Flow

```
User
   │
   ▼
Application Load Balancer
   │
   ▼
Target Group
   │
 ┌───────────────┐
 ▼               ▼
Web Server 1   Web Server 2
(Private AZ1)  (Private AZ2)

        ▲
        │
 Bastion Host (SSH)
        │
 Administrator
```

---

# 📂 Repository Structure

```
aws-shopnest-high-availability-architecture/
│
├── architecture/
│   ├── 01. AWS Architecture Diagram.png
│   └── README.md
│
├── commands/
│   └── aws-linux-commands.md
│
├── docs/
│   └── architecture-explanation.md
│
├── screenshots/
│   ├── VPC Dashboard
│   ├── Subnets
│   ├── Route Tables
│   ├── Internet Gateway
│   ├── NAT Gateway
│   ├── Security Groups
│   ├── Bastion Host
│   ├── Load Balancer
│   ├── Target Group
│   ├── SSH Connections
│   └── Browser Output
│
└── README.md
```

---

# 🛠️ Project Implementation

### Step 1
Created a custom Amazon VPC.

### Step 2
Created:

- 2 Public Subnets
- 2 Private Subnets

across two Availability Zones.

### Step 3
Configured:

- Internet Gateway
- Route Tables

for public connectivity.

### Step 4
Created two NAT Gateways for secure outbound internet access from private instances.

### Step 5
Launched:

- Bastion Host
- Web Server 1
- Web Server 2

### Step 6
Configured Security Groups for controlled network access.

### Step 7
Connected to private instances using SSH through the Bastion Host.

### Step 8
Hosted Python HTTP servers on both private EC2 instances.

### Step 9
Created:

- Application Load Balancer
- Target Group

and registered both web servers.

### Step 10
Verified health checks and tested load balancing by refreshing the ALB DNS repeatedly.

---

# 🖼️ Project Screenshots

Complete implementation screenshots are available inside the **screenshots/** folder.

---

# 🧪 Validation Performed

✔ SSH into Bastion Host

✔ SSH into Private Web Server 1

✔ SSH into Private Web Server 2

✔ Verified Target Group Health Checks

✔ Verified Load Balancer Routing

✔ Confirmed both servers receive traffic

✔ Verified High Availability

---

# 📚 Key Learnings

- Amazon VPC Networking
- Public & Private Subnets
- Route Tables
- Internet Gateway
- NAT Gateway
- Security Groups
- Bastion Host
- SSH
- Application Load Balancer
- Target Groups
- Health Checks
- High Availability
- Linux Networking
- AWS Troubleshooting

---

# 🚀 Future Improvements

- AWS CloudFormation
- AWS CLI Automation
- Amazon S3
- IAM Best Practices
- Auto Scaling Group
- CloudWatch Monitoring
- CI/CD Pipeline using GitHub Actions
- Terraform

---

# 👩‍💻 Author

**Anjali Gawali**

Engineering Student | AWS Cloud Enthusiast | Learning DevOps & Cloud Computing

GitHub:
https://github.com/anjaligawali37

LinkedIn:
https://www.linkedin.com/in/anjali-gawali-248b2a399/

---

⭐ If you found this project useful, feel free to star the repository.
