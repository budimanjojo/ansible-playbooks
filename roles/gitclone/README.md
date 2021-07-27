# ansible gitclone role

Role to clone github repositories to machine.

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
gitclone_git_package_name: name of git package name, default to 'git' (string)
gitclone_become: whether to become root or not, default to no (bool)

## List of repositories to add
gitclone_repo_add:
- repo_url: repository url link, default to nothing (string)
  repo_local_path: path where the repository will be clone to, default to nothing (string)
  repo_version: branch, tag, version of the repository to be cloned to, default to 'HEAD' (string)
  repo_accept_hostkey: whether to accept the first time prompt to accept repository hostkey, default to yes (bool)
  repo_recursive: whether to also clone the submodules, default to yes (bool)
  track_submodules: whether to track latest commit of submodules, default to no (bool)
  dir_mode: directory permission, default to OS default (string)
  dir_owner: owner of the directory, default to OS default (string)
  dir_group: group of the directory, default to OS default (string)
  dir_recursive: whether to recursively set the mode, owner, group of directory, default to yes (bool)
```

## Example playbook

Here is an example playbook:
```
- hosts: all

  vars:
    gitclone_become: yes
    gitclone_repo_add:
    - repo_url: https://github.com/username/repo.git
      local_path: /root/somewhere/repo
    - repo_url: https://gitlab.com/username/repo.git
      local_path: /etc/gitrepo/repo
      repo_recursive: no
      dir_owner: root
      dir_group: sudo

  roles:
  - gitclone
```

## Licence

MIT License
