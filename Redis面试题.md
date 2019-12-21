### 数据结构
- string : 二进制安全，可存任何格式，字段或json对象或图片
- hash : 类似于数据库表， 适合存储对象
- list : 双向链表，两端插入高效，中间插入效率越来越低，按插入顺序排序，普遍用来实现消息队列，需要注意
- set：集合类型，无序不重复，方便实现交并补运算，比如共同好友
- zset：给集合中每个元素加入一个分数用于排序，可以实现好友亲密度
- bitmap：适合存储bool值
- HyperLogLog：提供不精确的去重计数方案，比如统计 uv
- Geo：用于存储地理位置，可以解决附近的人等需求，底层其实是zset
- Pub/Sub
- Redis Module： 
- - BloomFilter： 用于判断某个值是否存在，节省90%空间，推荐系统推荐内容去重，爬虫系统url去重，垃圾邮件
- - RedisSearch
- - Redis-ML
- - redis-cell， 限流模块，漏斗算法
- Stream：

### redis 高可用
#### redis 持久化　rdb快照 和 aof
##### rdb
父进程fork子进程，父进程继续接收命令，子进程完成数据由内存到磁盘的写入，写入完成后，旧的快照被删除
- 根据配置自动
- save或bgsave
- flushall
- 复制

##### aof
相当与操作日志，每一秒将操作的命令追加到硬盘文件中，对性能有消耗


#### redis 复制
##### 建立连接
- slave 运行 slaveof 命令，获取master节点信息
- slave 每秒检查master是否可以连接，可以的话，就建立连接并建立一个处理复制工作的文件事件处理器
- slave 节点发送 ping 给 master，检测
- 如果master设置了requirepass，slave 必须发送认证

##### 数据同步
slave 向 master 发送 psync runid offset 命令， master 根据 runid 决定是全量复制还是增量复制，根据offset确定位置。
runid 不同，则全量复制

##### 命令复制
master 将写操作命令发送给 slave，同时写入 backlog 缓存，slave 接收到命令并执行，复制完成

##### 全量复制
- 主机重启初次复制，进行全量复制
- master 接收到全量复制请求后，执行 bgsave，生成rdb文件，并开启一个缓冲记录新的操作
- master 将 rdb 文件发送给 slave，slave 清空旧数据并载入新数据
- master 将缓冲中记录的新操作发送给slave

##### 部分复制（增量复制）
网络中断等原因引起，当slave重连master时，进行部分复制，master和slave会共同维护一个 offset，从offset处开始复制

#### 哨兵（单master多slave）
哨兵适合数据量小的场景。  
集群监控，消息通知，故障转移
#### 集群（cluster 多master多slave）
自动将数据进行分片，每个master 放一部分数据，实现海量存储，不需要手动配置复制和哨兵。  

cluster 模式下，每个 redis 开放两个端口，一个 6379， 一个 16379，前者提供服务，后者节点间通信，完成故障发现和转移。  

##### 数据分布算法

###### 原始 hash 算法
根据节点数量对 key 取模， 然后存到响应符的节点，一点有一个节点故障，大部分数据就要重新取模写入缓存，不能接受

###### 一致性hash
普通的一致性hash，计算key的hash值，找到圆环上距离最近的节点，节点宕机后，只有该节点受到影响。  

针对一致性hash的缺点，可以引入虚拟节点，

###### hash solt 算法

redis 有固定的 16384 个 hash solt，当接收到写请求后，会对 key计算CRC16值，然后再对16384取模，这样就可以获取key对应的hash slot

redis cluster 中每个 master 都会持有部分slot，当增加一个master时，就将其他master的hash slot部分移动过去，减少一个master，就将它的hash slot移动到其他master上去。

这样就可以高效的解决节点变化时造成的数据转移开销。

### 分布式锁
```
set lock_name true ex 10 nx
...
del lock_name
```
```
EX seconds – 设置过期时间，单位秒
PX milliseconds – 设置过期时间，单位毫秒
NX – key 不存在才设置 key 的值
XX – key 已经存在才可以设置 key 的值
```
#### 超时问题
不要执行过长的任务。给 value 设置随机值，使用lua语言在执行 del 前先判断value是否一致。

#### 锁冲突
抛出异常，由客户端决定是否重连  
把冲突的请求的消息加入另一个队列，另做处理

### zookeeper 分布式锁

#### 原理

- 设置一个 znode， 假设为 /lock
- 客户端连接 zookeeper，并在/lock下创建临时有序(ephemeral_sequential))的子节点, 例如：第一个客户端对应的子节点为/lock/lock-0000000000，第二个为/lock/lock-0000000001，依次类推。
- 客户端调用getChild() 获取 /lock下的子节点列表，判断自己创建的子节点是否为所有子节点中序号最小的，如果是则认为获得锁，否则监听刚好在自己之前一位的子节点删除消息，获得子节点变更通知后重复此步骤直至获得锁。
- 执行业务代码。
- 完成业务流程后，删除对应的子节点释放锁。


### 假如Redis里面有1亿个key，其中有10w个key是以某个固定的已知的前缀开头的，如果将它们全部找出来？

使用keys指令可以扫出指定模式的key列表。redis的单线程的。keys指令会导致线程阻塞一段时间，线上服务会停顿，直到指令执行完毕，服务才能恢复。这个时候可以使用scan指令，scan指令可以无阻塞的提取出指定模式的key列表，但是会有一定的重复概率，在客户端做一次去重就可以了，但是整体所花费的时间会比直接用keys指令长。

### 使用过Redis做异步队列么，你是怎么用的？
一般使用list结构作为队列，rpush生产消息，lpop消费消息。当lpop没有消息的时候，要适当sleep一会再重试。

如果对方追问可不可以不用sleep呢？list还有个指令叫blpop，在没有消息的时候，它会阻塞住直到消息到来。

如果对方追问能不能生产一次消费多次呢？使用pub/sub主题订阅者模式，可以实现1:N的消息队列。

如果对方追问pub/sub有什么缺点？在消费者下线的情况下，生产的消息会丢失，得使用专业的消息队列如rabbitmq等。

如果对方追问redis如何实现延时队列？我估计现在你很想把面试官一棒打死如果你手上有一根棒球棍的话，怎么问的这么详细。但是你很克制，然后神态自若的回答道：使用sortedset，拿时间戳作为score，消息内容作为key调用zadd来生产消息，消费者用zrangebyscore指令获取N秒之前的数据轮询进行处理。

到这里，面试官暗地里已经对你竖起了大拇指。但是他不知道的是此刻你却竖起了中指，在椅子背后。

### 如果有大量的key需要设置同一时间过期，一般需要注意什么？

如果大量的key过期时间设置的过于集中，到过期的那个时间点，redis可能会出现短暂的卡顿现象。一般需要在时间上加一个随机值，使得过期时间分散一些。

### Pipeline有什么好处，为什么要用pipeline？

可以将多次IO往返的时间缩减为一次，前提是pipeline执行的指令之间没有因果相关性。使用redis-benchmark进行压测的时候可以发现影响redis的QPS峰值的一个重要因素是pipeline批次指令的数目。

### 是否使用过Redis集群，集群的原理是什么？

Redis Sentinal着眼于高可用，在master宕机时会自动将slave提升为master，继续提供服务。

Redis Cluster着眼于扩展性，在单个redis内存不足时，使用Cluster进行分片存储。


### 限流  
高并发应用阻止大量请求对系统施压。  
控制用户行为。（发帖，点赞，回复） 

简单 用 zset 实现， value 和 score 都用当前时间。

#### 漏斗限流






