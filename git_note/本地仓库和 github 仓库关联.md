---
tags: [Notebooks/Git]
title: 本地仓库和 github 仓库关联
created: '2023-08-29T00:50:27.117Z'
modified: '2023-08-29T02:14:36.210Z'
---

# 本地仓库和 github 仓库关联
在本地生成一个 ssh 密钥对
```
ssh-keygen -t ed25519 -C 'youremail@xxx.com'
```
一路默认，点确定，生成密钥。
打开生成的文件 /c/Users/LC-47/.ssh/id_ed25519.pub

在 Github 上打开 Setting - SSH and GPG keys
把生成文件的内容拷贝到 “New SSH key” 中，点击确定，就添加成功了

建立完成后，就可以通过终端操作 Github 仓库, 而不需要输入密码了

在 Github 上创建一个远程仓库。

在本地创建一个仓库。

把本地仓库和远程仓库关联
```
git remote add origin 'your_github_repository.git'
```

由于 Github 上创建的仓库主分支名称为 main。
而本地创建的仓库的主分支名称为 master。

需要把本地分支的名称从 master 改为 main
```
git branch -m master main
```

由于远程服务器上已有提交（创建的Readme文件），本地也有提交，此时 pull 和 push 会失败
```
git pull --rebase origin main
```
把远程的提交，rebase 到本地来

最后，就可以 pull 拉取远端代码， push 推送本地代码到远端了。
