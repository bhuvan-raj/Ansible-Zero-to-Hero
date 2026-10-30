# Learning Path

[← Back to README](../README.md)

```
 FOUNDATIONS            AUTOMATION CORE             REUSABILITY              SECURITY
+-------------+       +------------------+       +------------------+     +-------------+
| 01 CM Intro |       | 04 Ad-Hoc        |       | 08 Roles         |     | 13 Vault    |
| 02 Inventory| ----> | 05 Playbooks     | ----> | 09 Galaxy        | --> |  & Secrets  |
| 03 EC2      |       | 06 Vars & Facts  |       | 10 Role Import * |     +-------------+
+-------------+       | 07 Nginx Lab *   |       | 11 Collections   |
                      +------------------+       | 12 Collections * |
                                                 +------------------+
                                                       * = hands-on lab
```

| Stage | Modules | Outcome |
|-------|---------|---------|
| Foundations | 01 to 03 | Understand CM, connect to nodes, manage cloud inventory |
| Automation Core | 04 to 07 | Write playbooks that are dynamic, idempotent, and real-world ready |
| Reusability | 08 to 12 | Package, share, and publish roles and collections |
| Security | 13 | Protect secrets with Ansible Vault |

## What You'll Be Able to Do

- Explain Configuration Management and Ansible's agentless architecture
- Manage nodes, inventories, and SSH authentication
- Automate AWS EC2 with dynamic inventory
- Use ad-hoc commands and modules
- Write YAML playbooks with handlers, variables, facts, and conditions
- Automate Nginx website hosting
- Build, publish, and import roles and collections via Galaxy
- Manage secrets with Ansible Vault
