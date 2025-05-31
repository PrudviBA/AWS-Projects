# Jenkins Deployment on EC2
## Project Overview  
This project demonstrates the deployment and configuration of Jenkins on an AWS EC2 instance running Ubuntu in the Asia Pacific (Tokyo) region. The goal is to set up a secure EC2 instance, install Java, deploy Jenkins, and ensure it’s accessible from the internet.

---

## Project Objectives  
- Launch an Ubuntu EC2 instance in the Tokyo region  
- Install Java before setting up Jenkins  
- Download and start Jenkins  
- Configure security groups to allow external access on port 8080  
- Access Jenkins via a browser using HTTP  
- Highlight important challenges faced during the setup  

---

## Tools and Services Used  
- AWS Management Console  
- AWS EC2 (Elastic Compute Cloud)  
- Ubuntu Server   
- Security Groups  
- Jenkins  
- OpenJDK Java  
- MobaXterm for SSH connection  

---

## Step-by-Step Process  

### 1️⃣ Region Selection  
Selected **Asia Pacific (Tokyo) ap-northeast-1** as the deployment region.

### 2️⃣ Launch EC2 Instance  
- Launched an **Ubuntu Server** instance.  
- Assigned a **public IP** for external access.

### 3️⃣ Connect to EC2 via SSH  
- Used **MobaXterm** to connect via SSH.  
- ⚠️ **Challenge Faced**:  
  - When connecting, ensure you use the correct username for Ubuntu which is `ubuntu`. Using the wrong username will cause login failures.

### 4️⃣ Update Packages and Install Java  
- Updated package lists and installed Java as Jenkins requires Java to run:  
```bash
  sudo apt update -y
  sudo apt install default-jdk -y
```
- Verified Java installation by checking the version:
  ```bash
  java --version

  ```
### 5️⃣ Install Jenkins
- Added the Jenkins repository and key:
- Visit the Jenkins official website to find the latest repository setup commands for Ubuntu.
  
  - Download and add the Jenkins keyring, add the repository, and update the package list:
    ```bash
    sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
    https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
    echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
    sudo apt-get update
    sudo apt-get install jenkins
    ```
 ### 6️⃣ Start Jenkins and Check Its Status
  - Start the Jenkins service:
      ```bash
      sudo systemctl start jenkins
      ```
  - Check the status to ensure it’s running:
      ```bash
     bash sudo systemctl status jenkins
      ```
  
  ### 7️⃣ Configure Security Group
  - Added an inbound rule for TCP port 8080 in the EC2 security group.

 - ⚠️ Reason:

 - Jenkins runs on port 8080 by default. Opening this port allows external access to the Jenkins web interface.

 - Opening the port to 0.0.0.0/0 for testing, but for production, restrict to trusted IPs.
  ### 8️⃣ Access Jenkins
 - Open browser and navigate to:
  ```bash
  http://<EC2_Public_IP>:8080
  ```
 -  ⚠️ Important Note:
 -  Use HTTP instead of HTTPS because Jenkins by default uses HTTP on port 8080 and does not have SSL certificates configured. Using HTTPS without certificates causes browser errors.

---

   ### Outcome
 - ✅ Successfully deployed Jenkins on Ubuntu EC2 instance.
 - ✅ Verified Jenkins dashboard access externally using HTTP.
 - ✅ Security group properly configured for secure and functional access.

---

  ### Future Enhancements
 - Set up SSL/TLS certificates to enable secure HTTPS access to Jenkins.
 - Automate deployment using Terraform or AWS CloudFormation.
 - Add NAT Gateway and private subnets for better security architecture.
 - Implement fine-grained security group rules and Jenkins user permissions.

---
   
  ### 📘 Key Learnings
 - 🔧 Jenkins Setup on Ubuntu – Learned full deployment steps.

 - ☕ Java Prerequisite – Importance of Java for Jenkins.

 - 🔓 Security Groups – How to open ports for application access.

 - 🖥️ SSH Connection – Correct OS username is crucial for connection.

 - 🌐 HTTP Access – Understanding Jenkins default uses HTTP and not HTTPS.





        
        






