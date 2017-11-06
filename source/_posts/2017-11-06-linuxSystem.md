---
title: linux系统配置
comments: true
tags: linux系统配置
categories: Linux
date: 2017-11-06 14:55:20
updated: 2017-11-06 14:55:20
---


### 查看和修改Linux的时区
1. 查看当前时区
```
    # Mon, 06 Nov 2017 16:51:54 +0800 代表本地时间 
    "date -R"
```
2. 修改当前时区
* 方法1. 终端输入`tzselect`
* 方法2. 终端输入`timeconfig`, 仅限于RedHat Linux 和 CentOS
* 方法3. 终端输入`dpkg-reconfigure tzdata`, 适用于Debian

### 开启cron日志, ubuntu默认没有开启cron日志记录
1. 修改rsyslog, 将`cron.* /var/log/cron.log`前面的注释符去掉
```
    sudo vim /etc/rsyslog.d/50-default.conf
``` 
2. 重启cron服务和rsyslog 
```
    sudo service cron restart  
    sudo service rsyslog restart 
```
3.查看crontab日志 
```
    less /var/log/cron.log
```
