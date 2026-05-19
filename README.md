## Ansible Zero-to-Hero

<img src="https://github.com/bhuvan-raj/Ansible-Zero-to-Hero/blob/main/assets/ansible.webp" alt="Banner" />

This repository is a comprehensive learning resource for students and professionals looking to master **Ansible**, the powerful, agentless IT automation engine. Start your journey from configuration management concepts to advanced playbook creation.

-----

## Repository Structure

This repository is meticulously organized into key sections, progressing from fundamental concepts to practical application and core automation logic. Each top-level folder contains its own dedicated $\text{README.md}$ file, providing in-depth explanations, examples, and usage instructions for the content within.

### 1\. Introduction to CM and Ansible

  * **Description:** A foundational guide covering **Configuration Management (CM)** principles, the need for automation, and what makes **Ansible** unique (agentless architecture, simplicity, security).
  * **Explore:** Navigate to [Introduction to CM and Ansible](./Introduction%20to%20CM%20and%20Ansible/) for detailed information.

### 2\. Managed Nodes and Inventory Management

  * **Description:** Learn how Ansible identifies and connects to the machines it manages. This section focuses on setting up your **Control Node**, configuring **SSH keys**, and mastering the **Inventory** file (static and dynamic).
  * **Explore:** Navigate to [Managed Nodes and Inventory Management](./Managed%20Nodes%20and%20Inventory%20Management/) for detailed information.

### 3\. Management of EC2 Instances

  * **Description:** Apply your inventory knowledge to a real-world cloud environment. This section details how to dynamically discover, provision, and manage **AWS EC2 instances** using Ansible's cloud-specific modules.
  * **Explore:** Navigate to [Management of EC2 Instances](./Management%20of%20EC2%20Instances/) for detailed information.

### 4\. Ansible Ad-Hoc Commands

  * **Description:** Master the art of executing quick, one-off commands across your infrastructure. This section is a hands-on guide to using various **Ansible Modules** directly from the command line for tasks like checking status or restarting services.
  * **Explore:** Navigate to [Ansible Ad-Hoc Commands](./Ansible%20Ad-Hoc%20Commands/) for detailed information.

### 5\. Introduction to Playbooks

  * **Description:** The heart of Ansible automation. This crucial section introduces the structure of **Playbooks** (written in YAML), defining **Plays** and **Tasks**, using **Handlers**, and understanding the importance of idempotency.
  * **Explore:** Navigate to [Introduction to Playbooks](./Introduction%20to%20Playbooks/) for detailed information.

### 6\. Nginx Website Hosting Lab

* **Description:** This hands-on lab demonstrates how to automate website hosting using Ansible and Nginx. You will learn how to create and execute Playbooks written in YAML, define **Plays** and **Tasks**, use **Handlers** for service management, manage file permissions, and understand the importance of **Idempotency** in automation. The lab covers installing Nginx, deploying a static website, configuring services, and verifying the deployment on a remote Linux server.
* **Explore:** Navigate to [Nginx Website Hosting Lab](./hosting-website/) for the complete step-by-step lab guide and detailed explanations.



### 7\. Ansible Roles

  * **Description:** Roles provide the essential organizational framework for large-scale Ansible projects. They enforce a standardized directory structure to group all related automation assets (tasks, handlers, files, and variables) into reusable units. Mastering roles is the key to writing modular, shareable, and maintainable automation.
  * **Explore:** Navigate to [Ansible Roles](./Ansible%20Roles/) for detailed information.
### 8\. Ansible Galaxy

  * **Description:** Ansible Galaxy is the central, public repository for the Ansible community, serving as the essential hub for discovering, sharing, and installing reusable automation content. It accelerates projects by providing pre-built components like Roles (self-contained units of configuration) and the newer, more comprehensive Collections (which bundle roles, modules, plugins, and documentation).
  * **Explore:** Navigate to [Ansible Galaxy](./Ansible%20Galaxy/) for detailed information.

### 9. Ansible Role Import Lab

* **Description:** This lab demonstrates how to create an Ansible Role, structure it properly using standard role directories, test it locally, push it to GitHub, and import it into Ansible Galaxy using the latest Galaxy UI. Students will learn how reusable automation components are shared and distributed through Ansible Galaxy for real-world infrastructure automation.
* **Explore:** Navigate to [Ansible Role Import Lab](./Ansible-Role-Import) for detailed information.


-----

