---
title: git使用详解
tags: undefined
categories: preview
date: 2017-10-31 23:07:06
---

Git是一个开源的分布式版本控制系统,可以有效, 高速的处理从很小到非常大的项目版本管理. GTI使用过程中涉及文件流转的三个工作区域:Git的工作目录(project/.git),暂存区域(stage),以及本地仓库(project)[参考文档](https://git-scm.com/book/zh/v1/起步-Git-基础)

###  安装GIT
    sudo apt-get install git
   
### 配置GIT
配置文件可以是针对当天用户: ~.gitconfig;　也可以针对所有用户: /etc/gitconfig
<!-- more -->

1. 配置默认用户名邮箱(cat .gitconfig)
```
    git config user.name littleFish
    git config user.email 1226231147@qq.com
```
1. 配置默认用户名邮箱(cat /etc/gitconfig)
```
    git config --system user.name littleFish
    git config --system user.email 1226231147@qq.com
```
2. 配置别名
```
    git config --global alias.st status
```

### 基础命令
```
    git init  # 初始化
    git add readme.txt  # 添加到暂存区
    git commit -m "readme version1.0"  # 提交到本地GIT master仓库
    git push origin master  # 推送到远程分支
    
``` 
1. `git status`命令, 产看仓库当前的状态