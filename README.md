# <img width="80" height="80" alt="image" src="https://github.com/user-attachments/assets/1d67d697-03bf-466c-a71c-e118e5fd2614" /> Module 15 – Configuration Management with Ansible
This exercise is part of Module 15 from the TWN DevOps Bootcamp. In Module 15, we focus on automating server setup and application deployment using Ansible. You learn how to configure servers, deploy Node.js and Nexus, integrate with Terraform and Jenkins, manage Docker containers, and organize playbooks with roles. Each demo builds practical automation skills for real-world DevOps environments.

---
<a id="demo5"></a>
# 📦Demo 6 – Ansible & AWS EKS
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
🚀 Uses Ansible to add a new namespace. <br>
🔄 End-to-end Kubernetes automation. <br>

# Prerequisites
* AWS account with valid keys.
* Terraform demo to deploy infrastructure.
* Terraform files are available at: 🔗
* For Ansible controller node:
  * python >=3.6
  * boto3 >= 1.26.0
  * botocore >= 1.29.0 
* Python modules require to execute  the K8 module:
  * python >= 3.6
  * kubernetes >= 12.0.0
  * PyYAML >= 3.11
  * jsonpatch
    
# 🏗 Project Architecture

# ⚙️ Project Configuration
## Terraform to deploy infrastructure
1. Create the EKS cluster with Terraform using the EKS Terraform demo.
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
   
5. Check EKS cluster.
   
   <img src="" width=800/>

   
## Ansible to configure EKS
2. Ansible documentation for this module: [Ansible EKS module](https://docs.ansible.com/ansible/latest/collections/kubernetes/core/k8s_module.html#ansible-collections-kubernetes-core-k8s-module)
3. Create the kubeconfig of the EKS cluster and save it in the desired location.
   aws eks update-kubeconfig --region us-east-2 --name myapp-eks-cluster --kubeconfig ~/terraform
   ```
4. Switch to Ansible and create a new YAML file.
5. Create a new play named deploy app in a new namespace.
6. Use the kubeconfig attribute to point to the path of the kubeconfig file.
   <details><summary><strong> kubeconfig attribute </strong></summary>
     If the location of the file is not specified, then it considers the kubeconfig file default location ~/.kube/config
   </details>
   
9. Ensure the Python modules  listed above  for this module are available: PyYAML, jsonpatch, kubernetes.
   <details><summary><strong> Activate/ Deactivate Python ENV </strong></summary>
     Activate virtual ENV to install modules
     ```bash
     python3 -m venv venv
     source venv/bin/activate
     ```
     ```bash
      deactivate
     ```
   </details>
   
   ```bash
   python3 -c "import YAML"
   python3 -c "import jsonptach"
   python3 -c "import kubernetes"
   ```
11. Install requirements PyYAML, jsonpatch, and kubernetes.
   ```bash
   pip3 install pyyaml
   pip3 install jsonpatch
   pip3 install kubernetes
   ```
12. Verify the host to configuration and chck that inventory points to hosts.
13. Execute Ansible playbook.
14. Go to the terminal and set kubeconfig to point to our EKS cluster to get CLI access.
  ```bash
    export KUBECOFNIG=/users/path/to/kubeconfig_file
  ```
14. Get namespaces
    ```bash
    kubectl get namespaces
    ```
15. Create a second task to deploy the nginx app in the K8 cluster using the nginx files from previous modules.
16. Set K8S_AUTH_KUBECOFNIG env variable to load the kubeconfig without specifying the kubeconfig attribute. Therefore, Ansible knows which file to use to execute all tasks.
    ```bash
    export K8S_AUTH_KUBECOFNIG=/users/path/to/kubeconfig_file
    ```
17. Ansible playbook should be able to connect to EKS
    
 
