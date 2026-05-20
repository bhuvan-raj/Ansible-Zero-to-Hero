# Ansible Collections

## What is an Ansible Collection?

An **Ansible Collection** is a structured package used to distribute and organize Ansible content.

A collection can contain:

* Roles
* Modules
* Plugins
* Playbooks
* Documentation
* Inventories
* Custom scripts

Collections help organize automation content in a standardized format and make sharing easier through platforms like Ansible Galaxy.

---

# Why Collections are Important

Before collections, everything was mainly distributed using roles.

As Ansible grew, managing:

* custom modules,
* plugins,
* roles,
* and reusable automation

became difficult.

Collections solve this by grouping everything into a single package.

---

# Benefits of Collections

## 1. Better Organization

All automation components stay inside one structured directory.

Example:

```text
Collection
 ├── Roles
 ├── Modules
 ├── Plugins
 ├── Playbooks
 └── Docs
```

---

## 2. Easy Sharing

Collections can be uploaded to:

* [Ansible Galaxy](https://galaxy.ansible.com?utm_source=chatgpt.com)
* Private Automation Hub

Other users can install them easily.

---

## 3. Reusability

A single collection can be reused across:

* multiple projects
* multiple teams
* different environments

---

## 4. Namespace Support

Collections use:

```text
namespace.collection_name
```

Example:

```yaml
community.mysql.mysql_db
```

This avoids naming conflicts.

---

# Collection Structure

Example structure:

```text
my_namespace/
└── my_collection/
    ├── docs/
    ├── galaxy.yml
    ├── meta/
    ├── plugins/
    │   └── modules/
    ├── roles/
    ├── playbooks/
    ├── README.md
    └── tests/
```

---

# Important Files

## 1. galaxy.yml

This is the metadata file of the collection.

Contains:

* author
* version
* namespace
* dependencies
* description

Example:

```yaml
namespace: devops
name: webserver
version: 1.0.0
readme: README.md
authors:
  - Bubu
description: Apache and Nginx automation collection
license:
  - MIT
```

---

## 2. plugins/

Contains:

* modules
* filter plugins
* lookup plugins
* callback plugins

Example:

```text
plugins/modules/
```

---

## 3. roles/

Stores reusable roles.

Example:

```text
roles/nginx/
roles/mysql/
```

---

# Installing Collections

## Install from Ansible Galaxy

```bash
ansible-galaxy collection install community.general
```

---

## Install Specific Version

```bash
ansible-galaxy collection install community.general:5.8.0
```

---

# Listing Installed Collections

```bash
ansible-galaxy collection list
```

---

# Using a Collection in Playbook

Example:

```yaml
---
- hosts: all
  collections:
    - community.general

  tasks:
    - name: Create a file
      file:
        path: /tmp/demo.txt
        state: touch
```

---

# Difference Between Roles and Collections

| Roles                      | Collections                               |
| -------------------------- | ----------------------------------------- |
| Contains only role content | Can contain roles, modules, plugins, docs |
| Smaller reusable unit      | Larger distributable package              |
| No namespace support       | Uses namespaces                           |
| Limited structure          | Standardized structure                    |

---

# LAB — Create and Push an Ansible Collection

---

# Lab Objective

In this lab you will:

1. Create a custom collection
2. Add a role inside it
3. Build the collection
4. Publish it to [Ansible Galaxy](https://galaxy.ansible.com?utm_source=chatgpt.com)

---

# Prerequisites

Install:

* Ansible
* Python
* Git

Check version:

```bash
ansible --version
```

---

# Step 1 — Create Collection Structure

Run:

```bash
ansible-galaxy collection init devops.webserver
```

Output:

```text
- Collection devops.webserver was created successfully
```

---

# Step 2 — Enter Collection Directory

```bash
cd devops/webserver
```

---

# Step 3 — View Structure

```bash
tree
```

Example:

```text
.
├── docs
├── galaxy.yml
├── meta
├── plugins
├── README.md
└── roles
```

---

# Step 4 — Create a Role Inside Collection

```bash
ansible-galaxy role init roles/nginx
```

This creates:

```text
roles/nginx/
```

---

# Step 5 — Create Role Task

Edit:

```bash
vim roles/nginx/tasks/main.yml
```

Add:

```yaml
---
- name: Install nginx
  package:
    name: nginx
    state: present

- name: Start nginx
  service:
    name: nginx
    state: started
    enabled: yes
```

---

# Step 6 — Create a Playbook

Create:

```bash
vim playbooks/install_nginx.yml
```

Add:

```yaml
---
- hosts: all
  become: yes

  roles:
    - nginx
```

---

# Step 7 — Update galaxy.yml

Edit:

```bash
vim galaxy.yml
```

Example:

```yaml
namespace: devops
name: webserver
version: 1.0.0

authors:
  - Bubu

description: Nginx automation collection

license:
  - MIT

readme: README.md

dependencies: {}
```

---

# Step 8 — Build the Collection

Run:

```bash
ansible-galaxy collection build
```

Output:

```text
devops-webserver-1.0.0.tar.gz
```

---

# Step 9 — Create Ansible Galaxy Account

Open:

[Ansible Galaxy Website](https://galaxy.ansible.com?utm_source=chatgpt.com)

Login using:

* GitHub account

---

# Step 10 — Generate Galaxy API Token

Open:

[Galaxy API Preferences](https://galaxy.ansible.com/me/preferences?utm_source=chatgpt.com)

Generate a token.

---

# Step 11 — Export Token

```bash
export ANSIBLE_GALAXY_TOKEN='your_token'
```

---

# Step 12 — Publish Collection

Run:

```bash
ansible-galaxy collection publish devops-webserver-1.0.0.tar.gz --token $ANSIBLE_GALAXY_TOKEN
```

Successful output:

```text
Collection has been successfully published
```

---

# Step 13 — Verify Collection

Search your collection on:

[Ansible Galaxy Explore Page](https://galaxy.ansible.com/ui/standalone/collections/?utm_source=chatgpt.com)

---

# Installing Your Published Collection

Other users can install it using:

```bash
ansible-galaxy collection install devops.webserver
```

---

# Real-World Use Cases

Collections are commonly used for:

* Kubernetes automation
* AWS automation
* Database management
* Network automation
* Internal enterprise automation

Popular examples:

* `amazon.aws`
* `community.docker`
* `kubernetes.core`

---

# Best Practices

* Use meaningful namespaces
* Follow semantic versioning
* Write proper documentation
* Keep roles modular
* Test collections before publishing
* Store collections in Git repositories

---

# Summary

Ansible Collections are the modern packaging standard in Ansible.

They help:

* organize automation content,
* distribute reusable code,
* simplify dependency management,
* and standardize automation projects.

Collections are widely used in enterprise DevOps environments and are the recommended way to distribute Ansible automation content.
