---
tags: [Notebooks/vim]
title: 03 vim api
created: '2023-05-18T11:31:45.814Z'
modified: '2023-09-16T07:54:31.791Z'
---

# 03 vim api
## vim.api.create_buf()
```vim
nvim_create_buf({listed}, {scratch})
```
- 参数：listed 
 	创建的 buffer 放入 bufferlist 中
- 参数：scrath
	throwaway，临时使用的 buffer

## vim.api.nvim_buf_get_name()
nvim_buf_get_name({buffer})
- buffer
  需要获取名字的 buf,0 为当前 buf

## vim.api.nvim_create_autocmd()
nvim_create_autocmd({event}, {*opts})
event 触发时，执行 callback

callback 方式
```lua
vim.api.nvim_create_autocmd({"BufEnter", "BufWinEnter"}, {
  pattern = {"*.c", "*.h"},
  callback = function(ev)
    print(string.format(vim.inspect(ev)))
  end
})
```

参数 ev 的结构如下
```lua
buf = 1,
event = "BufWinEnter",
file = "/home/llx/lyrics_lab/nvim_lua/api_vim_test.lua",
id = 102,
match = "/home/llx/lyrics_lab/nvim_lua/api_vim_test.lua"
```

command 方式
```lua
vim.api.nvim_create_autocmd({"BufEnter", "BufWinEnter"}, {
  pattern = {"*.c", "*.h"},
  command = "echo 'Entering a C or C++ file'",
})
```



## vim.api.nvim_get_current_line()
```
nvim_get_current_line()
```
获取当前行

## vim.api.nvim_get_runtime_file()
```
nvim_get_runtime_file({name}, {all})
```
在运行目录下查找指定的文件
- 参数: name
  需要查找的文件名
- 参数：all
  是否返回所有的查找结果,或者返回第一个查找到的结果

``` vim
vim.api.nvim_get_runtime_file("lua/custom/*.lua", true)
```

## vim.api.nvim_win_get_cursor({window})
```
nvim_win_get_cursor({window})
```
获取指定窗口的光标位置（x, y-1）
vim.api.nvim_win_get_cursor({window})

(x, y) 返回dict
vim.fn.screenpos(0, x, y) -- 

|  dict  |  |
| ---  | --- | 
| row	  |		screen row  |
| col   |			first screen column |
| endcol|		last screen column  |
| curscol|		cursor screen column  |













### keymap
```vim
nvim_buf_set_keymap({buffer}, {mode}, {lhs}, {rhs}, {*opts})

```
buffer, 0 代表当前buffer

```vim
nvim_buf_get_keymap({mode})
```
### autocmd 相关
```vim
nvim_create_augroup({name}, {*opts})
```
- {name} 组名
- {opts}
  - clear 是否清除组中已有的命令
  
```
  local id = vim.api.nvim_create_augroup("MyGroup", {
    clear = false
})
```
组的作用：方便更好的对自动命令进行管理

当你 source plugin 多次，autocommand 会累加，加入组的概念会避免累加。

autocommand,对于某些事件，自动执行一些命令。


#### vim cmd
```cpp
# vim.cmd 可以拆分为下面两个指令
vim.cmd(command) 
vim.api.nvim_cmd(table)
vim.api.nvim_exec(string)

```


Before getting into the this topic, first you should understand the vim.tbl_deep_extend function which is used for merging tables and their values recursively.

    The function vim.tbl_deep_extend is normally used to merge 2 tables, and its syntax looks like this:

-- table 1
local person = {
    name = "joe",
    age = 19,
}

-- table 2
local someone = {
    name = "siduck",
}

-- "force" will overwrite equal values from the someone table over the person table
local result = vim.tbl_deep_extend("force", person, someone)

-- result : 
{
    name = "siduck", -- as you can see, name has been overwritten
    age = 19,
}


Its usage can even be used in more complex tables. As said, it works recursively, which means that it will apply the same behaviour for nested table values:

local person = {
    name = "joe",
    age = 19,
    skills = {"python", "java", "c++"}

    distros_used = {
        ubuntu = "5 years",
        arch = "10 minutes",
        manjaro = "10 years",
    }
}

local someone = {
    name = "siduck",
    skills = {"js", "lua"},

    distros_used = {
       ubuntu = "1 month",
       artix = "2 years"
    }
}

local result = vim.tbl_deep_extend("force", person, someone)


The resulting table will have merged each property from the tables, and the same for the skills and distros_used values:

{
   name = "siduck",
   age = 19

   skills = {"js", "lua"},

   distros_used = {
       ubuntu = "1 month",
       arch = "10 minutes",
       manjaro = "10 years",
       artix = "2 years"
   }
}

-- tbl_deep_extend function merges values recursively, but if there's an array (list), it won't merge the list tables. 

-- Example: the first table has {"python", "java", "c++"} and the second table has {"js","lua"}. 

-- Now you might be wondering that it should merge it like this: { "python", "java", "c++", "lua"}

-- But no! thats wrong, the result will be only {"js","lua"}


To sum up, tbl_deep_extend merges dictonary tables recursively (i.e tables which have key/value pair but not lists).


dofile({filename})
dofile()
Opens the named file and executes its contents as a Lua chunk. When called without arguments, dofile executes the contents of the standard input (stdin). Returns all values returned by the chunk. In case of errors, dofile propagates the error to its caller (that is, dofile does not run in protected mode). 

