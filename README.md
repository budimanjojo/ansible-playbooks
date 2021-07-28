# ansible-playbooks

This repository contains my ansible roles. The goal of me making these roles instead of using the available roles in the Galaxy is to simplify everything and use the best practices of current Ansible version.
Most of these roles are not really features heavy, but fit my needs as a regular user perfectly.

## Available roles

Here are the list of currently available roles. Each role has its own README file explaining how to use it:
- [users](./roles/users/): This role lets you create and remove users and groups
- [sudo](https://galaxy.ansible.com/budimanjojo/sudo): This role lets you configure sudoers file
- [ssh](./roles/ssh/): This role lets you configure ssh
- [packages](https://galaxy.ansible.com/budimanjojo/packages): This role lets you install and uninstall packages
- [dotfiles](https://galaxy.ansible.com/budimanjojo/packages): This role lets you clone and link your dotfiles from remote repository
- [gitclone](./roles/gitclone/): This role lets you clone repositories to your machine
- [download](./roles/download/): This role lets you download files or archive files to your machine
- [zinit](./roles/zinit/): This role lets you install [zinit](https://github.com/zdharma/zinit)
- [vimplug](https://galaxy.ansible.com/budimanjojo/vimplug): This role lets you install [vim-plug](https://github.com/junegunn/vim-plug) and configure vim plugins

## Secret variables management

I personally use [sops](https://github.com/mozilla/sops) to manage my secrets. This require `sops` and your preferred encryption tool to be installed in the ansible host machine. I use [age](https://github.com/FiloSottile/age) as my preferred sops companion. The example secret group_vars is available in [inventory/example/group_vars/all.sops.yml](./inventory/example/group_vars/all.sops.yml). This is possible by the [community.sops ansible plugin](https://github.com/ansible-collections/community.sops). The provided [ansible.cfg](./ansible.cfg) file is configured to load the plugin by default. Public key to encrypt the secret file is in [.sops.yaml](./.sops.yaml) file.

## Example playbook
```
- hosts: all
  become: true

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
    sudo_admin_group_nopasswd: true
    sudo_users:
    - username: somebody
      commands:
      - /usr/bin/cp
      - /usr/bin/mv
      - /usr/bin/touch
    ssh_packages:
    - openssh-server
    - openssh-client
    ssh_sshd_config_options:
      ChallengeResponseAuthentication: "no"
      Port: 22
    ssh_ssh_config_options:
    - hostnames: ["*"]
      options:
        Port: 22
	IdentityFile:
	- ~/.ssh/id_rsa
	- ~/.ssh/id_dca
	- ~/.ssh/id_ecdsa
	- ~/.ssh/id_ed25519
    packages_install:
      all:
      - neovim
      archlinux:
      - python-pynvim
      debian:
      - python3-neovim
      redhat:
      - python36-neovim
    dotfiles_repo_url: https://github.com/budimanjojo/dotfiles.git
    dotfiles_repo_local_path: ~/dotfiles
    dotfiles_files:
    - .zshrc
    - .tmux.conf
    gitclone_repo_add:
    - repo_url: https://github.com/budimanjojo/ansible-playbooks.git
      repo_local_path: ~/ansible-playbooks
    download_geturl_options:
    - url: https://raw.githubusercontent.com/username/repo/master/file.txt
      dest_file: ~/Downloads/file.txt
      checksum: sha256:123584564yda2fas5df31fad23afa532
    - url: https://raw.githubusercontent.com/username/repo/master/file2.txt
      dest_file: ~/Documents/file2.txt
      checksum: sha256:http://example.com/path/sha256sum.txt
      owner: somebody
      group: somebody
      backup: yes
    download_geturl_archive_options:
    - url: https://raw.githubusercontent.com/username/repo/master/file.zip
      dest_folder: ~/Downloads
      checksum: sha256:123584564yda2fas5df31fad23afa532

  roles:
  - users
  - budimanjojo.sudo
  - ssh
  - budimanjojo.packages
  - budimanjojo.dotfiles
  - gitclone
  - download
  - zinit
  - budimanjojo.vimplug
```

## License

MIT License
