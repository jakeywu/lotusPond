---
title: markdown
tags: 
    - oo
    - 测试
categories: 预发布
date: 2017-10-27 16:26:07
---



下载单个文件, 默认将输出打印到标准输出(STDOUT)中...
curl http://www.centos.org

将文件保存到baidu.html中
curl -o baidu.html  http://www.baidu.com

使用URL中默认的文件名保存文件到本地
curl -O http://www.gnu.org/software/gettext/manual/gettext.html

如果默认不是文件名, 而是路径. 采用-O会拋错
```curl -O http://www.baidu.com
   curl: Remote file name has no length!
   curl: try 'curl --help' or 'curl --manual' for more information
```

<!-- more -->

同时获取多个文件
curl -O URL1 -O URL2

<!-- more -->
curl默认不会重定向, 采用-L进行重定向
curl -L http://www.google.com

通过使用-C选项可对大文件使用断点续传功能
```curl -C - -O http://www.gnu.org/software/gettext/manual/gettext.html
```

通过--limit-rate选项对CURL的最大网络使用进行限制
```curl --limit-rate 1000B -O http://www.gnu.org/software/gettext/manual/gettext.html
```

在访问需要授权的页面时，可通过-u选项提供用户名和密码进行授权(通常的做法是在命令行只输入用户名，之后会提示输入密码)
curl -u username:password URL

CURL同样支持FTP下载，若在url中指定的是某个文件路径而非具体的某个要下载的文件名，CURL则会列出该目录下的所有文件名而并非下载该目录下的所有文件
curl -u ftpuser:ftppass -O ftp://ftp_server/public_html/


-H/--header <line>              自定义头信息传递给服务器
-X/--request <command>          指定什么命令
-d/--data <data>                  HTTP POST方式传送数据

现实详细请求头
curl -I http://domain.com
