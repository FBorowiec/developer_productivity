---
title: Developer Productivity slides - Vim (Vi IMproved)
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
# Where to find everything that will be presented

Github: [github.com/FBorowiec](https://www.github.com/FBorowiec)

```qrcode
https://www.github.com/FBorowiec/developer_productivity
```

Prerequisites:

**A Linux OS**
---
# Imtroduction (Introduction improved)

## Why use VIM?

### Mastering your editing tool

INSERT THE PRAGMATIC PROGRAMMER QUOTE HERE

![25](images/learning_curves.jpg)

It's highly configurable and you can have an editor that's just like you want it.

BUT it's a long term investment.

INSERT HERE MASTERING CURVE

### Speed

That's it essentially - you won't be a better programmer, you'll be faster.

### LSP

Any language with a language server protocol can have their LSP used by VIM.
---
# Flavors of VIM

* VIM - Vi IMproved
* NeoVim
* SpaceVim
* LunarVim
---
# First steps

`vimtutor`
---
# Fundamentals - Files, Buffers, Windows, Splits

## Buffers

Representation of the file in memory.
When you edit a buffer you are editing a representation of the file.
When you write your buffer you overwrite the file in memory.

`:h buffer`

## Windows

A window is a buffer representation.
Windows can be closed but the underlying buffer can remain in memory.

## Splits

A split of a window.

You can create a vertical split by using:

`<C-w>v`

And a horizontal one by using:
`<C-w>s`
---
# Are you ready?

* This is a journey, not a day trip
* The journey is uphill
* The top of the mountain is incredible
---
# How to start

1. `vimtutor`
2. VIM extension in VS Code or CLion
---
# Vim modes

* Normal `<esc>`
* Insert `i`
* Visual
  * Visual line `<S-v>`
  * Visual block `<C-v>`
* Command `:`
* Window `<C-w>`
* Replace `R` <-- I never use it
* Ex <-- nobody knows what's it for
---
# Basic

## Movements

DON'T USE YOUR MOUSE AND DON'T USE ARROWS

`h, j, k, l` - move over character

`w, b, e` - move over words

`W, B, E` - move over whitespaces

`<C-o>`, `<C-i>` - move to prev/next change (jumplist)

`<C-d>`, `<C-u>` - page up/down

`{`, `}` - move through a block of code

`%` - move from `<,(,{,[` to `>,),},]`

`f, t, F, T` - find character

`/` - search, then `n, N`

`<C-^>` - move to last edited file

## Copy (yanking) pasting

`yy, Y, p, P`

## Entering insert mode

`i, I, a, A, o, O, c, C`, insert, append, line below, change

## Relative numbers / Combining numbers with commands

`10j`
`6dd`
---
# `init.lua` or `init.vim`

_setup presentation_
---
# Quickfix

* `<leader>fg` - Telescope grep
* `<C-q>` - Add results to quickfix list
* `:cfdo %s/ORIGINAL/REPLACEMENT/g | update` - replace within the qf-list
---
# Macros

* Record a macro using `q` + letter: `qd` - records to the register called `d`.
* Stop recording by pressing `q` in normal mode.
* Run macro n times using `19@d` - runs macro 19 times.
---
## Simple macro replace

### First using sed

```cpp
if (some_value == "some_other_value1") {
    return 1
} else if (some_value == "some_other_value2") {
    return 2
} else if (some_value == "some_other_value3") {
    return 3
} else if (some_value == "some_other_value4") {
    return 4
} else if (some_value == "some_other_value5") {
    return 5
} else if (some_value == "some_other_value6") {
    return 6
} else if (some_value == "some_other_value7") {
    return 7
} else if (some_value == "some_other_value8") {
    return 8
} else if (some_value == "some_other_value9") {
    return 9
} else if (some_value == "some_other_value10") {
    return 10
} else if (some_value == "some_other_value11") {
    return 11
} else if (some_value == "some_other_value12") {
    return 12
} else if (some_value == "some_other_value13") {
    return 13
} else if (some_value == "some_other_value14") {
    return 14
} else if (some_value == "some_other_value15") {
    return 15
} else if (some_value == "some_other_value16") {
    return 16
} else if (some_value == "some_other_value17") {
    return 17
} else if (some_value == "some_other_value18") {
    return 18
} else if (some_value == "some_other_value19") {
    return 19
} else if (some_value == "some_other_value20") {
    return 20
}
```

* Visually select the code
* Press `:` -> `:'<,'>`
* `:'<,'>s/.*"\(.*\)".*/case "\1":`
---
### Using a macro

* `qd` - record macro to `d`
* `0` - go to beginning of the line
* `dt"` - delete to `"`
* `f"` - find `"`
* `l` - move on character to the right
* `D` / `d$` - delete till end of line
* `A` - append at the end of the line
* type `:` - text to append
* `I` - insert at beginning of line
* type `case` - text to insert
* `jj` - move to lines below
* `q` - finish recording
---
