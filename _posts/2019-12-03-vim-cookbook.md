---
title: Vim cookbook
category: Unix/Linux
---

This post documents useful commands for working with the [Vim text editor](https://www.vim.org/). Some of this content is adapted from the [Vim help pages](https://vimhelp.org/). 

For a better reading experience, see [Learning the vi and Vim Editors](http://shop.oreilly.com/product/9780596529833.do).

## Open the editor

Open a file:

    vim example.txt


Open the help pages:

    vim<Enter> :help<Enter>

## Move around

Use the cursor keys or:

      k
    h   l
      j

## Toggle between modes

From Normal (i.e. command) mode, enter Insert mode:

    i

From Insert mode, return to Normal mode:

    <Esc>    

## Quit and (optionally) save

Quit and don't save:

    :q!

Quit and save:

    :wq

Save:

    :w

## Delete text

Delete a character:

    x

Delete 5 characters at the cursor and after:

    5x

Delete a line:

    dd

Delete five lines:

    5dd

## Copy and paste

Copy a line to the register:

    yy

Copy 5 lines to the register:

    5yy

Paste the register after the cursor:

     p