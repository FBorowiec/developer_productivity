---
title: Developer Productivity slides - Git magic features
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

1. You're currently writing tests on some branch
2. You need to fix some other branch that failed some CI checks
3. You stash your changes
4. You checkout the other branch
5. Make changes
6. Build
7. Checkout the original branch
8. Pop the stash
9. Rebuild

---
# Git worktrees

A worktree is a named commit.

You have to clone your repo using the `--bare` option.

`git clone --bare git@github.com:FBorowiec/developer_productivity.git`

## Let's learn a little about worktrees

`curl cht.sh/git~worktree`

Check current worktrees:

`git worktree list`

Create a new directory with the specified branch checked out into it:

`git worktree ad {{path/to/directory}} {{branch}}`

Create a new directory with a new branch checked out into it:

`git worktree ad {{path/to/directory}} -b {{branch}}`

Remove a worktree (after deleting worktree directory):

`git worktree prune`

---
# Example

* `git worktree add foo -b foo`
* `cd foo`
* Now you can have separate builds for all your branches!
