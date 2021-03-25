# Network Credentials

Used to configure local credentials. The option to purge all accounts that are not the specified user is configured. See the Role Variables section for the variable details.

## Role Variables

- **purge_users**: (yes/no) Whether to purge all local users that are not what is declared in primary_user. Defaults to No if nothing specified.
- **primary_user**: The name of the user to modify/keep. Default value is "admin"
- **local_pass**: The local password to configure for the primary user. Recommended to set this as a vaulted password or in Tower use a Custom Credential Type to encrypt this password.

See [Ansible Tower Custom Credential Types](https://docs.ansible.com/ansible-tower/latest/html/userguide/credential_types.html) for configuring the password as an encrypted variable.

## Example Playbook

#### Purge all users except "admin"

```yaml
- name: Configure Local Device Credentials
  hosts: all
  gather_facts: no

  vars:
    purge_users: yes
    primary_user: "admin"
    local_pass: "password123"

  roles:
    - network_credentials
```

#### Change only the "net_admin" user, don't purge other users.

```yaml
- name: Configure Local Device Credentials
  hosts: all
  gather_facts: no

  vars:
    purge_users: no
    primary_user: "net_admin"
    local_pass: "password123"

  roles:
    - network_credentials
```
