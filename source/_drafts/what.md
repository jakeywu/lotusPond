---
title: what
tags: 
    - 草稿
    - 测试 
categories: 预发布
date: 2017-10-30 13:03:49
---

```
# !/usr/bin/env python
# -*- coding:utf-8 -*-
# Author  jakey
# Date 2017-07-11 14:11


import sys

import tornado.web
from scpy.logger import get_logger
from tornado.ioloop import IOLoop

from handler.controllers.crawler_service.emotion import ContentEmotion
from handler.controllers.crawler_service.repeation import CrawlerDescHandler, CrawlerReleaseHandler, \
    CrawlerRepeatHandler
from handler.controllers.crawler_service.content_filter import FilterCompanyNews

logger = get_logger()

Handlers = [
    ("/api/news/filter", FilterCompanyNews),  # 新闻过滤
    ("/api/news/emotion", ContentEmotion),  # 新闻正负向评分
    ("/api/news/repeatList", CrawlerDescHandler),
    ("/api/news/repeatOne", CrawlerRepeatHandler),
    ("/api/news/release", CrawlerReleaseHandler)
]

if __name__ == "__main__":
    SERVER_PORT = 7003 if len(sys.argv) < 2 else int(sys.argv[1])
    app = tornado.web.Application(Handlers)
    app.listen(SERVER_PORT, address="0.0.0.0")
    logger.info('开启tornado服务, 端口为{port}'.format(port=SERVER_PORT))
    IOLoop.current().start()


```