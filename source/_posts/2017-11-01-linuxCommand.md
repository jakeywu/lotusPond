---
title: linux常用命令
comments: true
tags: linux常用命令
categories: linux
date: 2017-11-01 19:42:24
updated: 2017-11-01 19:42:24
---


在日常开发过程中, 会使用到很多linux命令. 在不熟悉的linux的情况下, 记录下常用的Linux命令对自己很有帮助. 
### Linux常用命令
* 更新系统软件, 很多重要的软件安装之前, 都建议先更新系统软件
```
    sudo apt-get upgrade
    sudo apt-get update
```
* 产看linux版本号或者内核
<!-- more -->
```
    cat /etc/issue
    lsb_release -a   
    uname -r
    查看更多信息
    uname --help
```
* 右键打开终端, 多屏操作, 需安装
```
    sudo apt-get install nautilus-open-terminal
```
* 查看磁盘使用情况以及挂载点
```
    df -hl
```
* 查看某端口号使用情况
```
    lsof -i:8001
```
* 查看此终端历史命令, 执行某一条历史命令
```
    history 
    !1046
```
* 解压压缩包.  tar高效率,linux应用广泛; zip跨平台
```
    压缩doc目录为doc.zip
    zip  -r doc.tar.gz doc
    zip  -r doc.tar doc
    tar -cvf doc.zip doc
    
    解压doc.zip到当前目录
    unzip doc.zip 
    tar -xvf doc.tar
    tar -xvf doc.tar.gz
```
* 卸载软件(卸载某个指定软件和自动卸载多余的软件)
```
    sudo apt-get purge nginx-core
    sudo apt-get autoremove
    # 修复某个以来关系
    sudo apt-get -f install
```
* 启动/重启/停止某个系统服务
```
    sudo service superviser start/restart/stop
```
* 压力测试脚本(20个客户端并发1000个请求)
```
    sudo apt-get install apache2-utils  
    ab -c 20 -n 1000
```
* 命令拷贝, 防止手动拷贝造成格式误差
```
    sudo apt-get install xclip
    xclip -sel clip < ~/.ssh/id_rsa.pub
```
* 安装和启动memcache缓存服务
```
    sudo apt-get install memcached
    /usr/bin/memcached -m 64 -p 11211 -u memcache -l 127.0.0.1
```
* ubuntu应用桌面快捷显示 `sudo gedit /usr/share/applications/dbeaver.desktop` [更多可以参考官网](https://help.ubuntu.com/community/UnityLaunchersAndDesktopFiles)
```
    [Desktop Entry]
    Version=1.0
    Name=dbeaver
    Comment=mysql management develop
    Exec=/opt/local/dbeaver/dbeaver
    Icon=/opt/local/dbeaver/icon.xpm
    Terminal=false
    Type=Application
    Categories=Application;Development;
```

