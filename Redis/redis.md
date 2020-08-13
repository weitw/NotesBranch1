```sql
# 启动redis客户端
redis-cli

# 检测redis服务是否启动
PING

# 登录远程服务器
redis-cli -h host -p port -a password
```

### 1. 支持的数据类型

#### 1.1 字符串

String是一组字节。在Redis数据库中，字符串是二进制安全的。这意味着它们具有已知长度，并且不受任何特殊终止字符的影响。可以在一个字符串中存储最多512兆字节的内容。

```sql
# 存储{"name": "hello"}
SET name "hello"
# 获取name的值
GET name
```

#### 1.2 哈希

哈希是键值对的集合。在Redis中，哈希是字符串字段和字符串值之间的映射。因此，它们适合表示对象。

```sql
# 存储一个用户对象，其中包含用户的基本信息
HMSET user username ajeet passwrod javatpoint alexa 2000
# 获取哈希数据
HGETALL user
# 结果
"username"  
"ajeet"  
"password"  
"javatpoint"  
"alexa"  
"2000" 
```

这里，HMSET和HGETALL是Redis的命令，而user是键。每个哈希可以存储多达40多亿

#### 1.3 列表

Redis列表定义为字符串列表，按插入顺序排序。可以将元素添加到Redis列表的头部或尾部。

```sql
# 存储数据
lpush  javatpoint java
lpush  javatpoint sql
lpush  javatpoint cmongodb
lpush  javatpoint cassandra
# 获取数据，lrange key start len。表示是获取key的值（从第0个开始，获取10个）
lrange javatpoint 0 10
"cassandra"  
"mongodb"  
"sql"  
"java" 
```

#### 1.4 集合

集合（set）是Redis数据库中的无序字符串集合。在Redis中，添加，删除和查找的时间复杂度是O(1)。

```sql
# 存储数据
sadd data redis  # 单个存储
sadd data sql mysql mongodb  # 多个存储
sadd data hello hello hello # 存储多个一样的值，最后只会保留一个

# 获取数据
smembers data
```

集合的特点是无序且不可重复的。集合中的最大成员数为232 – 1个元素（每个列表超过40亿个元素）。

#### 1.5 有序集合

Redis zset 和 set 一样也是string类型元素的集合,且不允许重复的成员。不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。zset的成员是唯一的,但分数(score)却可以重复。

`zadd key score member`

#### 1.6 总结

| 类型                 | 简介                                                   | 特性                                                         | 场景                                                         |
| :------------------- | :----------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| String(字符串)       | 二进制安全                                             | 可以包含任何数据,比如jpg图片或者序列化的对象,一个键最大能存储512M | ---                                                          |
| Hash(字典)           | 键值对集合,即编程语言中的Map类型                       | 适合存储对象,并且可以像数据库中update一个属性一样只修改某一项属性值(Memcached中需要取出整个字符串反序列化成对象修改完再序列化存回去) | 存储、读取、修改用户属性                                     |
| List(列表)           | 链表(双向链表)                                         | 增删快,提供了操作某一段元素的API                             | 1,最新消息排行等功能(比如朋友圈的时间线) 2,消息队列          |
| Set(集合)            | 哈希表实现,元素不重复                                  | 1、添加、删除,查找的复杂度都是O(1) 2、为集合提供了求交集、并集、差集等操作 | 1、共同好友 2、利用唯一性,统计访问网站的所有独立ip 3、好友推荐时,根据tag求交集,大于某个阈值就可以推荐 |
| Sorted Set(有序集合) | 将Set中的元素增加一个权重参数score,元素按score有序排列 | 数据插入集合时,已经进行天然排序                              | 1、排行榜 2、带权重的消息队列                                |





















































