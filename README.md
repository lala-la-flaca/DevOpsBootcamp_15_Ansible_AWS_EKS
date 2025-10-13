# <img width="80" height="80" alt="image" src="https://github.com/user-attachments/assets/1d67d697-03bf-466c-a71c-e118e5fd2614" /> Module 15 – Configuration Management with Ansible
This exercise is part of Module 15 from the TWN DevOps Bootcamp. In Module 15, we focus on automating server setup and application deployment using Ansible. You learn how to configure servers, deploy Node.js and Nexus, integrate with Terraform and Jenkins, manage Docker containers, and organize playbooks with roles. Each demo builds practical automation skills for real-world DevOps environments.

---
<a id="demo5"></a>
# 📦Demo 6 – Ansible and EKS
# 📌 Objective
  Automate the deployment of a Kubernetes application using Ansible and Terraform on AWS EKS.

# 🚀 Technologies Used
* Ansible: Configuration management tool for automation.
* Terraform: Provisions AWS infrastructure.
* AWS: Cloud provider.
* Linux: OS.
* AWS EKS: Managed Kubernetes service.

# 🎯 Features
✅ Provisions EKS with Terraform. <br>
🚀 Uses Ansible to deploy app in new namespace. <br>
🔄 End-to-end Kubernetes automation. <br>

# Prerequisites
* AWS account with valid keys.
* Terraform demo to deploy infrastructure.
* Terraform files are available at: 🔗
* For Ansible controller node:
  * python >=3.6
  * boto3 >= 1.26.0
  * botocore >= 1.29.0 
  
# 🏗 Project Architecture

# ⚙️ Project Configuration
## Terraform to deploy infrastructure
1. Create EC2 instances using Terraform files from the Terraform Demo
   [Terraform Files]()
   
3. Initialize Terraform  
   ```bash
     terraform init
   ```
  
4. Deploy AWS infrastructure using Terraform
   
   ```bash
   terraform plan
   terraform apply --auto-approve
   ```
   
5. Check the Amazon console and verify that EC2s are running.
   
   <img src="" width=800/>

   
## Ansible to configure EC2



 
