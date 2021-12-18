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

./ansible/ansible-run.sh
---
# Step 1

## Build the docker image

`docker build -t framaxwlad/ansible ansible`

## Run the docker image

`docker run -it --rm --name ansible framaxwlad/ansible /bin/bash`
---
# Step 2

## Run first ansible task

`ansible-playbook ansible/dev_prod.yml`
