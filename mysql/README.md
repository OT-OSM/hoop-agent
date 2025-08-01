# 🎯 Ansible Role: Hoop Connection Setup for mysql

This Ansible role automates the installation and configuration of the [Hoop CLI](https://hoop.dev) and registers a database connection securely. It ensures secure management of database credentials using `ansible-vault`.
---

## ⚙️ Default Variables (`defaults/main.yml`)

These variables can be overridden in your playbook or inventory.

| Variable              | Description                                           | Default Value                                                      |
|-----------------------|-------------------------------------------------------|--------------------------------------------------------------------|
| `hoop_agent_name`     | Name of the Hoop agent                                | `{{ ansible_hostname }}-dummy-agent`                              |
| `hoop_command`        | Command the Hoop agent will execute                   | `bash`                                                             |
| `hoop_key`            | gRPC key to communicate with the identity server      | `grpc://_default:xagt-REPLACE_ME@identity.opstree.dev:8010`      |
| `hoop_user`           | Linux user to run the agent as                        | `root`                                                             |
| `hoop_service_name`   | Name of the systemd service created                   | `hoop-agent`                                                       |
| `db_host`             | Database host IP or DNS                              | `127.0.0.1`                                                        |
| `db_port`             | Database port                                         | `3306`                                                             |
| `db_user`             | Database username                                     | `root`                                                             |
| `db_name`             | Name of the database to connect to                    | `mydb`                                                             |
| `db_pass`             | **Sensitive** — stored via `ansible-vault` only       | Not defined in defaults (see below)                               |

> ⚠️ **`db_pass`** must be stored securely in `vault.yml` (encrypted).

---

## 🔐 Secure Secrets with Ansible Vault

**Never store passwords in plaintext.**

### 1. Create the vault file:

```bash
ansible-vault create vault.yml
db_pass: "MySecurePassword123"
```
### Example Playbook

```
- name: Setup Hoop Agent and DB Connection
  hosts: all
  become: true

  vars_files:
    - vault.yml

  roles:
    - hoop_setup
```


