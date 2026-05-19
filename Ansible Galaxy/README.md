# Ansible Galaxy
<img src="https://github.com/bhuvan-raj/Ansible-Zero-to-Hero/blob/main/assets/galaxy.png" alt="Banner" width=800 height= 400 />

---

## 🌍 **1. What is Ansible Galaxy?**

**Ansible Galaxy** is the **official hub for sharing and discovering Ansible content** — primarily **roles** and **collections**.

Think of it like:

> **“GitHub for Ansible automation content.”**

It allows DevOps engineers to:

* Find **pre-built roles** (e.g., install Nginx, configure Docker, manage AWS, etc.)
* **Reuse** community-developed automation
* **Publish** their own roles or collections for others

🔗 Website: [https://galaxy.ansible.com](https://galaxy.ansible.com)

---

## ⚙️ **2. Why Use Ansible Galaxy?**

| Feature                | Description                                                     |
| ---------------------- | --------------------------------------------------------------- |
| 🔁 Reusability         | Download ready-made roles instead of writing from scratch       |
| 🌐 Collaboration       | Share your automation publicly or within a team                 |
| 🧱 Structure           | Provides standardized role templates                            |
| 🛠️ CLI Integration    | Comes with the `ansible-galaxy` command-line tool               |
| 🧩 Collections Support | Supports both **roles** and **collections** for larger projects |

---

## 🧰 **3. Ansible Galaxy CLI Overview**

Ansible provides the **`ansible-galaxy`** command to interact with Galaxy.

You can use it to:

* Create roles
* Download roles
* Remove roles
* List installed roles
* Manage collections

### 🔹 Common Syntax:

```bash
ansible-galaxy [subcommand] [options]
```

---

## 🧭 **4. Important Ansible Galaxy Commands**

| Command                                          | Description                                     | Example                                        |
| ------------------------------------------------ | ----------------------------------------------- | ---------------------------------------------- |
| `ansible-galaxy init <role_name>`                | Create a new role structure                     | `ansible-galaxy init nginx_setup`              |
| `ansible-galaxy install <role_name>`             | Install a role from Galaxy                      | `ansible-galaxy install geerlingguy.nginx`     |
| `ansible-galaxy install -r requirements.yml`     | Install multiple roles from a requirements file | `ansible-galaxy install -r requirements.yml`   |
| `ansible-galaxy list`                            | List installed roles                            | `ansible-galaxy list`                          |
| `ansible-galaxy remove <role_name>`              | Remove an installed role                        | `ansible-galaxy remove geerlingguy.nginx`      |
| `ansible-galaxy search <keyword>`                | Search roles on Galaxy                          | `ansible-galaxy search nginx`                  |
| `ansible-galaxy collection install <collection>` | Install a collection                            | `ansible-galaxy collection install amazon.aws` |
| `ansible-galaxy collection list`                 | List installed collections                      | `ansible-galaxy collection list`               |

---

## 🧱 **5. Structure of an Ansible Role**

When you create a role using `ansible-galaxy init`, it generates a standard directory layout:

```
my_role/
├── defaults/
│   └── main.yml
├── files/
├── handlers/
│   └── main.yml
├── meta/
│   └── main.yml
├── tasks/
│   └── main.yml
├── templates/
├── tests/
├── vars/
│   └── main.yml
└── README.md
```

### 🔹 Important File: `meta/main.yml`

Contains role metadata required for publishing:

```yaml
galaxy_info:
  author: bubu
  description: Install and configure Nginx
  company: ""
  license: MIT
  min_ansible_version: 2.9
  platforms:
    - name: Ubuntu
      versions:
        - focal
        - jammy
  galaxy_tags:
    - nginx
    - web
dependencies: []
```

---

## 📦 **6. How to Download (Install) a Role from Ansible Galaxy**

### ✅ **Step-by-Step**

1. **Search for a role:**

   ```bash
   ansible-galaxy search nginx
   ```

2. **Choose a role** (example: `geerlingguy.nginx`)

3. **Install the role:**

   ```bash
   ansible-galaxy install geerlingguy.nginx
   ```

4. **Verify installation:**

   ```bash
   ansible-galaxy list
   ```

   Output example:

   ```
   - geerlingguy.nginx, 3.2.0 (installed in /home/user/.ansible/roles)
   ```

5. **Use in a playbook:**

   ```yaml
   - hosts: webservers
     roles:
       - geerlingguy.nginx
   ```

---

