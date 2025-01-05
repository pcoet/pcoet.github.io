---
draft: false
date: 2019-12-03
categories:
  - Vim
  - Unix/Linux
tags:
  - tools
---

# Vim cookbook

*Last updated: December 8, 2019*

This post documents useful commands for working with the [Vim text editor](https://www.vim.org/). Some of this content is adapted from the [Vim help pages](https://vimhelp.org/). For a more fully developed intro to Vim, see [Learning the vi and Vim Editors](http://shop.oreilly.com/product/9780596529833.do).

## Why Vim?

Many Vim commands are not intuitive for users of modern text editors, and Vim doesn't have anything like the feature set of a modern IDE. So why use it? Two reasons:

  1. Vim is ubiquitous on Unix and Linux machines.
  1. It serves as a really fast way to edit files when you're working in a shell. 

If you've ever needed to do remote debugging of a Linux machine, you'll probably understand why Vim can be useful.

## Basics

The sections below assume that you know how to work in a Unix/Linux environment, and that you understand [Vim modes](http://vimdoc.sourceforge.net/htmldoc/intro.html#vim-modes-intro).

### Opening the editor

Open a file:

    vim example.txt


Open the help pages:

    vim<Enter> :help<Enter>

### Toggling between Normal mode and Insert mode

From Normal (i.e. command) mode, enter Insert mode:

    i

From Insert mode, return to Normal mode:

    <Esc>    

To learn more about modes, see [Vim Modes](https://guide.freecodecamp.org/vim/modes/) and [Modes](https://en.wikibooks.org/wiki/Learning_the_vi_Editor/Vim/Modes).

### Moving around

Use the cursor keys or:

      k
    h   l
      j

### Quitting and (optionally) saving

Quit and don't save:

    :q!

Quit and save:

    :wq

Save:

    :w

### Deleting text

Delete a character:

    x

Delete 5 characters at the cursor and after:

    5x

Delete a line:

    dd

Delete five lines:

    5dd

Delete all lines in the file/buffer:

    :1,$d

### Copying and pasting

Copy a line to the register:

    yy

Copy 5 lines to the register:

    5yy

Paste the register after the cursor:

     p

## Config

There are some pretty creative ways to configure Vim, if you want to use it for serious software development. The first thing to know is [where to find your .vimrc file](https://stackoverflow.com/questions/10921441/where-is-my-vimrc-file).

### Adding config

Create (or open) your **.vimrc**:

    vim ~/.vimrc

If you want some good basic config, paste in the contents of [basic.vim](https://raw.githubusercontent.com/amix/vimrc/master/vimrcs/basic.vim).

Alternatively, you could start with this [minimal example](https://vim.fandom.com/wiki/Example_vimrc).