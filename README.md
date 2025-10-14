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
* Python modules require these dependencies to execute the K8 module:
  * python >= 3.6
  * kubernetes >= 12.0.0
  * PyYAML >= 3.11
  * jsonpatch
    
# 🏗 Project Architecture

# ⚙️ Project Configuration
## Create the EKS Cluster with Terraform
1. Run the EKS Terraform demo
   Use the provided Terraform files to create the EKS cluster.
   [Terraform Files](https://gitlab.com/devopsbootcamp4095512/devopsbootcamp_12_terraform_aws/-/tree/demo/ansible-terraform-3-eks?ref_type=heads)
   
3. Initialize Terraform.
   ```bash
     terraform init
   ```
  
4. Deploy the AWS infrastructure
   
   ```bash
   terraform plan
   terraform apply --auto-approve
   ```
   
5. Verify the EKS cluster in the AWS console.
   
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_15_Ansible_AWS_EKS/blob/demo/ansible-demo6-eks/Img/eks%20cluster%20runnig.PNG" width=800/>

   
## Configure EKS with Ansible
1. Review the Ansible EKS module documentation:
   [Ansible EKS module](https://docs.ansible.com/ansible/latest/collections/kubernetes/core/k8s_module.html#ansible-collections-kubernetes-core-k8s-module)
  
2. Create the kubeconfig file
   Generate the kubeconfig file for your EKS cluster and save it in your preferred location:
   
   ```bash
   aws eks update-kubeconfig --region us-east-2 --name myapp-eks-cluster --kubeconfig ~/path/to/kubeconfig/file
   ```

   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_15_Ansible_AWS_EKS/blob/demo/ansible-demo6-eks/Img/2%20creating%20aws%20eks%20kubeconfig%20file.PNG" width=800 />
    
4. Create a new Ansible playbook.
   Switch to Ansible and create a new YAML file.
   
5. Define a play named deploy app in a new namespace.
    ```bash
    ---
    - name: Deploy application in new namespace
      hosts: localhost
      tasks:
      - name: Create a k8s namespace
        kubernetes.core.k8s:
          name: my-app
          api_version: v1
          kind: Namespace
   ```
   <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_15_Ansible_AWS_EKS/blob/demo/ansible-demo6-eks/Img/play%201%20task%201.PNG" width=800 />
    
6. Specify the kubeconfig path:
    Set the kubeconfig attribute in your playbook to specify the path to your kubeconfig file.
   <details><summary><strong> kubeconfig attribute </strong></summary>
     If no location is specified, Ansible uses the default path: ~/.kube/config
   </details>
   
   ```bash
     - name: Deploy application in new namespace
      hosts: localhost
      tasks:
      - name: Create a k8s namespace
        kubernetes.core.k8s:
          name: my-app
          api_version: v1
          kind: Namespace
          kubeconfig: /home/lala/DevOpsBootCamp/terraform/Demo1/kubeconfiig_my_app-eks-cluster
   ```
   
8. Verify Python dependencies.
    
   Ensure the following Python modules are installed: PyYAML, jsonpatch, and kubernetes.<br>

   <details><summary><strong> Activate/ Deactivate Python ENV </strong></summary>
     Activate virtual ENV to install modules<br>
     ```bash
      python3 -m venv venv
      source venv/bin/activate
     ```
     <br>
    ```bash
    deactivate
    ```
     <br>
   </details>
   
     ```bash
     python3 -c "import YAML"
     python3 -c "import jsonptach"
     python3 -c "import kubernetes"
     ```
     <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_15_Ansible_AWS_EKS/blob/demo/ansible-demo6-eks/Img/5%20checking%20that%20th%20emodules%20are%20installed.PNG" width=800 />
   
10. Install Python dependencies
    ```bash
     pip3 install pyyaml
     pip3 install jsonpatch
     pip3 install kubernetes
    ```

    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_15_Ansible_AWS_EKS/blob/demo/ansible-demo6-eks/Img/6%20installing%20modules.png" width=800 />
   
12. Verify the Ansible inventory in the ansible.cfg file <br>

    Confirm that the inventory file points to the correct hosts file.<br>
    
13. Run the Ansible playbook
    Execute your playbook to apply the configuration.
    ```bash
    ansible-playbook 
    ```
     <img src="" width=800 />
    
14. Set the kubeconfig for CLI access
    
    ```bash
    export KUBECOFNIG=/users/path/to/kubeconfig_file
    ```
     <img src="" width=800 />
     
15. List namespaces in the cluster
    
    ```bash
    kubectl get ns
    ```
     <img src="" width=800 />
     
16. Deploy the NGINX application.<br>
    
    Add a second task in your playbook to deploy the NGINX app to the Kubernetes cluster using files from previous modules.<br>
    
    ```bash
    - name: Deploy nginx application
      kubernetes.core.k8s:
        src: /home/lala/DevOpsBootCamp/aws-eks/demo1/nginx-config.yaml
        state: present
        kubeconfig: /home/lala/DevOpsBootCamp/terraform/Demo1/kubeconfiig_my_app-eks-cluster
        namespace: my-app
    ```

    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_15_Ansible_AWS_EKS/blob/demo/ansible-demo6-eks/Img/play%201%20task%202.PNG" width=800 />
    
17. Set the environment variable for Ansible<br>
    Use the environment variable K8S_AUTH_KUBECONFIG to load the kubeconfig file automatically:<br>
    
    ```bash
    export K8S_AUTH_KUBECOFNIG=/users/path/to/kubeconfig_file
    ```
     <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_15_Ansible_AWS_EKS/blob/demo/ansible-demo6-eks/Img/kubeconfig%20env%20var.PNG" width=800 />
     
18. Verify connectivity <br>
    Confirm that the Ansible playbook can successfully connect to the EKS cluster.<br>
    
    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_15_Ansible_AWS_EKS/blob/demo/ansible-demo6-eks/Img/eks%20cluster%20runnig.PNG" width=800 />
    
19. Verify nginx is running

    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_15_Ansible_AWS_EKS/blob/demo/ansible-demo6-eks/Img/nginx%20pod%20running%20in%20eks.png" width=800 />
    
20. Check the Kubernetes service
    ```bash
    kubectl  get services -n my-app
    ```
    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_15_Ansible_AWS_EKS/blob/demo/ansible-demo6-eks/Img/checking%20svc.png" width=800/>
    
22. Access to Nginx

    <img src="https://github.com/lala-la-flaca/DevOpsBootcamp_15_Ansible_AWS_EKS/blob/demo/ansible-demo6-eks/Img/nginx%20up.PNG" width=800 />
 
