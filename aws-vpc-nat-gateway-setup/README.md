# 🌐 AWS NAT Gateway Setup

This project demonstrates how to set up a NAT Gateway on AWS to enable instances in a private subnet to securely access the internet, while restricting inbound traffic to sensitive resources such as databases.

---

## 📌 Project Objectives

- Set up a custom VPC with public and private subnets.
- Allow outbound internet access from private subnet using NAT Gateway.
- Restrict inbound access to private instances.
- Launch EC2 instances to verify connectivity.

---

## 🛠️ Tools and Services Used

- AWS Management Console  
- Amazon VPC  
- EC2 (Windows Server 2025)  
- NAT Gateway  
- Internet Gateway  
- Subnets (Public and Private)  
- Route Tables  
- Security Groups  
- Remote Desktop Protocol (RDP)

---

## 🧭 Step-by-Step Process

### 1. ✅ Region Selection
- **Region Used:** Asia Pacific (Tokyo) `ap-northeast-1`

---

### 2. 🏗️ Create a Custom VPC
- **CIDR Block:** `10.0.0.0/16`
- **Purpose:** To create an isolated virtual network environment.

---

### 3. 📦 Create Subnets
- **Public Subnet:** `10.0.0.0/24`  
- **Private Subnet:** `10.0.1.0/24`  
- **Purpose:** Public subnet allows internet access; private subnet hosts secure resources.

---

### 4. 🌐 Internet Gateway (IGW)
- Created and attached an Internet Gateway to the VPC.
- Enables internet access for instances in the public subnet.

---

### 5. 🗺️ Configure Route Tables
- **Public Route Table:**  
  - Associated with the public subnet.  
  - Route: `0.0.0.0/0 → Internet Gateway`  
- **Private Route Table:**  
  - Associated with the private subnet.  
  - Initially had no route to the internet.

---

### 6. 🚀 Launch EC2 Instances
- **Public Subnet Instance:**  
  - Windows Server 2025 AMI  
  - Auto-assign Public IP: Enabled  
  - Inbound rules: Allow HTTP, HTTPS  
- **Private Subnet Instance:**  
  - Same AMI  
  - Auto-assign Public IP: Disabled  
  - Inbound rules: Allow HTTP, HTTPS

---

### 7. 🔌 Connectivity Test (Before NAT Gateway)
- Public instance: Successfully reachable from the internet.  
- Private instance: No internet access yet (as expected).

- ### Private Instance Internet Access Without NAT Gateway
- ### *Note:* The above screenshot shows successful internet access on the **public EC2 instance**.

<img width="960" alt="10-internet" src="https://github.com/user-attachments/assets/0480091a-c320-4169-b7e9-d922188fc8a8" />

However, **instances in the private subnet cannot access the internet without a NAT Gateway configured.**  

This ensures that private instances remain secure by not exposing them directly to inbound internet traffic while still allowing outbound internet access when a NAT Gateway is set up.

---

### 8. 🚪 Create NAT Gateway
- Launched a NAT Gateway in the public subnet.
- Attached an Elastic IP to it.
- Purpose: Allow private subnet instances to reach the internet for updates.

---
### Private Instance Internet Access Without NAT Gateway

### 9. 🧭 Update Private Route Table
- Added a route:  
  `0.0.0.0/0 → NAT Gateway`
- Result: Private EC2 instance gained secure outbound internet access.

---

## ✅ Outcome

- Custom VPC and subnets created with security best practices.
- NAT Gateway enabled secure internet access for private resources.
- Verified public and private EC2 instance connectivity.
- Demonstrated secure AWS network design.

---

## 🧩 Future Enhancements

- Automate the setup using AWS CloudFormation or Terraform.
- Add Network ACLs for deeper traffic control.
- Deploy Linux instances and configure SSH.
- Set up CloudWatch for monitoring network traffic.

---

## 📘 Key Learnings

- 🧱 Understood VPC architecture and isolated networking.
- 🌐 Learned how NAT Gateway enables outbound access without inbound exposure.
- 🔐 Gained practical experience in securing cloud workloads.
- 🛠️ Practiced EC2 instance provisioning and network troubleshooting.

---

