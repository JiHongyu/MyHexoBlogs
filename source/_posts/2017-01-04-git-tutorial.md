---
title: git_tutorial
date: 2017-01-04 08:56:49
tags: [git]
---

Git 是牛逼的软件开发版本控制系统，学习它是大大的好

<!--more-->

# 配置 Git 与 Github 连接

1.生成 SSH Key
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

2.把 SSH Key 加入 SSH 代理（可选）
```bash
eval $(ssh-agent -s)  #保证 ssh-agent 处于运行中
ssh-add ~/.ssh/id_rsa
```

3.将 .ssh/id_rsa.pub 文件内的内容粘贴至个人Github配置中去。

（Settings -> SSH and GPG keys -> New SSH key）

4.连接测试
```bash
ssh -T your_email@example.com
```

# Git 基本术语

工作区：当前项目工作目录下，除了 `.git` 文件夹下的所有内容。

版本库：`.git` 文件下的所有东西，里面包含了暂存区和分支区

暂存区：虚拟工作区，跟踪工作区文件的变化。由 index 文件维护。

分支区：保存分支信息的地方，暂存区的内容经过 commit 后会产生新的分支。HEAD 一般指向最新commit的引用，可以通过版本回退的方式改变HEAD的指向

# 基本使用方法

git init: 将当前目录设置为 git 仓库。它会生成一个 `.git` 文件夹。

git add: 添加文件到暂存区。

git commit: 将暂存区文件提交到本地仓库。

git diff: 对比文件。只能对比文本文件，二进制文件就无能为力了。

git status: 查看仓库状态。

git log: 查看历史记录。

git reset: 版本退回。

git checkout: 从暂存区或者分支中迁出文件。

# 参考文献

[Git使用教程](http://www.cnblogs.com/tugenhua0707/p/4050072.html)
[Git 菜鸟变大神 （三） 工作区、暂存区、版本库之间的关系案例](http://www.cnblogs.com/lilongsheng1125/p/4978479.html)



