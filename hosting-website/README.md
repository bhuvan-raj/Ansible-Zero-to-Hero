# Complete Lab — Host a Website Using Ansible and Nginx

This lab demonstrates how to automate website hosting using Ansible by installing and configuring Nginx on a remote Linux server.

---


# Architecture

```text id="j6f5q3"
+----------------------+
|  Ansible Control Node|
|  (Master Machine)    |
+----------+-----------+
           |
           | SSH
           |
+----------v-----------+
|   Managed Node       |
|   Ubuntu EC2 Server  |
|   Nginx Web Server   |
+----------------------+
```

---

# Prerequisites

## Infrastructure

You need:

| Component    | Requirement                       |
| ------------ | --------------------------------- |
| Control Node | Ubuntu/Linux machine with Ansible |
| Managed Node | Ubuntu EC2/Linux server           |
| SSH Access   | PEM key                           |
| Port         | 22 and 80 open                    |

---

# Lab Environment Example

| Server            | Purpose       |
| ----------------- | ------------- |
| Control Node      | Runs Ansible  |
| EC2 Ubuntu Server | Hosts website |

---

# Security Group Rules

Allow:

| Type | Port |
| ---- | ---- |
| SSH  | 22   |
| HTTP | 80   |

---

# Step 1 — Install Ansible on Control Node

## Ubuntu

```bash id="f0g6x0"
sudo apt update
sudo apt install ansible -y
```

---

# Verify Installation

```bash id="3dqdfy"
ansible --version
```

Example output:

```text id="bp1v3t"
ansible [core 2.x.x]
```

---

# Step 2 — Create Project Directory

```bash id="c4pp92"
mkdir ansible-nginx-lab
cd ansible-nginx-lab
```

---

# Step 3 — Create Inventory File

Create inventory file:

```bash id="krwj5r"
vim inventory.ini
```

Add:

## Ubuntu Server

```ini id="s6n4c9"
[web]
172.31.10.20 ansible_user=ubuntu ansible_ssh_private_key_file=~/mykey.pem
```

## Amazon Linux

```ini id="k2vrlq"
[web]
172.31.10.20 ansible_user=ec2-user ansible_ssh_private_key_file=~/mykey.pem
```

---

# Understanding Inventory

| Part                           | Meaning          |
| ------------------------------ | ---------------- |
| `[web]`                        | Group name       |
| `172.31.10.20`                 | Target server IP |
| `ansible_user`                 | SSH username     |
| `ansible_ssh_private_key_file` | PEM key path     |

---

# Step 4 — Test Connectivity

Run ping module:

```bash id="n4jyvd"
ansible web -i inventory.ini -m ping
```

Expected output:

```text id="5rz1zi"
SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

---

# Step 5 — Create Website Files

Create website directory:

```bash id="0xb7d8"
mkdir website
```

Create HTML file:

```bash id="1ah3yy"
vim website/index.html
```

Add:

```html id="yn8x3z"
<!DOCTYPE html>
<html>
<head>
    <title>Ansible Website</title>
</head>
<body>

    <h1>Website Hosted Using Ansible + Nginx</h1>

    <h2>Lab Successfully Completed</h2>

</body>
</html>
```

---

# Step 6 — Create Playbook

Create playbook:

```bash id="0rjryj"
vim playbook.yml
```

---

# Complete Playbook

```yaml id="wdsh0q"
---
- name: Host website using nginx
  hosts: web
  become: yes

  tasks:

    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install nginx
      apt:
        name: nginx
        state: present

    - name: Start and enable nginx
      service:
        name: nginx
        state: started
        enabled: yes

    - name: Remove default nginx page
      file:
        path: /var/www/html/index.html
        state: absent

    - name: Copy website files
      copy:
        src: ./website/index.html
        dest: /var/www/html/index.html
        owner: www-data
        group: www-data
        mode: '0644'
      notify: Reload nginx

  handlers:

    - name: Reload nginx
      service:
        name: nginx
        state: reloaded
```

---

# Understanding the Playbook

---

# Play Definition

```yaml id="mjlzq1"
- name: Host website using nginx
```

Defines the play name.

---

# Hosts

```yaml id="i6s3fz"
hosts: web
```

Targets servers inside `[web]` group.

---

# Become

```yaml id="0f55jz"
become: yes
```

Runs tasks with sudo privileges.

---

# Task 1 — Update Apt Cache

```yaml id="5fd8kw"
- name: Update apt cache
  apt:
    update_cache: yes
```

Updates package repository cache.

Equivalent command:

```bash id="nm3szh"
sudo apt update
```

---

# Task 2 — Install Nginx

```yaml id="wy1krj"
- name: Install nginx
  apt:
    name: nginx
    state: present
```

Equivalent command:

```bash id="dgqz6j"
sudo apt install nginx -y
```

---

# Understanding `state`

| State   | Meaning         |
| ------- | --------------- |
| present | Install package |
| absent  | Remove package  |
| latest  | Upgrade package |

---

# Task 3 — Start Service

```yaml id="3hxjlz"
- name: Start and enable nginx
  service:
    name: nginx
    state: started
    enabled: yes
```

Equivalent commands:

```bash id="54ylxv"
sudo systemctl start nginx
sudo systemctl enable nginx
```

---

# Task 4 — Remove Default Page

```yaml id="o90ozq"
- name: Remove default nginx page
  file:
    path: /var/www/html/index.html
    state: absent
```

Deletes default Nginx page.

---

# Task 5 — Copy Website File

```yaml id="i40ozt"
- name: Copy website files
  copy:
    src: ./website/index.html
    dest: /var/www/html/index.html
```

Copies local HTML file to remote server.

---

# Owner and Group

```yaml id="g24gz9"
owner: www-data
group: www-data
```

Sets proper ownership for Nginx.

---

# File Permission

```yaml id="vkq4qk"
mode: '0644'
```

Permission meaning:

| User   | Permission   |
| ------ | ------------ |
| Owner  | Read + Write |
| Group  | Read         |
| Others | Read         |

---

# Handler

```yaml id="6i9w10"
notify: Reload nginx
```

Triggers handler only when file changes.

---

# Reload Handler

```yaml id="d4vlc6"
handlers:

  - name: Reload nginx
    service:
      name: nginx
      state: reloaded
```

Reloads Nginx configuration.

---

# Step 7 — Run Playbook

```bash id="7g5eb9"
ansible-playbook -i inventory.ini playbook.yml
```

---

# Expected Output

```text id="0f34ma"
PLAY RECAP ****************************************************************

172.31.10.20 : ok=5 changed=5 unreachable=0 failed=0
```

---

# Step 8 — Verify Website

Open browser:

```text id="3jl09w"
http://<public-ip>
```

Expected:

```text id="te4w4t"
Website Hosted Using Ansible + Nginx
```

---

# Verification Commands

---

# Check Nginx Status

```bash id="xy1v1s"
sudo systemctl status nginx
```

---

# Check Port 80

```bash id="rxt4uw"
sudo ss -tulnp | grep 80
```

---

# Test Using Curl

```bash id="rslfb8"
curl http://localhost
```

---

# Step 9 — Understand Idempotency

Run the playbook again:

```bash id="r4zhtx"
ansible-playbook -i inventory.ini playbook.yml
```

Expected:

```text id="h8m5z7"
changed=0
```

This is called:

# Idempotency

Meaning:

* No duplicate changes
* Same output every time
* Infrastructure remains consistent

---

# Real-World Production Improvements

---

# 1. Use Roles

Structure:

```text id="2av8y0"
roles/
└── nginx/
    ├── tasks/
    ├── handlers/
    ├── templates/
    ├── vars/
    └── defaults/
```

---

# 2. Use Templates

Instead of static HTML:

```yaml id="q3x9dc"
template:
```

Use dynamic variables.

---

# 3. Configure Domain

Edit:

```text id="t1cw92"
/etc/nginx/sites-available/default
```

---

# 4. Enable SSL

Use:

* Certbot
* Let's Encrypt

---

# 5. Deploy Applications

You can deploy:

* React
* Angular
* Node.js
* Python Flask
* Java Spring Boot

behind Nginx reverse proxy.

---

# Common Errors

---

# Permission Denied

Cause:

```text id="l8u74n"
Wrong PEM permissions
```

Fix:

```bash id="n8h8e4"
chmod 400 mykey.pem
```

---

# SSH Failed

Check:

* Security group
* Username
* IP address
* PEM file

---

# Nginx Not Accessible

Check:

* Port 80 open
* Service running

---

# Ubuntu vs Amazon Linux Differences

| Ubuntu           | Amazon Linux    |
| ---------------- | --------------- |
| User = ubuntu    | User = ec2-user |
| Group = www-data | Group = nginx   |
| apt module       | yum module      |

---

# Amazon Linux Playbook Example

```yaml id="w6c4wa"
- name: Install nginx
  yum:
    name: nginx
    state: present
```

---

# Adhoc Commands

---

# Install Nginx

```bash id="44g3a0"
ansible web -i inventory.ini -m apt -a "name=nginx state=present" --become
```

---

# Start Service

```bash id="u0f30e"
ansible web -i inventory.ini -m service -a "name=nginx state=started enabled=yes" --become
```

---

# Copy File

```bash id="3i6j17"
ansible web -i inventory.ini -m copy -a "src=website/index.html dest=/var/www/html/index.html" --become
```

---

# Final Folder Structure

```text id="vq4k6m"
ansible-nginx-lab/
│
├── inventory.ini
├── playbook.yml
└── website/
    └── index.html
```

---

# Lab Outcome

Successfully automated:

* Nginx installation
* Service management
* Website deployment
* File permissions
* Configuration reload

using Ansible automation.
