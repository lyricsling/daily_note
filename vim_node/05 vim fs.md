---
tags: [Notebooks/vim]
title: 05 vim fs
created: '2023-09-16T07:19:44.409Z'
modified: '2023-09-16T07:24:37.739Z'
---

# 05 vim fs

## vim.fs.normalize()
normalize({path},{opts})
- path
  需要被标准化的目录
- opts
  expand_env: 扩展环境变量，默认为 true

```lua
vim.fs.normalize('C:\\Users\\jdoe')
--> 'C:/Users/jdoe'

vim.fs.normalize('~/src/neovim')
--> '/home/jdoe/src/neovim'

vim.fs.normalize('$XDG_CONFIG_HOME/nvim/init.vim')
--> '/Users/jdoe/.config/nvim/init.vim'
```

