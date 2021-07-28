# ansible vimplug role

Role to install [vim-plug](https://github.com/junegunn/vim-plug) and vim plugins. It's better if you remove all the vim-plug related lines in your `.vimrc` file before running this role.

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
vimplug_become: whether to run as root or not, default is no (bool)
vimplug_vim_cmd: vim command name, default to 'vim' (string)
vimplug_vim_datadir: vim data directory, default to '~/.vim' (string)
vimplug_vimrc_path: path of .vimrc file, default to '.vimrc' (string)

## List of packages needed for vim-plug, ignore this if you're not sure
vimplug_packages: []

## List of vim plugins to install
vimplug_plugins
- name: name of the plugin (string)
  options:
  - key: value (string)
```

## Example playbook

Here is an example playbook:
```
- hosts: all

  vars:
    vimplug_vim_cmd: nvim
    vimplug_vim_datadir: ~/.config/nvim
    vimplug_vimrc_path: ~/.config/nvim/init.vim
    vimplug_plugins:
    - name: nsf/gocode
      options:
      - tag: v.20150303
      - rtp: vim
    - name: neoclid/coc/nvim
      options:
      - branch: release
    - nama: junegunn/vim-easy-align

  roles:
  - vimplug
```

## Licence

MIT License
