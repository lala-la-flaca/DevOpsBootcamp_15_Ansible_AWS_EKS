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
## Create the EKS Cluster with Terraform
1. Run the EKS Terraform demo
   Use the provided Terraform files to create the EKS cluster.
   [Terraform Files]()
   
3. Initialize Terraform.
   ```bash
     terraform init
   ```
  
4. Deploy the AWS infrastructure
   
   ```bash
   terraform plan
   terraform apply --auto-approve
   ```
   
5. Verify the EKS cluster in AWS console.
   
   <img src="" width=800/>

   
## Configure EKS with Ansible
1. Review the Ansible EKS module documentation:
   [Ansible EKS module](https://docs.ansible.com/ansible/latest/collections/kubernetes/core/k8s_module.html#ansible-collections-kubernetes-core-k8s-module)
  
2. Create the kubeconfig file
   Generate the kubeconfig file for your EKS cluster and save it in your preferred location:
   aws eks update-kubeconfig --region us-east-2 --name myapp-eks-cluster --kubeconfig ~/terraform
   ```
    <img src="" width=800 />
    
3. Create a new Ansible playbook.
   Switch to Ansible and create a new YAML file.
   
   <img src="" width=800 />
  
4. Define a play named deploy app in a new namespace.
    ```bash
    
   ```
   <img src="" width=800 />
    
5. Specify the kubeconfig path:
    Set the kubeconfig attribute in your playbook to specify the path to your kubeconfig file.
   <details><summary><strong> kubeconfig attribute </strong></summary>
     If no location is specified, Ansible uses the default path: ~/.kube/config
   </details>
   
   ```bash
   ```
   
6. Verify Python dependencies.
    
   Ensure the following Python modules are installed: PyYAML, jsonpatch, and kubernetes.
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
   <img src="" width=800 />
   
7. Install Python dependencies

   ```bash
   pip3 install pyyaml
   pip3 install jsonpatch
   pip3 install kubernetes
   ```
   <img src="" width=800 />
   
8. Verify the Ansible inventory
    Confirm that the inventory file points to the correct hosts.
     <img src="" width=800 />
    
9. Run the Ansible playbook
    Execute your playbook to apply the configuration.
    ```bash
    ```
     <img src="" width=800 />
    
10. Set the kubeconfig for CLI access
    
    ```bash
    export KUBECOFNIG=/users/path/to/kubeconfig_file
    ```
     <img src="" width=800 />
     
11. List namespaces in the cluster
    
    ```bash
    kubectl get namespaces
    ```
     <img src="" width=800 />
     
12. Deploy the NGINX application.
    
    Add a second task in your playbook to deploy the NGINX app to the Kubernetes cluster using files from previous modules.
    ```bash
    ```

    <img src="" width=800 />
    
13. Set the environment variable for Ansible
    Use the environment variable K8S_AUTH_KUBECONFIG to load the kubeconfig file automatically:
    ```bash
    export K8S_AUTH_KUBECOFNIG=/users/path/to/kubeconfig_file
    ```
     <img src="" width=800 />
     
14. Verify connectivity
    Confirm that the Ansible playbook can successfully connect to the EKS cluster.
    <img src="" width=800 />
    
15. Verify nginx is running
     <img src="" width=800 />
    
    
 
