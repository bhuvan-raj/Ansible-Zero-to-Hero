# Ansible Zero-to-Hero

<img src="https://github.com/bhuvan-raj/Ansible-Zero-to-Hero/blob/main/assets/ansible.webp" alt="Ansible Banner" />

[![Ansible][badge-ansible]][ansible-site]
[![Modules][badge-modules]](#modules)
[![License: MIT][badge-license]][license]
[![PRs Welcome][badge-prs]][contributing]

A hands-on learning resource for mastering **Ansible**, the agentless IT automation engine. It takes you from Configuration Management fundamentals to roles, collections, secrets management, and real-world automation.

---

## Quick Start

```bash
git clone https://github.com/bhuvan-raj/Ansible-Zero-to-Hero.git
cd Ansible-Zero-to-Hero
```

Pick a module below and follow its `README.md`. New here? Read [Prerequisites][prereqs] and the [Learning Path][path] first.

---

## Modules

| #  | Module | What you'll learn |
|----|--------|-------------------|
| 01 | [Introduction to CM and Ansible][m01] | CM fundamentals, agentless architecture, SSH, YAML |
| 02 | [Managed Nodes and Inventory][m02] | Control/managed nodes, static & dynamic inventory, groups |
| 03 | [Management of EC2 Instances][m03] | AWS auth, dynamic inventory, cloud modules |
| 04 | [Ad-Hoc Commands][m04] | One-off operations: packages, services, files |
| 05 | [Introduction to Playbooks][m05] | Plays, tasks, handlers, privilege escalation, idempotency |
| 06 | [Variables, Facts and Conditions][m06] | Variables, registered vars, facts, conditionals |
| 07 | [Nginx Website Hosting Lab][m07] | Hands-on: install Nginx, deploy a site, use handlers |
| 08 | [Ansible Roles][m08] | Role structure: tasks, handlers, templates, defaults |
| 09 | [Ansible Galaxy][m09] | Discover, install, and use community roles/collections |
| 10 | [Role Import Lab][m10] | Build, test, publish, and import a role into Galaxy |
| 11 | [Ansible Collections][m11] | Collection structure, namespaces, plugins |
| 12 | [Collections Lab][m12] | Build and publish a collection to Galaxy |
| 13 | [Vault and Secret Management][m13] | Encrypt files and variables, manage Vault passwords |

> Full progression, dependencies between modules, and lab markers: [Learning Path][path].

---

## More Docs

| Doc | Purpose |
|-----|---------|
| [Prerequisites][prereqs] | Skills and tools to have before starting |
| [Getting Started][start] | Clone, set up, and work through a module |
| [Learning Path][path] | Recommended order and what each stage unlocks |
| [Contributing][contributing] | How to report issues and submit PRs |

---

## License

Released under the [MIT License][license].

**Happy Learning! Automate Everything with Ansible.** 🚀

<!-- Badges -->
[badge-ansible]: https://img.shields.io/badge/Ansible-Automation-EE0000?logo=ansible&logoColor=white
[badge-modules]: https://img.shields.io/badge/Modules-13-blue
[badge-license]: https://img.shields.io/badge/License-MIT-green.svg
[badge-prs]: https://img.shields.io/badge/PRs-welcome-brightgreen.svg

<!-- Links -->
[ansible-site]: https://www.ansible.com/
[license]: ./LICENSE
[prereqs]: ./docs/prerequisites.md
[start]: ./docs/getting-started.md
[path]: ./docs/learning-path.md
[contributing]: ./docs/contributing.md

<!-- Modules -->
[m01]: ./Introduction%20to%20CM%20and%20Ansible/
[m02]: ./Managed%20Nodes%20and%20Inventory%20Management/
[m03]: ./Management%20of%20EC2%20Instances/
[m04]: ./Ansible%20Ad-Hoc%20Commands/
[m05]: ./Introduction%20to%20Playbooks/
[m06]: ./Variables,%20Facts%20and%20Conditions/
[m07]: ./hosting-website/
[m08]: ./Ansible%20Roles/
[m09]: ./Ansible%20Galaxy/
[m10]: ./Ansible-Role-Import/
[m11]: ./Ansible%20Collections/
[m12]: ./Ansible-Collections/
[m13]: ./Ansible%20Vault%20and%20SecretManagement/
