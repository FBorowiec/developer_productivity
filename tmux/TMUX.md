---
title: Developer Productivity slides - Terminals and terminals multiplexers
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
# Terminals

Very personal, I personally use Alacritty for the following reasons:

* sensible defaults
* extensive configurability
* VI mode - move around and create selections using vi bindings
* Search for any text withing the scrollback buffer

---
# Tmux

![60](images/tmux-server.png)

At the base there's a tmux server.

Each server can have multiple sessions etc.

---
# First try

* `sudo apt install tmux`
* `tmux`

## Basic commands

Prefix: `Ctrl+b` (I recommend to leave this default)

* `tmux list-sessions`
* `tmux kill-server`
* `tmux`
* `<prefix> d` - tmux detach
* `tmux a` - attach

---
# Sessions, Windows, Panes (Splits)

* `<prefix> w` - tmux status
* `<prefix> c` - new-window

## Navigating between windows

* `<prefix> n` - next window
* `<prefix> p` - previous window
* `<prefix> l` - last window
* `<prefix> L` - last session
* `<prefix> 1..0` - go to `1..0` window
* `<prefix> ,` - rename window
* `<prefix> $` - rename session
* `<prefix> &` - kill window

## Panes (Splits)

* `<prefix> v` - vertical split
* `<prefix> s` - horizontal split

I don't use them and they're inverted respective to how vim treats splits.

---
# Tmux scripting

* `tmux new-session -s "foobar" -d -c "$HOME/dev/developer_productivity"` - create a new session in a specific directory
* `tmux new-window -n "foobar" -c "$HOME/dev"`
* `tmux switch-client -t "foobar"` - switches sessions
* `tmux new-window -n "foobar" [some command goes here]`

As you can see there's potential for scripting some tmux commands.

`cht.sh`

