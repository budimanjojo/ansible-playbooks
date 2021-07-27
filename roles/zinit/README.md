# ansible zinit role

Role to install [zinit](https://github.com/zdharma/zinit). It's better if you already have `~/.zshrc` file before running this role.

## Dependencies

None.

## Supported OS families

- Ubuntu (tested)
- Arch Linux (tested)
- Redhat (untested)
- All the other linux distros should work just fine

## Role variables

Availables variables are listed below, the default values are in [defaults/main.yml](./defaults/main.yml):
```
## List of packages needed for zinit, ignore this if you're not sure
zinit_packages: []

zinit_become: whether to run as root or not, default is no (bool)
```

## Example playbook

Here is an example playbook:
```
- hosts: all

  roles:
  - zinit
```

## Licence

MIT License
