# ansible packages role

Role to install and remove packages.

## Dependencies

None.

## Supported OS families

- Ubuntu (tested)
- Arch Linux (tested)
- Redhat (untested)
- Other Linux distributions supported by 'package' module should work just fine

## Role variables

Available variables are listed below, the default values are in [defaults/main.yml](./defaults/main.yml):
```
packages_pacman_update_mirrorlist: whether to update pacman mirrorlist (requires to define packages_pacman_mirrorlist_url), default to no (bool)
packages_pacman_mirrorlst_url: link to get the mirrorlist file, default to nothing (string)
packages_update_cache: whether to update package manager cache, default to yes (bool)

## Dict of packages to install based on OS
packages_install:
  all: []
  debian: []
  archlinux: []
  redhat: []

## Dict of packages to uninstall based on OS
packages_uninstall:
  all: []
  debian: []
  archlinux: []
  redhat: []
```

## Example playbook

Here is an example playbook:
```
- hosts: all

  vars:
  packages_pacman_update_mirrorlist: yes
  packages_pacman_mirrorlist_url: https://archlinux.org/mirrorlist/?country=UA&country=GB&country=US&protocol=http&protocol=https&ip_version=4
  packages_update_cache: no
  packages_install:
    all:
    - neovim
    - zsh
    debian:
    - python3-neovim
    archlinux:
    - python-pynvim
    redhat:
    - python36-neovim
  packages_uninstall:
    all:
    - neovim
    - zsh
    debian:
    - python3-neovim
    archlinux:
    - python-pynvim
    redhat:
    - python36-neovim

  roles:
  - sudo
```

## License

MIT License
