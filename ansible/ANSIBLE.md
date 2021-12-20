---
title: Developer Productivity slides - Ansible
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
Use case - I have a new computer (and this is a problem).

Now I have to constantly install new libraries just to be able to start working.

You will spend the next two days (or more) setting up your computer.

Worst things about a new computer? **SSH Keys**.

---
# Installing the things I need

Ansible - a cloud configuration platform.

Make sure you are inside the `ansible` folder!

`./ansible-run.sh`

---
# Step 1

## Build the docker image

`./build-docker`

## Run the docker image

`docker run -it --rm new-computer /bin/bash`

---
# Step 2

## Run first ansible task from within the container

* `ansible-playbook local_1.yml`
* Enter `zsh`

---
# Step 3

## Install `Bazel` using `npm`

Adding `node`, `npm` and `bazel`.

* `ansible-playbook local_2.yml`

Install will fail! Ansible is trying to reinstall `zsh` etc.

---
# Step 4

## Use tags

Tagging `local_3.yml`.

* `ansible-playbook -t node local_3.yml`

As you can see you could also specify a different package manager or make a different version for a different OS.

---
# Step 5

## Making a file per task

Create a directory tasks and a task file for each task you need.

* `ansible-playbook -t node local_4.yml`

---
# Ansible playbook vs pull

If you have a `local.yml` file on your git repository you don't even need to clone your repo in order to use
`ansible-playbook`. You can do:

`sudo ansible-pull -U https://github.com/YourRepoWithAnsible.git`

---
# Where Ansible shines!

* `ansible-vault encrypt testfile`

Now your file is encrypted with a quantum secure `AES256` algorithm!

* `ansible-vault decrypt testfile`

_Type in your super secure password..._

---
# SSH keys

* `ansible-playbook -t ssh --ask-vault-pass local_5.yml`
* `cat ~/.ssh/id_rsa`

---
# Backup codes

You can do the same thing with your backup codes!

![40](images/authenticator.png)
