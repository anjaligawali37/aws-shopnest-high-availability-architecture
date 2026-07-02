# AWS ShopNest High Availability Architecture - Commands Used

This document contains the Linux and SSH commands used throughout the implementation of the ShopNest High Availability AWS Infrastructure project.

---

# 1. Connect to Bastion Host (Public EC2)

```bash
ssh -i aws_login.pem ubuntu@<BASTION_PUBLIC_IP>
```

Example:

```bash
ssh -i aws_login.pem ubuntu@51.xx.xx.xx
```

---

# 2. Connect from Bastion Host to Private Web Server 1

```bash
ssh -i aws_login.pem ubuntu@10.0.11.24
```

---

# 3. Connect from Bastion Host to Private Web Server 2

```bash
ssh -i aws_login.pem ubuntu@10.0.12.82
```

---

# 4. Check Current Working Directory

```bash
pwd
```

---

# 5. List Files

```bash
ls
```

Detailed list

```bash
ls -l
```

---

# 6. Check Server Private IP

```bash
hostname -I
```

---

# 7. Check Hostname

```bash
hostname
```

---

# 8. Update Packages

```bash
sudo apt update
```

Upgrade packages

```bash
sudo apt upgrade -y
```

---

# 9. Install Python

```bash
sudo apt install python3 -y
```

---

# 10. Verify Python Version

```bash
python3 --version
```

---

# 11. Create HTML Page

```bash
nano index.html
```

Example for Web Server 1

```html
<!DOCTYPE html>
<html>
<head>
<title>ShopNest</title>
</head>

<body>

<h1>Welcome to ShopNest</h1>
<h2>Web Server 1</h2>
<h3>Private Subnet 1</h3>

</body>

</html>
```

Example for Web Server 2

```html
<!DOCTYPE html>
<html>
<head>
<title>ShopNest</title>
</head>

<body>

<h1>Welcome to ShopNest</h1>
<h2>Web Server 2</h2>
<h3>Private Subnet 2</h3>

</body>

</html>
```

Save

```
Ctrl + O
Enter
Ctrl + X
```

---

# 12. Start Python HTTP Server

```bash
sudo python3 -m http.server 80
```

---

# 13. Stop HTTP Server

```
Ctrl + C
```

---

# 14. Check HTTP Server

```bash
curl localhost
```

Check HTTP Response

```bash
curl -I localhost
```

---

# 15. Check Listening Port

```bash
sudo ss -tlnp | grep :80
```

---

# 16. Check Running HTTP Server Process

```bash
ps -ef | grep http.server
```

---

# 17. Kill Existing HTTP Server

Find PID

```bash
ps -ef | grep http.server
```

Kill Process

```bash
sudo kill -9 <PID>
```

Example

```bash
sudo kill -9 4601
```

---

# 18. Search index.html

```bash
find / -name index.html 2>/dev/null
```

---

# 19. Verify HTML Page

```bash
cat index.html
```

---

# 20. Check Network Connectivity

```bash
ping google.com
```

Ping Private Server

```bash
ping 10.0.11.24
```

```bash
ping 10.0.12.82
```

---

# 21. Test Local Web Server

```bash
curl http://localhost
```

---

# 22. Exit Private Server

```bash
exit
```

---

# 23. Exit Bastion Host

```bash
exit
```

---

# 24. Git Commands (Repository)

Clone Repository

```bash
git clone <repository-url>
```

Check Status

```bash
git status
```

Stage Files

```bash
git add .
```

Commit

```bash
git commit -m "Initial commit"
```

Push

```bash
git push origin main
```

Pull Latest Changes

```bash
git pull origin main
```

---

# AWS Console Tasks Performed

The following AWS resources were configured through the AWS Management Console:

- Created Custom Amazon VPC
- Created Public Subnet 1
- Created Public Subnet 2
- Created Private Subnet 1
- Created Private Subnet 2
- Attached Internet Gateway
- Created Public Route Table
- Created Private Route Table
- Associated Route Tables with Subnets
- Created NAT Gateway 1
- Created NAT Gateway 2
- Allocated Elastic IPs
- Configured Security Groups
- Launched Bastion Host EC2
- Launched Private Web Server 1
- Launched Private Web Server 2
- Configured Application Load Balancer (ALB)
- Created Target Group
- Registered EC2 Targets
- Configured Health Checks
- Verified Healthy Targets
- Tested High Availability using the Load Balancer DNS

---

# Project Verification

SSH Login

```bash
ssh -i aws_login.pem ubuntu@<PUBLIC_IP>
```

Private Server Access

```bash
ssh -i aws_login.pem ubuntu@10.0.11.24
```

```bash
ssh -i aws_login.pem ubuntu@10.0.12.82
```

Start Web Server

```bash
sudo python3 -m http.server 80
```

Verify

```bash
curl localhost
```

Access Application

```
http://<ALB-DNS-NAME>
```

Refresh multiple times to observe traffic being distributed between both web servers.

---

**Project Completed Successfully**
