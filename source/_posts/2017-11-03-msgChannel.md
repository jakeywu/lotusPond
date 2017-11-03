---
title: 消息通道
comments: true
tags: 
    - 消息通道
    - NSQ
    - RabbitMQ
categories: 开源工具
date: 2017-11-03 17:41:18
updated: 2017-11-03 17:41:18
---


消息中间件利用高效可靠的消息传递机制进行平台无关的数据交流,并基于数据通信来进行分布式系统的集成.通过提供消息传递和消息排队模型,它可以在分布式环境下扩展进程间的通信.通常会遵从[AMQP协议](http://blog.csdn.net/u011301203/article/details/52356166). AMQP,即Advanced Message Queuing Protocol,一个提供统一消息服务的应用层标准高级消息队列协议,是应用层协议的一个开放标准,为面向消息的中间件设计.基于此协议的客户端与消息中间件可传递消息,并不受客户端/中间件不同产品,不同的开发语言等条件的限制.Erlang中的实现有 RabbitMQ等. 现有的基于AMQP协议的中间件有很多, 可参考: [Queue队列](http://queues.io/).
- 消息系统的作用: 异步处理, 削减峰值, 减少组件之间的耦合. 选择消息系统考虑如下方面
1. 是否持久化
2. 吞吐能力
3. 高可用
4. 分布式扩展能力
5. 兼容现有协议
6. 易于维护
7. 避免单节点故障
8. 负载均衡
9. 其他(消息丢失和重复处理)

<!-- more -->

- 常见的消息系统的协议有
1. STOMP
2. AMQP
3. HTTP

- 常见的消息系统有, 可以参考[Queue队列](http://queues.io/)
1. Active mq
2. RabbitMQ
3. Apollo
4. Beanstalkd
5. Gearman
6. Apache Kafka
7. NSQ

# RabbitMQ介绍
[RabbitMq](https://www.rabbitmq.com/tutorials/tutorial-one-python.html)遵从ampq协议, amqp(advanced message queueing protocol)协议. 高级消息队列协议, 主要特征为面向消息，队列，路由(点对点, 发布和订阅),可靠安全. 是用erlang语言编写，用于在分布式系统中存储和转发消息
- 几种典型的使用场景如下. [demo](https://github.com/jakeywu/jakeywutility)
1. 单发送单接收，　不做任何处理　　＂Hello World＂
2. 单发送，　多个接收　(分布式任务派发，　消息处理完之后ack)   (Work Queues)
3. 发布，订阅模式，　发送端发布广播消息，　多个接收端接收     (Publish/Subscribe)
4. 按线路发送和接收消息，其中交换机type=dict，发送接收端都按照不同的routing key收发消息(Routing)
5. 按topic发送接收消息，其中交换机type=topic，发送接收端按字符串匹配模式收发消息(Topic)
6. RPC(远程调用方法，　同步，　基本不用了, Rest api接口取代)
