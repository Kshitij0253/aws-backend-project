# aws-backend-project
AWS VPC Project with Auto Scaling, Load Balancer, and Bastion Host. Set up a scalable and secure AWS backend infrastructure that hosts a webpage using EC2 instances, Auto Scaling, and Load Balancing.
# AWS Backend Project (Manual Setup via AWS Console)

## 🎯 Project Objective
Create a custom VPC with subnets.
Implement Auto Scaling for EC2 instances.
Set up a Bastion host for secure access.
Configure a Load Balancer to distribute traffic
— **all configured manually using the AWS Console**.

---

## 🧱 Architecture Overview

- Custom VPC (`aws_backend_vpc`)
- 2 AZs: each with 1 public and 1 private subnet
- Bastion host in public subnet for SSH access to private EC2
- Auto Scaling Group (ASG) in private subnets
- Application Load Balancer (ALB) in public subnet
- Web Page hosted on one private instance to See Load Balancing (index.html)

---

## 🔧 Step-by-Step Setup (via AWS Console)

### ✅ Step 1: Create VPC and Subnets

1. Go to **VPC > Your VPCs > Create VPC**
   - Name: `aws_backend_vpc`
   - CIDR: `10.0.0.0/16`

2. **Create 4 subnets**:
   - AZ1:
     - Public Subnet A (e.g., `10.0.1.0/24`)
     - Private Subnet A (`10.0.2.0/24`)
   - AZ2:
     - Public Subnet B (`10.0.3.0/24`)
     - Private Subnet B (`10.0.4.0/24`)

3. Create an **Internet Gateway** and attach it to the VPC.

4. Configure **Route Tables**:
   - Public route → IGW
   - Private route → NAT Gateway 

📸 _Screenshot: `images/vpc-subnet.png`_

---

### ✅ Step 2: Create Auto Scaling Group

1. Create a **Launch Template**:
   - AMI: Amazon Linux / Ubuntu
   - Instance type: t2.micro or t3.micro

📸 _Screenshot: `images/Launch_template.png`_

2. Go to **EC2 > Auto Scaling Groups > Create**
   - Select your launch template
   - Choose both private subnets
   - Desired: 2 | Min: 1 | Max: 3

📸 _Screenshot: `images/auto-scaling.png`_

---

### ✅ Step 3: Create Bastion Host

1. Launch EC2 instance in Public Subnet A
   - Allow SSH access (from your IP)
   - Assign an Elastic IP
   - Save key pair (.pem)

📸 _Screenshot: `images/bostion-host.png`_

2. Connect via:
   ```bash
   ssh -i mykey.pem ubuntu@<EIP>
   
📸 _Screenshot: `images/connect.png`_


### ✅ Step 4: Create LoadBalancer
2. Go to **EC2 > Load Balancer > Create**
   - Create a Load-Balancer
   - Create a Target group inside that 
   

📸 _Screenshot: `images/load-balancer.png`_


### ✅ Step 5: Test
 Test the Application to access from broswer 

 📸 _Screenshot: `images/test.png`_

 📸 _Screenshot: `images/test1.png`_

 In second image you see that i am unable to see my web page because i only code in one instance and here load balancer dived the request accordingly 