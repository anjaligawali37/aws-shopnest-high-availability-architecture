# AWS ShopNest High Availability Architecture

This folder contains the architecture diagram used in the **AWS ShopNest High Availability Architecture** project.

## Architecture Diagram

The diagram illustrates how AWS services work together to build a secure, scalable, and highly available infrastructure for a fictional e-commerce platform called **ShopNest**.

### Architecture Components

- Amazon VPC
- 2 Public Subnets
- 2 Private Subnets
- Internet Gateway (IGW)
- 2 NAT Gateways
- Public Route Table
- Private Route Table
- Bastion Host (Public EC2)
- Two Private Ubuntu EC2 Web Servers
- Application Load Balancer (ALB)
- Target Group
- Security Groups

---

## Traffic Flow

```
User
   │
   ▼
Application Load Balancer
   │
   ▼
Target Group
   │
   ├──────────────► Web Server 1 (Private Subnet - AZ1)
   │
   └──────────────► Web Server 2 (Private Subnet - AZ2)
```

Administrators securely access the private web servers through the Bastion Host using SSH, while private EC2 instances use NAT Gateways for outbound internet access.

---

## High Availability

The infrastructure is deployed across **two Availability Zones** to improve reliability and fault tolerance.

If one web server becomes unavailable, the Application Load Balancer automatically forwards incoming requests to the healthy server, ensuring uninterrupted application availability.

---

## Security Features

- Private EC2 instances are not directly accessible from the Internet.
- SSH access is allowed only through the Bastion Host.
- Security Groups restrict inbound and outbound traffic.
- NAT Gateways provide secure outbound internet access for private instances.
- The Application Load Balancer distributes traffic only to healthy targets.

---

## Architecture Diagram

The complete architecture diagram is available in this folder:

**📄 01. AWS Architecture Diagram.png**
