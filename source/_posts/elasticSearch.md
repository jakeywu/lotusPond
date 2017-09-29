---
title: elasticSearch
date: 2017-06-08 19:53:01
tags:
---
[ElasticSearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started.html)ElasticSearch是
一个基于[全文检索引擎工具包 Lucene](http://baike.baidu.com/item/Lucene)的可扩展, 分布式, 实时的搜索与数据分析引擎. Elasticsearch
是用Java开发的，并作为Apache许可条款下的开放源码发布，是当前流行的企业级搜索引擎. 设计用于云计算，能够达到实时搜索，稳定，可靠，快速，安装使用方便

具体的使用场景为:
- 比如在线产品商店, 用于存储产品名录, 可以根据用户搜索结果推荐产品名录
- 采用LogStash 收集日志, 聚合日志, 然后推送日志数据到ES中, 提供搜索和聚合功能
- 商品价格预警, 比如比商家客户的所有商品价格写入ES中, 再提供API给普通用户, 用于当某商品价格低于一定价位, 再推送给用户
- 大量数据分析, 并迅速可视化, 可采用[Kibana](https://www.elastic.co/de/products/kibana)建立自定义表格, 采用ES聚合功能来执行数据查询


基础词汇:
- Near RealTime(NRT)   准实时
- Cluster   集群   一个或者多个节点[服务器]的集合, 一个集群名称必须是唯一的. 默认名称Elasticsearch, 如果节点设置为按照名称加入集群, 则该节点只能是集群的一部分
- Node  节点[单机服务器]     可以通过修改集群名称加入特定的集群, 默认加入elasticsearch集群, 单集群有N个节点
- Index  索引[相似特性的文档集合]   名称必须为小写, 单集群可以定义N个索引
- Type  类型   在索引中，可以定义一个或多个类型(比如可以把所有数据存储在一个索引中...)
- Document 文档   可以被索引的基本信息单位, 用JSON表示
- Shards & Replicas   碎片和副本
- 碎片的优势: 水平扩展, 分发和并行化操作     副本的优势: 提高可用性, 可以应对shard/node失效. 分片和副本不应该和主分片在同一个节点上, 提上搜索能力(主分片和分片副本不应在同一个node上)
    
1. 集群的总体了解  ES提供了丰富的REST API和Cluster交互, 例如:
      
- 检查集群健康状态
``` curl -XGET 'localhost:9200/_cat/health?v&pretty'
    epoch      timestamp cluster       status node.total node.data shards pri relo init unassign pending_tasks max_task_wait_time active_shards_percent
    1497257485 16:51:25  elasticsearch yellow          1         1      5   5    0    0        5             0                  -                 50.0%
```

- 集群的所有节点
```curl -XGET 'localhost:9200/_cat/nodes?v&pretty'
   ip        heap.percent ram.percent cpu load_1m load_5m load_15m node.role master name
   127.0.0.1           17          94   9    0.83    0.67     0.60 mdi       *      t--l8qc
```

- 罗列集群的所有指标
```curl -XGET 'localhost:9200/_cat/indices?v&pretty'
   health status index   uuid                   pri rep docs.count docs.deleted store.size pri.store.size
   yellow open   twitter 7I9lWp72RXmTPNcczV6UIg   5   1          1            0      5.3kb          5.3kb
```

- 创建索引
```curl -XPUT 'localhost:9200/customer?pretty&pretty'
   {
     "acknowledged" : true,
     "shards_acknowledged" : true
   }
```

- 根据索引执行CRUD操作
- 执行高级查询操作(分页, 排序, 过滤, Scripting 聚合==)

``` ES的_cat API    _cat格式化json返回的结果, ?v代表返回标签   所有的_cat命令接收help查询字符串, /_cat现实所有可用命令
    
    curl -XGET 'localhost:9200/_cat/master?v&pretty'   ?v现实标签  pretty可视化(方便look, 格式化)输出
    curl -XGET 'localhost:9200/_cat/master?help&pretty'   help  现实输出说明
    curl -XGET 'localhost:9200/_cat/nodes?h=ip,port,heapPercent,name&pretty'   指定输出某些字段
 ```
    
    
集群监控状态(status状态为green\[功能齐全], yellow\[功能齐全, 副本尚未分配], red\[功能有问题]):

    ➜  ~ curl -XGET 'localhost:9200/_cat/health?v&pretty'
    epoch      timestamp cluster       status node.total node.data shards pri relo init unassign pending_tasks max_task_wait_time active_shards_percent
    1496887453 10:04:13  elasticsearch yellow          1         1      5   5    0    0        5             0                  -                 50.0%
    

查看集群下的节点

    ➜  ~ curl -XGET 'localhost:9200/_cat/nodes?v&pretty'
    ip        heap.percent ram.percent cpu load_1m load_5m load_15m node.role master name
    127.0.0.1            8          96  10    0.49    0.56     0.56 mdi       *      t--l8qc

查看集群所有指标(默认没有任何指标)
    
    ➜  ~ curl -XGET 'localhost:9200/_cat/indices?v&pretty'
    health status index    uuid                   pri rep docs.count docs.deleted store.size pri.store.size

创建索引(但节点时状态为yellow)

    ➜  ~ curl -XPUT 'localhost:9200/customer?pretty&pretty'
    {
      "acknowledged" : true,
      "shards_acknowledged" : true
    }
    ➜  ~ curl -XGET 'localhost:9200/_cat/indices?v&pretty'
    health status index    uuid                   pri rep docs.count docs.deleted store.size pri.store.size
    yellow open   customer Jtd6mLz9R0y_lrVfxoA9zA   5   1          0            0       260b           260b

插入一个索引文档到customer中, 类型为external, ID为1

    ➜  ~ curl -XPUT 'localhost:9200/customer/external/1?pretty&pretty' -H 'Content-Type: application/json' -d' { "name": "John Doe" } '
    
    {
      "_index" : "customer",
      "_type" : "external",
      "_id" : "1",
      "_version" : 1,
      "result" : "created",
      "_shards" : {
        "total" : 2,
        "successful" : 1,
        "failed" : 0
      },
      "created" : true
    }
    
根据索引名, 类型, 和ID 查询索引文档. 整个JSON文档在_source中

    ➜  ~ curl -XGET 'localhost:9200/customer/external/1?pretty&pretty'
    {
      "_index" : "customer",
      "_type" : "external",
      "_id" : "1",
      "_version" : 1,
      "found" : true,
      "_source" : {
        "name" : "John Doe"
      }
    }

删除指定索引

    ➜  ~ curl -XDELETE 'localhost:9200/customer?pretty&pretty'
    {
      "acknowledged" : true
    }
    ➜  ~ curl -XGET 'localhost:9200/_cat/indices?v&pretty'
    health status index uuid pri rep docs.count docs.deleted store.size pri.store.size

***

搜索服务:(搜索API的范围很广: )

1. 在一个索引内, 所有类型

```
    curl -XGET 'localhost:9200/twitter/_search?q=user:kimchy&pretty'
```

2. 一个索引内, N个特定类型中查询

```
    curl -XGET 'localhost:9200/twitter/tweet,user/_search?q=user:kimchy&pretty'
```

3. 多个指标内, 某个类型中查询

```
    curl -XGET 'localhost:9200/kimchy,elasticsearch/tweet/_search?q=tag:wow&pretty'
```

4. 所有指标内, 特定类型中

```
    curl -XGET 'localhost:9200/_all/tweet/_search?q=tag:wow&pretty'
```
5. 所有指标内, 所有类型中
```
    curl -XGET 'localhost:9200/_search?q=tag:wow&pretty'
```

查询句子 Query DSL
1. 单查询  Leaf query clauses   比如在特定字段查询特定值 match, term, range
2. 复合查询  Compound query clauses  多个单查询或者复合查询组合

查询包含Query和Filter
Query  如何查询, 会影响_score值  Filter查询结果是否匹配, 不会影响_score值

1. Match All Query
所有_score值都是1.0   可以根据boost设置_score分值
``` 
    curl -XGET 'localhost:9200/_search?pretty' -H 'Content-Type: application/json' -d'
    {
        "query": {
            "match_all": {}
        }
    }
    '
    
    curl -XGET 'localhost:9200/_search?pretty' -H 'Content-Type: application/json' -d'
    {
        "query": {
            "match_all": { "boost" : 100 }
        }
    }
    '
```

Full text queries== running full text queries on full text fields 
match   标准全文查询, 包括模糊匹配, 短语, 邻近查询
match_phrase  精确查询或短语匹配
match_phrase_prefix
multi_match   
query_string   可以用AND|OR|NOT条件组合
