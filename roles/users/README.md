# ansible users role

Role to manage users and groups in Linux.

## Dependencies

None.

## How to generate password

To generate hashed password, run this command:
```
ansible all -i localhost, -m debug -a "msg={{ 'yourpassword' | password_hash('sha512', 'secretsalt') }}"
```

## Supported OS families

- Ubuntu (tested)
- Arch Linux (tested)
- Redhat (untested)
- All the other linux distros should work just fine

## Role variables

Availables variables are listed below, the default values are in [defaults/main.yml](./defaults/main.yml):
```
## List of users to add
users_add:
- username: username you want to add (string)
  password: sha512 hashed password, to generate it see above (string)
  create_home: whether to create home directory, default is yes (bool)
  generate_ssh_key: whether to generate ssh key, default is no (bool)
  append: whether to append user to existing groups or remove other groups, default is no (bool)
  groups: list of groups the user will be added to, default is nothing (list)
  update_password: 'always' or 'on_create', whether to update password only for new user or always, default is always (string)
  shell: the user's shell, default is follow OS (string)
  authorized_keys: list of public key strings you want to add to user, default is nothing (list)
  authorized_keys_exclusive: whether to remove other non-specified keys, default is no (bool)

## List of users to remove
users_remove:
- username: username you want to remove (string)
  remove_dir: whether to also remove the directories associated, default is no (bool)

## List of groups to remove
groups_remove: []
```

## Example playbook

Here is an example playbook:
```
- hosts: all

  vars:
    users_add:
    - username: admin
      password: $6$secretsalt$rhg1DOUiEqjMGlpDXDdS8wXQfgM2WXxnbvNFNCdSp4wjwGOGpOC5lkuHPDHe7NraAc9oLq5yFqz0tbgfUbSy/0
      groups:
      - group1
      - group2
    - username: admin2
      password: $6$secretsalt$rhg1DOUiEqjMGlpDXDdS8wXQfgM2WXxnbvNFNCdSp4wjwGOGpOC5lkuHPDHe7NraAc9oLq5yFqz0tbgfUbSy/0
      generate_ssh_key: true
      shell: /bin/zsh
      authorized_keys:
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDIgzLDHHRtLD9DLfNTX8Te9zBcDmEF33UPJ5HngP6aJAhdQln7ebSOzQoehxN0th644G9csnujxjNAStIEUjzeXO1NQQfEYGqDVxDL0jE4hXr1WVg+6GxQnV1nWP5Sd2i24+ElygCdw3KuteeNlfGZ7BKs91zySb03DICXPNcgXj6ZR9INalabFhbjeVG5MRH38KRR9cxZKbgW+eQZZwVtDRPzL7rAfaeeJPg7ZQ3Iu0SC3q5SskGQD5XfqCwPDx9n0GWva36jwNneifv5WFDh0U+xKaoVT4HJTWyV/vf3+fTji1yEsGMBbPexuD5aHvmun9SdgIlGw65GJB7Ibz47Bq/jVfnTV6o5BVDhEfwayHZgahODl5Uyc3VqkKoJh9IWivoBr/bLHXepiJGUReEw61nBc3JL9QC4J5ngterLXP/iapl185+JSvUzDjbtFDHLiXCqa8X17Cm9LSIKik/W7gM2tU63QcQd/p8H55he/Kgm94vWJlq98rjLCtBYTNQDSNAU6AFQqk2c3x23L09wSRIQJ1aUEq6aPx3yfbiRHyTslTyP4tg0I1U1o+jjh9tZV/+JpRcwg9xi9YLoGMAv9aUVGHodjehZw1wHnuql3ALiy/Nnm2LANDh4vhJ2fKsrBqhk8dyDdqFHFsLyTSXUAE4NKGG1AUV3fgMjvRRZZQ==
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDJVJ+gHYFCoyd1WG8uJ2d0ErwmyASjhqv8ZXblNBHMjTSNXtqxTZ/MIIAPkxi3XSSFIcAGO7nr5myKyQVfiFlPAQMDR64iTfL6N/peMi25xE5+MhQKTIcJBSlRYx3RjJmx9JwmDuT8aXlPqL16QWk8WVe5XErNAXrsj+PrTISlS9O8wbqKExcC2jTzieg4L3II4cBv+M7QySt8ApzLJ5geYniO4mc5Jqor1hBZakQDw8vJdohOgnjVK+MIvVFm97iVmhNXUCgqFn3EGXVGLAB8J8h2aix8WvkP85WmvJ4nZ9k22QvijBr3WHQdwU/VoZ7xWpXVcGsXwnlD9tpGUotx
ssh-rsa
    users_remove:
    - username: trash
      remove_dir: true
    groups_remove:
    - disk
    - adm

  roles:
  - users
```

## Licence

MIT License
