# AWS NAT Gateway Setup 

This project demonstrates how to set up a NAT Gateway on AWS to enable instances in a private subnet to access the internet securely, while controlling inbound access to sensitive resources like database servers.

---

## Project Overview

The goal is to create a secure network architecture using AWS Virtual Private Cloud (VPC) with both public and private subnets. A NAT Gateway is used to allow instances in the private subnet to access the internet for updates or patches without exposing them to direct inbound internet traffic.

---

## Step-by-Step Setup

### 1. Create a Custom VPC
- **Why?**  
  A VPC (Virtual Private Cloud) provides an isolated virtual network environment in AWS where you can launch resources with customized IP addressing and network configurations.
- **What was done?**  
  Created a new VPC to isolate our infrastructure and control network settings.

---

### 2. Create Two Subnets: Public and Private
- **Public Subnet:** CIDR block `10.0.0.0/24`  
- **Private Subnet:** CIDR block `10.0.1.0/24`
- **Why?**  
  Subnets divide the VPC into smaller network segments. The public subnet allows resources with direct internet access, while the private subnet hosts resources that must remain isolated from direct internet access for security reasons.

---

### 3. Create and Attach an Internet Gateway (IGW)
- **Why?**  
  An Internet Gateway enables communication between the VPC and the internet. It allows instances in the public subnet to send and receive traffic from the internet.
- **What was done?**  
  Created an IGW and attached it to the custom VPC.

---

### 4. Create Two Route Tables: Public and Private
- **Public Route Table:**  
  - Associated with the public subnet  
  - Contains a route `0.0.0.0/0` pointing to the Internet Gateway  
- **Private Route Table:**  
  - Associated with the private subnet  
  - Initially, no route to the internet
- **Why?**  
  Route tables control traffic routing in the VPC. The public route table directs internet traffic to the IGW, while the private route table restricts direct internet access.

---

### 5. Launch EC2 Instances in Each Subnet
- **Public Subnet:**  
  - EC2 instance with Auto-assign Public IP enabled  
  - Microsoft Windows Server 2025 AMI used  
- **Private Subnet:**  
  - EC2 instance with Auto-assign Public IP disabled (no direct internet access)  
  - Same AMI as above  
- **Security Groups:**  
  - Allowed inbound HTTP and HTTPS traffic for both instances  
- **Why?**  
  Public instance acts as a web server accessible from the internet, while the private instance (e.g., database server) is isolated to enhance security.

---

### 6. Test Connectivity
- **Result:**  
  - Successfully pinged the public EC2 instance from the internet  
  - Private EC2 instance cannot access the internet yet
- **Why?**  
  Without a NAT Gateway, instances in the private subnet have no route to the internet.

---

### 7. Setup NAT Gateway in Public Subnet
- **Why?**  
  NAT Gateway allows instances in the private subnet to initiate outbound connections to the internet (e.g., for software updates), but blocks inbound internet traffic, protecting private resources.
- **What was done?**  
  Created a NAT Gateway in the public subnet.

---

### 8. Update Private Route Table to Use NAT Gateway
- Added a route `0.0.0.0/0` pointing to the NAT Gateway in the private route table.
- **Effect:**  
  Private subnet instances can now access the internet securely through the NAT Gateway.
  
---

## Why This Architecture?

- **Public Subnet:**  
  Hosts resources (like web servers) that need to be publicly accessible.
- **Private Subnet:**  
  Hosts sensitive resources (like databases) that must be isolated from inbound internet traffic.
- **NAT Gateway:**  
  Provides controlled outbound internet access to private subnet resources without exposing them directly.
- **Security:**  
  This design ensures sensitive data is protected while maintaining necessary connectivity for updates and patches.

---





