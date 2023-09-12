---
tags: [Notebooks/vim]
title: chad
created: '2023-08-30T12:48:06.402Z'
modified: '2023-08-30T14:32:44.851Z'
---

# chad
## lua/core/init.lua

他会执行以下这些步骤
- 加载配置文件
- 加载配置文件
- 设置全局变量
- 设置 opt
- 设置 mason 的安装目录
- 设置 autocmd

### 设置全局变量
	g.nvchad_theme = config.ui.theme
	g.base46_cache = "~/.local/share/nvim/nvchad/base46/"
### 赋值一些 option 变量
```lua
opt.laststatus = 3	--状态栏显示方式
opt.showmode = false
```

#### laststatus
控制是否显示状态栏
- 0：不显示
- 1：多个窗口的时候才显示
- 2：总是显示
- 3：总是显示，但只显示当前被激活窗口的状态

#### showmode
当处于 插入，替换，可视模式时，在状态栏显示所处模式的状态

#### cursorline
设置为 true 时，会高亮光标所在行

#### tab
- expandtab
	用合适的空格代替 tab
- tabstop
	 一个tab等于多少个空格，当 expandtab 的情况下，会影响在插入模式下按下<tab>键输入的空格，以及真正的 \t 用多少个空格显示；当在 noexpandtab 的情况下，只会影响 \t 显示多少个空格（因为插入模式下按 <tab> 将会输入一个字符 \t）
- softtabstop
	 按下 <tab> 将补出多少个空格。在 noexpandtab 的状态下，实际补出的是 \t 和空格的组合。所以这个选项非常奇葩，比如此时 tabstop=4, softtabstop=6 ，那么按下 <tab> 将会出现一个 \t 两个空格
- shiftwidth
	使用 >> << 或 == 来缩进代码的时候补出的空格数。这个值也会影响 autoindent 自动缩进的值。
- smartindex
cinden

#### number
- number
	行号
- numberwidth
	行号的宽度
- ruler
	显示行，列
	
#### fillchars
窗口分隔符的填充字符串
```lua
-- 这个值默认为 '~'，空行的行首填充
opt.fillchars = { eob = " " }
```
#### mouse
```lua
-- 允许鼠标操作
mouse = a
```

## lua/core/utils.lua
### remove_disabled_keys
```
remove_disabled_keys(chadrc_mappings, default_mappings)
```
把 chadrc_mappings 中有的项，在 default_mappings 中禁用掉

### load_config
 读取 lua/custom/chadrc.lua 的内容
 
 读取 core/default_config.lua 的内容
 
调用 remove_disabled_keys()

把 custom 的配置复制到 default 中

config.mappings.disabled = nil
 
return config

## lua/core/bootstrap.lua
### gen_chadrc_template
如果 lua/custom/chadrc.lua 不存在，此函数才会执行以下内容

询问，是否安装一个 example custom config

- 如果输入 y

  从 github 上下载模板，其中就包含了 chadrc.lua 这个文件

	删除 .git 文件

- 如果输入 N

  	则会先创建 /lua/custom/ 这个目录
  
	再创建 chadrc.lua 这个文件，并包含以下内容
	```
	local M = {}
	M.ui = {theme = 'onedark'}
	return M
	```
