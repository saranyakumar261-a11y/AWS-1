# AWS-1
Secure EC2 Web Server with IAM &amp; VPC Project for AWS Cloud Engineer portfolio
**Secure EC2 Web Server with IAM & VPC  
**

**Goal:** Launch a secure web server on EC2 inside a custom VPC using an IAM role

**Table of Contents**

- Project Overview
- Architecture Diagram
- Steps (1-7) Explanation
- Conclusion
- Infrastructure Diagram
- Workflow Diagram
- **Project Overview**

Using a **custom VPC** with a public subnet. Attaching an **IAM role** to the EC2 instance for secure AWS service access. Configuring a **security group** to allow only SSH (22) and HTTP (80) traffic. Installing and running an **Apache web server** to serve a static webpage.

**2\. Architecture Diagram**

Developer

(SSH/HTTP Access

Internet Gateway

(10.0.0.0/16)

VPC

PublicSubnet 10.0.1.0/24

EC2 Server

Web App

Amazon Linux + IAM Role

- **STEP 1: Create a VPC**

- Created a custom private network with CIDR 10.0.0.0/16.
- This ensures isolation of resources and enables subnetting.

**STEP 2: Create Public Subnet**

- Created PublicSubnet with CIDR 10.0.1.0/24.
- Public subnet allows EC2 instances to receive public IPs for internet access.

**STEP 3: Create Internet Gateway**

- Created and attached MyIGW to the VPC.
- Provides internet connectivity for EC2 instances in the public subnet.

**STEP 4: Configure Route Table**

Edited the main route table of MyVPC:

- Destination: 0.0.0.0/0
- Target: MyIGW
- Associated the route table with PublicSubnet to enable internet traffic.

**Step 5: Create IAM Role for EC2**

- Created EC2-S3-Role with AmazonS3ReadOnlyAccess policy.
- IAM role allows secure AWS API access without storing credentials on EC2.

**Step 6: Launch EC2**

- Launched a t2.micro Amazon Linux instance in PublicSubnet.
- Assigned public IP for internet access.
- Attached IAM role EC2-S3-Role.
- Configured security group to allow:
  - SSH (port 22) for administration
  - HTTP (port 80) for web traffic

**Step 7: Install Web Server**

- SSH into EC2 and installed Apache web server:

sudo yum update -y

sudo yum install httpd -y

sudo systemctl start httpd

**Created a simple webpage:**

echo "Hello from AWS EC2" | sudo tee /var/www/html/index.html

- Verified website accessible via the EC2 public IP.

**4\. Conclusion**

- Successfully deployed a secure web server on AWS EC2 inside a custom VPC.
- Used IAM role for secure service access instead of access keys.
- Demonstrated network configuration, security groups, and basic web server setup.

Project highlights key cloud skills: VPC, subnets, route tables, EC2, IAM roles, security, and web deployment.

**5\. Workflow Diagram**

Developer (SSH/HTTP)  

Public Subnet EC2  

Apache Web Server  

Web Response
