# Lab: Creating and Publishing an Ansible Role to Ansible Galaxy

## Objective

In this lab, you will learn how to:

* Create an Ansible role
* Understand the role directory structure
* Add tasks, variables, and handlers
* Test the role locally
* Push the role to GitHub
* Import and publish the role to Ansible Galaxy using the latest UI

---

# Prerequisites

Ensure the following are available:

* Linux machine
* Ansible installed
* Git installed
* GitHub account
* Internet connectivity

---

# Lab Architecture

```text id="6x9n4r"
Local Machine
     │
     ├── Create Ansible Role
     ├── Test Role
     ├── Push to GitHub
     └── Import to Ansible Galaxy
```

---

# Step 1: Verify Ansible Installation

Check whether Ansible is installed.

```bash id="6mrj4j"
ansible --version
```

Expected Output:

```text id="4tlx1r"
ansible [core 2.x.x]
```

---

# Step 2: Create an Ansible Role

Create a role named `nginx_role`.

```bash id="mtc7ri"
ansible-galaxy role init nginx_role
```

Expected directory structure:

```text id="wdnl74"
nginx_role/
├── defaults/
├── files/
├── handlers/
├── meta/
├── tasks/
├── templates/
├── tests/
├── vars/
└── README.md
```

---

# Step 3: Understand Role Structure

| Directory  | Purpose                        |
| ---------- | ------------------------------ |
| tasks/     | Main automation tasks          |
| handlers/  | Service restart/reload actions |
| defaults/  | Default variables              |
| vars/      | Internal variables             |
| files/     | Static files                   |
| templates/ | Jinja2 templates               |
| meta/      | Role metadata                  |
| tests/     | Test inventory and playbooks   |

---

# Step 4: Configure Tasks

Edit the tasks file.

```bash id="9ev9d2"
vim nginx_role/tasks/main.yml
```

Add the following:

```yaml id="x95plk"
---
- name: Install nginx
  apt:
    name: nginx
    state: present
    update_cache: yes

- name: Start nginx service
  service:
    name: nginx
    state: started
    enabled: yes
```

---

# Step 5: Configure Handlers

Edit handler file.

```bash id="7zhqg4"
vim nginx_role/handlers/main.yml
```

Add:

```yaml id="d7ynjq"
---
- name: restart nginx
  service:
    name: nginx
    state: restarted
```

---

# Step 6: Configure Default Variables

Edit defaults file.

```bash id="tx7jzd"
vim nginx_role/defaults/main.yml
```

Add:

```yaml id="lj4sn8"
---
package_name: nginx
```

---

# Step 7: Configure Role Metadata

Edit metadata file.

```bash id="ihmv3z"
vim nginx_role/meta/main.yml
```

Add:

```yaml id="q6dgbv"
galaxy_info:
  author: your_name
  description: Install and configure nginx
  company: your_company
  license: MIT
  min_ansible_version: 2.9

  platforms:
    - name: Ubuntu
      versions:
        - focal
        - jammy

dependencies: []
```

---

# Step 8: Create Test Inventory

Move into test directory.

```bash id="1w4t72"
cd nginx_role/tests
```

Edit inventory file.

```bash id="69tofn"
vim inventory
```

Add:

```text id="2k2m0y"
localhost ansible_connection=local
```

---

# Step 9: Create Test Playbook

Edit test playbook.

```bash id="9lpkdn"
vim test.yml
```

Add:

```yaml id="ft8i9w"
---
- hosts: all
  become: yes

  roles:
    - nginx_role
```

---

# Step 10: Test the Role

Run the playbook.

```bash id="ej0z03"
ansible-playbook -i inventory test.yml
```

Check nginx service.

```bash id="m7te61"
systemctl status nginx
```

---

# Step 11: Initialize Git Repository

Move to role directory.

```bash id="jyygm4"
cd ..
```

Initialize Git.

```bash id="2p9f7n"
git init
```

Add files.

```bash id="gnf3cn"
git add .
```

Commit files.

```bash id="4vz6oz"
git commit -m "Initial nginx role"
```

---

# Step 12: Create GitHub Repository

Open:

[GitHub](https://github.com?utm_source=chatgpt.com)

Create a new public repository.

Recommended repository name:

```text id="whg3hv"
ansible-role-nginx
```

---

# Step 13: Connect Local Repository to GitHub

Add remote repository.

```bash id="fsyclg"
git remote add origin https://github.com/USERNAME/ansible-role-nginx.git
```

Push code.

```bash id="czr8nl"
git branch -M main
git push -u origin main
```

---

# Step 14: Login to Ansible Galaxy

Open:

[Ansible Galaxy](https://galaxy.ansible.com?utm_source=chatgpt.com)

Login using your GitHub account.

---

# Step 15: Import Role Using Updated Galaxy UI

In the latest Galaxy UI:

1. Click **Roles**
2. Click **Import role**

You will see fields like:

* GitHub user
* GitHub repository
* GitHub ref

---

# Step 16: Fill Import Details

Example:

| Field             | Value              |
| ----------------- | ------------------ |
| GitHub user       | bhuvan-raj         |
| GitHub repository | ansible-role-nginx |
| GitHub ref        | Automatic          |

Important:

* Enter only repository name
* Do NOT paste full GitHub URL

Correct:

```text id="mgv7dt"
ansible-role-nginx
```

Wrong:

```text id="u0fmlt"
https://github.com/bhuvan-raj/ansible-role-nginx
```

Then click:

```text id="k98hqn"
Import
```

---

# Step 17: Verify Role Import

After import:

1. Go to **Role Imports**
2. Verify import status shows:

```text id="4h3d0m"
Completed
```

---

# Step 18: Install Published Role

Once published, users can install it.

Example:

```bash id="14u76q"
ansible-galaxy role install bhuvan_raj.nginx_role
```

---

# Step 19: Use the Role in Another Playbook

Create a playbook.

```yaml id="2jlwmj"
---
- hosts: webservers
  become: yes

  roles:
    - bhuvan_raj.nginx_role
```

Run playbook.

```bash id="w5e3sa"
ansible-playbook -i inventory site.yml
```

---

# Recommended Naming Convention

Repository name:

```text id="rme9zb"
ansible-role-<service-name>
```

Examples:

```text id="3g4mrz"
ansible-role-nginx
ansible-role-apache
ansible-role-docker
ansible-role-mysql
```

---

# Best Practices

* Keep roles modular
* Use variables instead of hardcoded values
* Add README documentation
* Use handlers for service restart
* Keep repository public
* Test roles before publishing

---

# Common Errors

| Error                | Cause                  |
| -------------------- | ---------------------- |
| Repository not found | Wrong repository name  |
| Import failed        | Missing meta/main.yml  |
| No roles detected    | Invalid role structure |
| Permission denied    | Repository is private  |

---

# Cleanup

Remove nginx if required.

```bash id="lqtm0w"
sudo apt remove nginx -y
```

---

# Conclusion

In this lab, you learned how to:

* Create an Ansible role
* Configure tasks and handlers
* Test the role locally
* Push the role to GitHub
* Import the role using the updated Ansible Galaxy UI
* Publish and reuse the role across projects
