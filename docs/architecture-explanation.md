# ShopNest High Availability Architecture - Detailed Explanation

## Overview

This project demonstrates a production-inspired AWS High Availability architecture for a fictional e-commerce platform called **ShopNest**.

The objective was to build a secure, scalable, and fault-tolerant infrastructure where web applications remain available even if one server becomes unavailable.

---

# Architecture Overview

The infrastructure consists of the following components:

- Custom Amazon VPC
- 2 Public Subnets
- 2 Private Subnets
- Internet Gateway (IGW)
- 2 NAT Gateways
- Public Route Table
- Private Route Table
- Bastion Host
- Two Ubuntu EC2 Web Servers
- Application Load Balancer (ALB)
- Target Group
- Security Groups

---

# Real-World Scenario

Imagine ShopNest is an online shopping platform.

Customers access the application through a public URL.

Instead of exposing the web servers directly to the Internet, all incoming traffic first reaches the **Application Load Balancer (ALB)**.

The ALB distributes requests across two web servers running in different Availability Zones.

If one web server becomes unhealthy or unavailable, the ALB automatically routes traffic to the healthy server, ensuring uninterrupted service.

The web servers are deployed in private subnets, making them inaccessible from the public Internet.

For administration, a Bastion Host is deployed in a public subnet. Administrators securely connect to the Bastion Host using SSH and then access the private web servers through their private IP addresses.

Private EC2 instances access the Internet through NAT Gateways for software updates while remaining protected from inbound Internet traffic.

---

# Network Flow

The request flow is as follows:

User

↓

Application Load Balancer

↓

Target Group

↓

Web Server 1 (Private Subnet - AZ1)

OR

↓

Web Server 2 (Private Subnet - AZ2)

---

# Component Explanation

## Amazon VPC

A custom Virtual Private Cloud provides an isolated network environment where all AWS resources are deployed securely.

---

## Public Subnets

The public subnets host:

- Bastion Host
- Application Load Balancer
- NAT Gateways

These resources require Internet connectivity.

---

## Private Subnets

The private subnets host:

- Web Server 1
- Web Server 2

These servers do not have public IP addresses and cannot be accessed directly from the Internet.

---

## Internet Gateway

The Internet Gateway enables communication between resources in public subnets and the Internet.

---

## NAT Gateway

The NAT Gateways allow EC2 instances in private subnets to access the Internet for software installation and updates without exposing them publicly.

---

## Bastion Host

The Bastion Host acts as a secure entry point for administrators.

SSH Flow:

Local Machine

↓

Bastion Host

↓

Private Web Server

---

## Application Load Balancer

The ALB receives incoming HTTP requests and distributes them across multiple EC2 instances.

Benefits include:

- High Availability
- Load Distribution
- Automatic Failover
- Improved Reliability

---

## Target Group

The Target Group contains the registered EC2 web servers.

The ALB forwards traffic only to healthy targets.

---

## Health Checks

The ALB continuously performs health checks on each EC2 instance.

If an instance becomes unhealthy:

- It is removed from request routing.
- Traffic is redirected to the healthy instance.
- Once healthy again, it is automatically added back.

---

## Security Groups

Security Groups act as virtual firewalls.

### Bastion Host Security Group

Allowed:

- SSH (22) from My IP

---

### Load Balancer Security Group

Allowed:

- HTTP (80) from Anywhere

---

### Web Server Security Group

Allowed:

- HTTP (80) from ALB Security Group
- SSH (22) from Bastion Host Security Group

This prevents direct Internet access to private servers.

---

# High Availability

The web servers are deployed across two different Availability Zones.

Benefits:

- Fault Tolerance
- Continuous Availability
- Improved Reliability
- Automatic Traffic Distribution

If one Availability Zone fails, the application remains accessible through the second Availability Zone.

---

# Project Validation

The following tests were successfully completed:

- SSH access to Bastion Host
- SSH access to both private web servers
- Python HTTP Server deployment
- Successful HTTP response from both web servers
- Successful ALB Health Checks
- Both targets reported Healthy
- Load Balancer successfully distributed traffic between both web servers

---

# AWS Services Used

- Amazon VPC
- Amazon EC2
- Internet Gateway
- NAT Gateway
- Route Tables
- Security Groups
- Elastic IP
- Application Load Balancer
- Target Groups
- Health Checks

---

# Learning Outcomes

Through this project, I gained practical experience with:

- Amazon VPC networking
- Public and Private subnet architecture
- Route Table configuration
- Internet Gateway configuration
- NAT Gateway implementation
- Bastion Host architecture
- Secure SSH access
- Security Group configuration
- Application Load Balancer
- Target Groups
- Health Checks
- High Availability architecture
- Linux server management
- Troubleshooting AWS networking issues

---

# Conclusion

This project demonstrates how modern cloud applications are designed for security, scalability, and high availability.

Instead of exposing backend servers directly to the Internet, the infrastructure uses private subnets, NAT Gateways, a Bastion Host, and an Application Load Balancer to create a secure and production-inspired AWS environment capable of handling failures while maintaining application availability.
