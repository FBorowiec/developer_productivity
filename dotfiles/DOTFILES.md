---
title: Developer Productivity slides - Dotfiles
author: F.Borowiec
date: 2021-12-16
extensions:
    - qrcode
    - image_ueberzug
styles:
    style: paraiso-dark
    table:
        column_spacing: 3
        header_divider: "-"

---
# Use case

1. Programs we use with our configuration
2. Keep track and commit changes over time
3. Compatible with any OS

---
# What are dotfiles?

A configuration file of your program.

Example for `~/.config/nvim/init.vim`:

```viml
set tabstop=4 softtabstop=4
set shiftwidth=4
set expandtab
set smartindent
```

---
# GNU/Stow

It's simple! -> it only manages simlinks (therefore is OS and version-able).

![50](images/stow.png)

---
# Stow example

* `cd dotfiles/target_dir/stow_dir`
* `stow nvim`
* `find .`

As you can see nothing changes under `stow_dir`. But now check the `target_dir`.

* `cd ..`
* `ls -la`

You can also unstow a directory:

* `stow -D nvim`

And stow is smart enough to abort when you have conflicting tree structures :)

---
# Stow with Ansible

An example of `dotfiles.task`:

## `dotfiles.task`

```Ansible
- name: Installing stow
  apt: name=stow
  tags:
    - install
    - dotfiles
    - stow
- name: Cloning .dotfiles
  ansible.builtin.git:
    repo: 'git@github.com:FBorowiec/dotfiles.git'
    dest: "{{ lookup('env', 'HOME') }}/.dotfiles"
    recursive: yes
    update: yes
    accept_hostkey: yes
    version: master
  tags:
    - install
    - dotfiles
    - stow
- name: Stow dotfiles
  shell: cd $HOME/.dotfiles && ./install
  tags:
    - install
    - dotfiles
    - stow
```

---
# `install`

```zsh
#!/usr/bin/env bash

if [[ -z $STOW_FOLDERS ]]; then
    STOW_FOLDERS="alacritty,discord,dwm,git,mutt,nvim,ranger,rofi-spotlight,scripts,spotify,terminator,tmux,zsh"
fi

if [[ -e $HOME/.zshrc ]]; then
    rm $HOME/.zshrc
fi

for folder in $(echo $STOW_FOLDERS | sed "s/,/ /g")
do
    stow -D $folder
    stow $folder
done

```

**VERDICT**: Stow is better.

