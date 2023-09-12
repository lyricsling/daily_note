---
tags: [Notebooks/vim]
title: 04 vim opt
created: '2023-09-12T13:59:31.163Z'
modified: '2023-09-12T14:05:45.069Z'
---

# 04 vim opt
## buflisted
当前 buffer 是否存在于 buflist 之中，不在 list 的，不会在 bnext 的列表之内

## cursorline
设置为 true 时，会高亮光标所在行

## fillchars
窗口分隔符的填充字符串
```lua
-- 这个值默认为 '~'，空行的行首填充
opt.fillchars = { eob = " " }
```

## mouse
```lua
-- 允许鼠标操作
mouse = a
```
## laststatus
控制是否显示状态栏
- 0：不显示
- 1：多个窗口的时候才显示
- 2：总是显示
- 3：总是显示，但只显示当前被激活窗口的状态

## number
- number
	行号
- numberwidth
	行号的宽度
- ruler
	显示行，列

## showmode
当处于 插入，替换，可视模式时，在状态栏显示所处模式的状态

## tab
- expandtab
	用合适的空格代替 tab
- tabstop
	 一个tab等于多少个空格，当 expandtab 的情况下，会影响在插入模式下按下<tab>键输入的空格，以及真正的 \t 用多少个空格显示；当在 noexpandtab 的情况下，只会影响 \t 显示多少个空格（因为插入模式下按 <tab> 将会输入一个字符 \t）
- softtabstop
	 按下 \<tab\> 将补出多少个空格。在 noexpandtab 的状态下，实际补出的是 \t 和空格的组合。所以这个选项非常奇葩，比如此时 tabstop=4, softtabstop=6 ，那么按下 <tab> 将会出现一个 \t 两个空格
- shiftwidth
	使用 >> << 或 == 来缩进代码的时候补出的空格数。这个值也会影响 autoindent 自动缩进的值。
- smartindex
cinden



