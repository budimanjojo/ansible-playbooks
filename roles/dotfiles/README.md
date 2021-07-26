# ansible dotfiles role

Role to link dotfiles from repository to machine. You will need a repository containing dotfiles.

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
dotfiles_git_package_name: name of git package name, default to 'git' (string)
dotfiles_repo_url: repository url link, default to 'https://github.com/budimanjojo/dotfiles.git' (string)
dotfiles_repo_local_path: path where the repository will be clone to, default to '~/github/dotfiles' (string)
dotfiles_repo_version: branch, tag, version of the repository to be cloned to, default to 'HEAD' (string)
dotfiles_repo_accept_hostkey: whether to accept the first time prompt to accept repository hostkey, default to yes (bool)
dotfiles_home: home directory path of the machine, default to '~' (string)
dotfiles_become: whether to become root or not, default to no (bool)

## List of files in the repository to be linked to home directory
dotfiles_files: []

## List of directories to be created before making symlink
dotfiles_create_dir: []
```

## Example playbook

Here is an example playbook:
```
- hosts: all

  vars:
    dotfiles_repo_url: https://github.com/username/repo.git
    dotfiles_local_path: ~/repo
    dotfiles_files:
    - .zshrc
    - .vimrc
    - .config/nvim
    dotfiles_create_dir:
    - .config/nvim
```

## Licence

MIT License
