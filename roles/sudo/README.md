# ansible sudo role

Role to manage sudoers file.

## Dependencies

None.

## Supported OS families

- Ubuntu (tested)
- Arch Linux (tested)
- Redhat (untested)

## Role variables

Available variables are listed below, the default values are in [defaults/main.yml](./defaults/main.yml):
```
sudo_admin_group_name: group name which can run sudo command, default to OS default (string)
sudo_admin_group_nopasswd: whether users in admin group can run sudo commands without password, default to false (bool)
sudo_sudoers_d: sudoers directory to be included, default to OS default (string)

## List of admin group hostnames
sudo_admin_group_hosts: []

## List of admin group runas rusers
sudo_admin_group_runas_users: []

## List of admin group runas groups
sudo_admin_group_runas_groups: []

## List of admin group permitted commands
sudo_admin_group_commands: []

## List of users that can run sudo
sudo users:
- username: username to add to sudoers (string)
  nopasswd: whether user can run sudo commands without password, default to false (bool)
  is_admin_group: whether user is in admin group, default to false (bool)
  ## List of users's runas hostnames
  hosts: []
  ## List of user's runas users
  runas_users: []
  ## List of user's runas groups
  runas_groups: []
  ## List of user's permitted commands
  commands: []

## List of sudo defaults configurations
sudo_defaults:
- defaults: defaults config (string)
```

## Example playbook

Here is an example playbook:
```
- hosts: all

  vars:
    sudo_admin_group_nopasswd: true
    sudo_users:
    - username: somebody
      nopasswd: true
      is_admin_group: true
    - username: somebody2
      hosts:
      - localhost
      - production
      runas_users:
      - somebody3
      - somebody4
      runas_groups:
      - production
      commands:
      - /usr/bin/passwd
      - /usr/bin/cp

  roles:
  - sudo
```

## License

MIT License
