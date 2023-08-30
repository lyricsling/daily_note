---
tags: [Notebooks/vim]
title: chad
created: '2023-08-30T12:48:06.402Z'
modified: '2023-08-30T14:25:42.740Z'
---

# chad
 
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
如果输入 y
	从 github 上下载模板，其中就包含了 chadrc.lua 这个文件
	删除 .git 文件
如果输入 N
	先创建 /lua/custom/ 这个目录
	再创建 chadrc.lua 这个文件，并创建以下内容
	```
	local M = {}
	M.ui = {theme = 'onedark'}
	return M
	```
