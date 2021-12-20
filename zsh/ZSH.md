---
title: Developer Productivity slides - Shells
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
# Shells vs terminals

* Terminals get key input and displays text output
* Shells protect you from making anything dumb (like a shell!)

Try typing `ls -;a`:

```bash
ls: cannot access '-': No such file or directory
zsh: command not found: a
```

You can have only one terminal open but multiple shells nested inside (just open zsh inside bash).

---
# zsh

I use `zsh` because of the extensions:

* `bazel`
* `git`
* `docker`
* `docker-compose`
* `docker-machine`
* `pip`
* `sudo`
* `ubuntu`
* `zsh-autosuggestions`
* `zsh-navigation-tools`

Some plugins list:

[github.com/unixorn/awesome-zsh-plugins](https://github.com/unixorn/awesome-zsh-plugins)

---
# OhMyZsh

Saves you time off beautfying your terminal experience.

Install it using this command:

```bash
$ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Or use Ansible! :)

