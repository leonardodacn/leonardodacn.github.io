# elasticsearch


## 基本概念

### Node 与 Cluster

Elastic 本质上是一个分布式数据库，允许多台服务器协同工作，每台服务器可以运行多个 Elastic 实例。

单个 Elastic 实例称为一个节点（node）。一组节点构成一个集群（cluster）。

### Index

Elastic 会索引所有字段，经过处理后写入一个反向索引（Inverted Index）。查找数据的时候，直接查找该索引。

所以，Elastic 数据管理的顶层单位就叫做 Index（索引）。它是单个数据库的同义词。每个 Index （即数据库）的名字必须是小写。

### Document

Index 里面单条的记录称为 Document（文档）。许多条 Document 构成了一个 Index。Document 使用 JSON 格式表示。同一个 Index 里面的 Document，不要求有相同的结构（scheme），但是最好保持相同，这样有利于提高搜索效率。

### Type

Document 可以分组，比如weather这个 Index 里面，可以按城市分组（北京和上海），也可以按气候分组（晴天和雨天）。这种分组就叫做 Type，它是虚拟的逻辑分组，用来过滤 Document。

不同的 Type 应该有相似的结构（schema），举例来说，id字段不能在这个组是字符串，在另一个组是数值。这是与关系型数据库的表的一个区别。性质完全不同的数据（比如products和logs）应该存成两个 Index，而不是一个 Index 里面的两个 Type（虽然可以做到）。

在6.0之前的版本，一个ElasticSearch索引中，可以有多个类型；从6.0版本开始，，一个ElasticSearch索引中，只有1个类型。一个类型是索引的一个逻辑上的分类，通常具有一组相同字段的文档组成。ElasticSearch的类型概念相当于关系数据库的数据表。

### shard

当数据量较大时，索引的存储空间需求超出单个节点磁盘容量的限制，或者出现单个节点处理速度较慢。为了解决这些问题，ElasticSearch将索引中的数据进行切分成多个分片（shard），每个分片存储这个索引的一部分数据，分布在不同节点上。当需要查询索引时，ElasticSearch将查询发送到每个相关分片，之后将查询结果合并，这个过程对ElasticSearch应用来说是透明的，用户感知不到分片的存在。 一个索引的分片一旦指定，不再修改。

### 副本

其实，分片全称是主分片，简称为分片。主分片是相对于副本来说的，副本是对主分片的一个或多个复制版本（或称拷贝），这些复制版本（拷贝）可以称为复制分片，可以直接称之为副本。当主分片丢失时，集群可以将一个副本升级为新的主分片。

## 对比

| ElasticSearch    | RDBMS              |
| ---------------- | ------------------ |
| 索引（index）    | 数据库（database） |
| 类型（type）     | 表（table）        |
| 文档（document） | 行（row）          |
| 字段（field）    | 列（column）       |
| 映射（mapping）  | 表结构（schema）   |
| 全文索引         | 索引               |
| 查询DSL          | SQL                |
| GET              | select             |
| PUT/POST         | update             |
| DELETE           | delete             |

## 节点信息

### 查看节点信息

``` shell
curl localhost:9200
```

### 查看节点健康度

``` shell
curl localhost:9200/_cat/health?v&pretty=true
```

### 查看集群状况

``` shell
curl localhost:9200/_cat/nodes?v&pretty=true
```

## index(索引)操作

### 查看当前节点的所有 Index。

``` shell
curl -X GET 'http://localhost:9200/_cat/indices?v'
```

### 可以列出每个 Index 所包含的 Type

``` shell
curl 'localhost:9200/_mapping?pretty=true'
```

### 新建一个名叫weather的 Index。

``` shell
curl -X PUT 'localhost:9200/weather'
```

### 删除这个 Index。

``` shell
curl -X DELETE 'localhost:9200/weather'
```

## 文档操作

### 获取

``` shell
GET /website/blog/123?pretty

{
  "_index" :   "website",
  "_type" :    "blog",
  "_id" :      "123",
  "_version" : 1,
  "found" :    true,
  "_source" :  {
      "title": "My first blog entry",
      "text":  "Just trying this out...",
      "date":  "2014/01/01"
  }
}
```

检索文档的一部分

``` shell
GET /website/blog/123?_source=title,text

{
  "_index" :   "website",
  "_type" :    "blog",
  "_id" :      "123",
  "_version" : 1,
  "exists" :   true,
  "_source" : {
      "title": "My first blog entry" ,
      "text":  "Just trying this out..."
  }
}
```

只想得到_source字段而不要其他的元数据

``` shell
GET /website/blog/123/_source

{
   "title": "My first blog entry",
   "text":  "Just trying this out...",
   "date":  "2014/01/01"
}
```

### 存在

如果你想做的只是检查文档是否存在——你对内容完全不感兴趣——使用HEAD方法来代替GET。HEAD请求不会返回响应体，只有HTTP头：

``` shell
curl -i -XHEAD http://localhost:9200/website/blog/123
```

Elasticsearch将会返回200 OK状态如果你的文档存在：

``` shell
HTTP/1.1 200 OK
Content-Type: text/plain; charset=UTF-8
Content-Length: 0
```

如果不存在返回404 Not Found：

``` shell
HTTP/1.1 404 Not Found
Content-Type: text/plain; charset=UTF-8
Content-Length: 0
```

### 更新整个文档

``` shell
PUT /website/blog/123
{
  "title": "My first blog entry",
  "text":  "I am starting to get the hang of this...",
  "date":  "2014/01/02"
}
```

### 新建文档

``` shell
PUT /website/blog/123
{ ... }
```

### 删除文档

``` shell
DELETE /website/blog/123
```

## 配置

elasticsearch的config文件夹里面有两个配置文件：elasticsearch.yml和log4j2.properties，第一个是es的基本配置文件，第二个是日志配置文件，es也是使用log4j2来记录日志的，所以log4j2.properties里的设置按普通log4j2配置文件来设置就行了。

### cluster.name

Elasticsearch 默认启动的集群名字叫 elasticsearch 。 你最好给你的生产环境的集群改个名字，改名字的目的很简单， 就是防止某人的笔记本电脑加入了集群这种意外。简单修改成 elasticsearch_production 会很省心。

你可以在你的 elasticsearch.yml 文件中修改：

`cluster.name: elasticsearch_production`

### node.name

建议给每个节点设置一个有意义的、清楚的、描述性的名字，同样你可以在 elasticsearch.yml 中配置：

`node.name: elasticsearch_005_data`

### Master节点 （主节点）

``` shell
node.master: true
node.data: false
```

这样配置的节点为master节点。主节点的主要职责是和集群操作相关的内容，如创建或删除索引，跟踪哪些节点是群集的一部分，并决定哪些分片分配给相关的节点。稳定的主节点对集群的健康是非常重要的。

#### discovery.zen.minimum_master_nodes

为了防止数据丢失，配置discovery.zen.minimum_master_nodes设置是至关重要的（默认为1），每个主节点应该知道形成一个集群的最小数量的主资格节点的数量。

假设我们有一个集群。有3个主资格节点，当网络发生故障的时候，有可能其中一个节点不能和其他节点进行通信了。这个时候，当discovery.zen.minimum_master_nodes设置为1的时候，就会分成两个小的独立集群，当网络好的时候，就会出现数据错误或者丢失数据的情况。当discovery.zen.minimum_master_nodes设置为2的时候，一个网络中有两个主资格节点，可以继续工作，另一部分，由于只有一个主资格节点，则不会形成一个独立的集群，这个时候当网络回复的时候，节点又会从新加入集群。

设置这个值的原则是：（master_eligible_nodes / 2）+ 1

#### discovery.zen.ping.unicast.hosts

Elasticsearch 默认被配置为使用单播发现，以防止节点无意中加入集群。只有在同一台机器上运行的节点才会自动组成集群。

虽然组播仍然作为插件提供， 但它应该永远不被使用在生产环境了，否则你得到的结果就是一个节点意外的加入到了你的生产环境，仅仅是因为他们收到了一个错误的组播信号。 对于组播本身并没有错，组播会导致一些愚蠢的问题，并且导致集群变的脆弱（比如，一个网络工程师正在捣鼓网络，而没有告诉你，你会发现所有的节点突然发现不了对方了）。

使用单播，你可以为 Elasticsearch 提供一些它应该去尝试连接的节点列表。 当一个节点联系到单播列表中的成员时，它就会得到整个集群所有节点的状态，然后它会联系 master 节点，并加入集群。

这意味着你的单播列表不需要包含你的集群中的所有节点， 它只是需要足够的节点，当一个新节点联系上其中一个并且说上话就可以了。如果你使用 master 候选节点作为单播列表，你只要列出三个就可以了。 这个配置在 elasticsearch.yml 文件中：

`discovery.zen.ping.unicast.hosts: ["host1", "host2:port"]`

注：端口非9200的节点， ip后需加端口号， 因 es 默认识别端口是9200

### Data节点（数据节点）

``` shell
node.master: false
node.data: true
```

数据节点主要是存储索引数据的节点，主要对文档进行增删改查操作，聚合操作等。数据节点对cpu，内存，io要求较高，在优化的时候需要监控数据节点的状态，当资源不够的时候，需要在集群中添加新的节点。

### Client节点 (客户端节点)

``` shell
node.master: false
node.data: false
```

当主节点和数据节点配置都设置为false的时候，该节点只能处理路由请求，处理搜索，分发索引操作等，从本质上来说该客户节点表现为智能负载平衡器。独立的客户端节点在一个比较大的集群中是非常有用的，他协调主节点和数据节点，客户端节点加入集群可以得到集群的状态，根据集群的状态可以直接路由请求。
警告：添加太多的客户端节点对集群是一种负担，因为主节点必须等待每一个节点集群状态的更新确认！客户节点的作用不应被夸大，数据节点也可以起到类似的作用。

## 安全

search-guard是elastcisearch的一款插件，提供加密，身份验证和授权，基于search guard SSL，另外提供可插入的身份验证/授权模块，search-guard是shield的替代品，可免费提供所有的基本安全功能。

## 参考

[阮一蜂的博客](http://www.ruanyifeng.com/blog/2017/08/elasticsearch.html)
