---
layout: post
title: bash,vim配色设置
date: 2015-08-18 11:48
tags:
  - tech
  - vim
  -linux
---

Bash
===
修改home目录下的.bash_profile,增加

```sh

alias ll='ls -lG'
PS1="\n\e[1;37m[\e[m\e[1;32m\u\e[m\e[1;33m@\e[m\e[1;35m\H\e[m \e[4m\W\e[m\e[1;37m]\e[m\e[1;36m\e[m\n\$"
export PS1

```
  
  
 
vim
===
[solarized](http://ethanschoonover.com/solarized)
[github 地址](https://github.com/altercation/vim-colors-solarized)  

在home目录创建一个~/.vim/colors文件夹,把solarized.vim文件拷贝进去  
同时建一个.vimrc文件,内容如下:

```sh

syntax enable
set background=dark
colorscheme solarized

```