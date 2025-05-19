# # AWS Custom VPC Setup

## Project Overview
This project demonstrates the creation and configuration of a Virtual Private Cloud (VPC) in AWS using the Tokyo (Asia Pacific) region. The goal is to set up a custom VPC environment with subnets, internet gateway, route tables, and launch a Windows EC2 instance inside the VPC. Finally, I verified internet connectivity on the instance via RDP.

---

## Project Objectives
- Create a VPC with a custom CIDR block.
- Create public subnets within the VPC.
- Attach and configure an Internet Gateway to enable internet access.
- Set up route tables to route outbound traffic through the Internet Gateway.
- Launch a Windows EC2 instance inside the subnet.
- Verify the instance's internet connectivity through pinging external IP (8.8.8.8) via RDP.

---

## Tools and Services Used
- AWS Management Console
- AWS EC2 (Elastic Compute Cloud)
- VPC (Virtual Private Cloud)
- Internet Gateway
- Route Tables
- Subnets
- Windows Server Instance
- Remote Desktop Protocol (RDP)

---

## Step-by-Step Process

### 1. Region Selection
Selected **Asia Pacific (Tokyo) ap-northeast-1** as the deployment region to demonstrate multi-region capability.

### 2. Create a VPC
- Navigated to the VPC Dashboard.
- Created a new VPC with a CIDR block `10.0.0.0/16`.

### 3. Create Subnet
- Created a public subnet inside the VPC with CIDR block `10.0.0.0/24`.
- Assigned the subnet to the VPC.

### 4. Create and Attach Internet Gateway (IGW)
- Created an Internet Gateway.
- Attached the IGW to the VPC to allow internet connectivity.

### 5. Configure Route Table
- Created a new route table associated with the VPC.
- Added a route with destination `0.0.0.0/0` pointing to the Internet Gateway.
- Associated the public subnet with this route table.

### 6. Launch Windows EC2 Instance
- Launched a Windows Server EC2 instance inside the public subnet.
- Assigned a public IP address to the instance to enable external access.

### 7. Connect and Verify
- Used Remote Desktop Protocol (RDP) to connect to the Windows instance.
- Opened Command Prompt and ran `ping 8.8.8.8` to verify internet connectivity.
- Successful ping replies confirmed proper internet access.


## Outcome
- Successfully created a custom VPC with public subnet and internet gateway.
- Proper route tables were configured allowing internet access for the Windows instance.
- Verified that the Windows EC2 instance can access the internet, fulfilling the project objective.

## Future Enhancements
- Add private subnets and configure NAT Gateway for outbound internet access.
- Automate VPC and instance setup using AWS CloudFormation or Terraform.
- Set up security groups and Network ACLs for better traffic control.
- Explore launching Linux instances and connecting via SSH.

## 📘 Key Learnings
This setup helped me develop a strong understanding of AWS VPC architecture and cloud networking fundamentals:
- 🔧 **Custom VPC Setup** – Gained understanding of why and how to create a custom VPC instead of using the default one.
- 🌐 **Internet Gateway & Public Subnets** – Learned how to enable internet access by attaching an Internet Gateway and configuring public subnets.
- 🧭 **Routing Concepts** – Understood how route tables work and how to set up routes to direct outbound traffic.
- 💻 **Launching EC2 Instances** – Practiced launching Windows EC2 instances and assigning public IPs for remote access.
- 🔒 **Security Awareness** – Became more familiar with AWS access methods like RDP and basic security configurations.
- 📡 **Connectivity Testing** – Used the `ping` command to verify internet connectivity from inside the instance.
- 🌍 **Region Awareness** – Understood the importance of selecting the appropriate AWS region for deployment.
- 🧱 **Component Relationships** – Learned how different VPC components (VPC, subnets, route tables, IGWs) work together to form a secure, functional network.


