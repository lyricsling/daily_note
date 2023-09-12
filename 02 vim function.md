---
tags: [Notebooks/vim]
title: 02 vim function
created: '2023-09-12T13:43:24.900Z'
modified: '2023-09-12T13:58:52.477Z'
---

# 02 vim function
## vim.tbl_map({func}, {t})
对 table 中的每一个元素都执行 func 操作。
```lua
local val = {1, 3, 5, 7, 9}
local new_val = vim.tbl_map(function(map_val) map_val = map_val + 1 return map_val end, val)
print(vim.inspect(new_val)) -- {2, 4, 6, 8, 10}
```

## vim.opt_local
与之关联的是
- opt_local
- opt_global
- opt

opt_local 相当于 :setlocal，只在当前的 buffer 或者 windows 中生效
opt_global 相当于 :setglobal，只改变全局的选项，但不改变 local 中的值
