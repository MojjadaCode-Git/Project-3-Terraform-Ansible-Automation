# Project-3-Terraform-Ansible-Automation
Terraform &amp; Ansible Automation

Provision AWS EC2 infrastructure using Terraform and automate server configuration using Ansible following Infrastructure as Code (IaC) principles.

---

## 🛠 Technologies Used

- AWS (EC2, VPC, Subnet, Security Group)
- Terraform
- Ansible
- Ubuntu WSL
- Amazon Linux 2
- Nginx

---

## 🏗 Architecture Overview

- Used custom VPC and Subnet (explicit configuration)
- Created Security Group allowing:
  - SSH (22)
  - HTTP (80)
- Provisioned EC2 instance using Terraform
- Configured SSH access using key pair
- Automated Nginx installation using Ansible
- Verified deployment via browser

---

## 📂 Terraform Configuration

- AWS Provider configuration
- Security Group resource
- EC2 resource with:
  - Subnet ID
  - VPC Security Group ID
  - Key Pair
- Output block for public IP

Run Commands:

```bash
terraform init
terraform plan
terraform apply

####################################################################

Ansible Configuration

[web]
<public-ip> ansible_user=ec2-user ansible_ssh_private_key_file=/home/username/project3-key.pem

#####################################################################

Playbook – install_nginx.yml

---
- name: Install and Start Nginx
  hosts: web
  become: yes

  tasks:
    - name: Install nginx
      yum:
        name: nginx
        state: present

    - name: Start nginx
      service:
        name: nginx
        state: started
        enabled: yes


ansible-playbook -i inventory.ini install_nginx.yml

ansible -i inventory.ini web -m ping

This is the final public ip -- http://54.174.76.45/

**Output** 

Welcome to nginx!
If you see this page, the nginx web server is successfully installed and working. Further configuration is required.

For online documentation and support please refer to nginx.org.
Commercial support is available at nginx.com.

Thank you for using nginx.





