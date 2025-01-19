#  Automated Deployment with Ansible

This project automates the deployment of a multi-service infrastructure using **Ansible**, **Docker**, and **Docker Compose**. It includes:

- Disabling IPv6
- Installing Docker and Docker Compose
- Deploying a Drupal stack with HAProxy, Nginx, Apache, PHP, and MariaDB
- Deploying Gitea and Woodpecker CI
- Setting up hourly backups
- Deploying a FastAPI development environment with Redis

## 📂 Folder Structure

![image](https://github.com/user-attachments/assets/f9edeeba-62e2-4c32-b3e5-57a2042e9431)



## 🛠️ Prerequisites

Before running the playbooks, ensure the following:

-  **Ansible Installed**:
```bash
   sudo apt update
   sudo apt install ansible
```

- SSH Access: Ensure you have SSH access to the target server(s) with a user that has sudo privileges.

- Inventory File: Create an Ansible inventory file (e.g., hosts) to define the target servers:

```bash
[webservers]
your-server-ip ansible_user=your-ssh-user
```
**🚀 Installation and Deployment Steps**

- Clone the Repository
	Clone the repository containing the Ansible playbooks and templates:

```bash
git clone hhttps://github.com/OsamaOracle/Ansible-playbook-Linux.git
cd Anisble-playbook-Linux
```
- **Disable IPv6**
Run the playbook to disable IPv6 on the target server(s):

```bash
ansible-playbook -i hosts playbooks/disable_ipv6.yml
```
-  Install Docker and Docker Compose
Run the playbook to install Docker and Docker Compose:

```bash
ansible-playbook -i hosts playbooks/install_docker.yml
```

- **Deploy the Drupal Stack**
Run the playbook to deploy the Drupal stack:

```bash
ansible-playbook -i hosts playbooks/deploy_drupal_stack.yml
```

**This will**

- Deploy HAProxy for routing
- Deploy Nginx for domain1.com
- Deploy Apache for domain2.com
- Set up PHP 7.4 and PHP 8.2
- Deploy MariaDB as the shared database


Deploy Gitea and Woodpecker CI
Run the playbook to deploy Gitea and Woodpecker CI:

```bash
ansible-playbook -i hosts playbooks/deploy_gitea_woodpecker.yml
```


This will:
- Deploy Gitea for Git repository hosting
- Deploy Woodpecker CI for continuous integration

- **Set Up Hourly Backups**
Run the playbook to set up hourly backups:

```bash
ansible-playbook -i hosts playbooks/setup_backups.yml
```

This will:

- Create a backup script
- Schedule hourly backups using cron

- **Deploy the FastAPI Development Environment**
Run the playbook to deploy the FastAPI development environment:

```bash
ansible-playbook -i hosts playbooks/setup_fastapi.yml
```

This will:

- Deploy FastAPI with Redis
- Expose FastAPI on port 8001

**✅ Verification**

**Verify Drupal Stack**
- Access http://<your-server-ip> to see the HAProxy routing in action.
- Access http://domain1.com for the Nginx site.
- Access http://domain2.com for the Apache site.

**Verify Gitea and Woodpecker CI**
- Access Gitea at http://<your-server-ip>:3000.
- Access Woodpecker CI at http://<your-server-ip>:8000.

**Verify FastAPI**
- Access the FastAPI endpoint at http://<your-server-ip>:8001/increment.

**➕ Adding More Websites**
To add more websites to the Drupal stack:

- Update the docker-compose-drupal.yml file with additional services.
- Update the haproxy.cfg file to route traffic to the new services.

Re-run the deploy_drupal_stack.yml playbook:

```bash
ansible-playbook -i hosts playbooks/deploy_drupal_stack.yml
```
**💾 Backups**

Backups are stored in /backups/ on the server. You can restore them by extracting the .tar.gz files.
