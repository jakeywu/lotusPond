---
title: docker入门知识
comments: true
tags: 
    - docker  
    - 微服务
categories: 开源工具
date: 2017-11-07 14:58:59
updated: 2017-11-07 14:58:59
---

简要描述: 传统虚拟化是虚拟一套硬件, 在上面运行一个完整的操作系统, 最后再运行进程. Docker容器是直接运行于宿主的内核,无需硬件虚拟化, 更高效的利用系统资源, 更快速的启动时间, 一致的运行环境, 持续交付和部署.

参考资料:

1. [Docker从入门到实践](https://yeasy.gitbooks.io/docker_practice/content/)

### Docker镜像, 容器, 仓库
* Docker自动安装
```
    curl	-sSL	https://get.docker.com/	|	sh
    sudo service docker restart
```
<!-- more -->
* 列出所有镜像
```
    sudo docker images
```
* 列出部分镜像
```
    sudo docker images ubuntu:14.04
```
* 查看正在运行的容器
```
    sudo docker ps
```
* 以bash进入正在运行的容器
```
    sudo docker exec -it [容器名字] bash
```
* 停止正在运行的容器
```
    sudo docker stop [容器名字]
```
* 移除某个容器
```
    sudo docker rm [容器名字]
```
* 删除主机中的某个镜像
```
    sudo docker rmi [镜像名字]
```
* 查看容器的改动
```
    sudo docker diff [容器名字]
```
* 将最新容器保存为镜像
```
    sudo docker commit --author "email" --message "修改了默认首页" webserver nginx:owner
```
* 查看镜像内的历史记录
```
    sudo docker history nginx:owner
```
* 清理所有处于终止状态的容器
```
    docker	rm	$(docker	ps	-a	-q)
```
* 显示容器进程ID
```
    echo $(docker-pid c3b653f51afc)
```
* 进入容器
```
    docker-enter c3b653f51afc
```

### 镜像的基本使用方式
* 获取ubuntu镜像
```
    sudo docker pull ubuntu:14.04
```
* 启动容器ubuntu:14.04 并进行交互式操作
```
   sudo docker run -it --rm ubuntu:14.04 bash
   备注: -i 让容器的标准输入保持打开   -t: 终端    --rm  容器退出之后删除   ubuntu:14.04镜像作为基础来启动容器   bash  交互式Shell 
```
* 以nginx镜像为基础启动容器
```
    sudo docker run --name webserver -d -p 90:80 nginx
    备注: -d 以守护进程方式运行    -p[主机端口][容器端口] 指定端口号
```