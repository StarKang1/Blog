---
title: git基本指令
abbrlink: 51637
date: 2022-02-10 15:40:11
tags:
 - git
 - 基本指令
categories: 笔记
cover: https://picsum.photos/id/9/300/300
---

git init 在想要创建repositoory的地方点击Git Bash
git status 查看变化/状态
git add -A 添加<file>
再次查看状态，提示changes to committed
git commit -m"添加你的备注，或者你修改了什么"
运行git log可以查看提交记录
git diff 查看文件做了哪些变化
git checkout -- .撤销修改
git reset --hard 版本号前7位 执行版本回退
git reflog 查看HEAD版本变化
再次git reset --hard 最新版本号
回到最新的版本
git clean -xf 删除没有add的文件

如果你的文件名是中文的可能会乱码，执行以下代码
git config --global i18n.commitencoding utf-8
git config --global i18n.logoutputencoding utf-8

本地git和github的链接
1.github注册账号
2.配置你的用户和邮箱：git config --global user.name "用户名"
		   git config --global user.email“邮箱”
3.生成ssh key
  运行ssh-keygen -t rsa -C"email"
  将生成的ssh key复制，执行clip < ~/.ssh/id_rsa.pub
4.ssh -T git@github.com
查看是否链接成功
5.首次提交 git remote add origin git@你的github库地址
6.git push -u origin master 提交
去github上就可以看到更新