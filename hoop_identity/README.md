# Ansible Role: hoop_identity

This Ansible role automates user and group management via the Hoop Identity API.  
It creates groups and users and assigns users to specified groups using Ansible's built-in modules.

---

## 🔧 Role Variables

You can override these variables in your playbook or via command line.

| Variable            | Description                                   | Default                       |
|---------------------|-----------------------------------------------|-------------------------------|
| `hoop_api_base_url` | Base URL of the Hoop Identity API             | `https://identity.opstree.dev/api` |
| `hoop_token`        | Bearer token for authentication               | `""` *(required)* *(location: ~/.hoop/config.toml)*            |
| `hoop_group_name`   | Name of the group to be created               | `"engineering"`              |
| `hoop_user_email`   | Email address of the user                     | `"aayush.verma@opstree.com"` |
| `hoop_user_name`    | Display name of the user                      | `"ayush"`                    |
| `hoop_user_password`| Password for the user                         | `"mysecurepassword"`         |
| `hoop_user_groups`  | List of groups the user should be assigned to | `["coe-team"]`               |

---

## 📦 Example Playbook

```yaml
- name: Create user and group in Hoop Identity
  hosts: localhost
  roles:
    - hoop_identity
