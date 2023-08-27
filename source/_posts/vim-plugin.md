---
title: 记录一下自己使用的vim配置和插件
date: 2023-07-08 18:17:19
tags: vim
---

## fzf插件

```
Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }
Plug 'junegunn/fzf.vim'
```

```
nnoremap <silent> <c-p> :Files <CR>
```
全范围搜索文件名

## airline主题
```
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
```

## 目录栏插件
Plug 'preservim/nerdtree', { 'on': 'NERDTreeToggle' }


