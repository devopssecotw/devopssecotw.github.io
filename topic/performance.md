# OTW1248
## topic
### high performance

#### General best practices
##### Enable telemetry to collect metrics 
##### Monitor the 90/95/99 percentiles, not just average
##### Attack one bottleneck at a time
##### Errors and retries can have a large impact on performance
#####  performance anti-patterns
##### Look for opportunities to parallelize
##### 
#### performance anti-patterns 
##### Busy Database
##### Busy Front End
##### Chatty I/O
##### Extraneous Fetching
##### Improper Instantiation
##### Monolithic Persistence
##### No Caching
##### Noisy Neighbor
##### Retry Storm
##### Synchronous I/O
#### 队列
##### 应用场景
- 异步处理  流程并不需要在本次请求中立即处理
- 流量削峰  使用消息队列进行排队缓冲
- 系统解耦  依赖服务可以订阅开播事件的消息队列进行解耦
- 数据同步  消息队列可以起到数据总线的作用
- 柔性事务  基于消息队列的一种分布式事务实现
##### 应用分类
- 缓冲队列  采用 Kafka 作为日志缓冲队列
- 请求队列  网络框架一般都有请求队列
- 任务队列  线程池的任务队列
- 消息队列  点对点和发布订阅两种模式,常见的有 RabbitMQ、RocketMQ、Kafka
#### 缓存
##### 应用场景
- 一旦生成后基本不会变化的数据
- 读密集型或存在热点的数据
- 计算代价大的数据
- 千人一面的数据
##### 不适合使用缓存的场景
- 写多读少，更新频繁
- 对数据一致性要求严格
##### 缓存的分类
- 进程级缓存 缓存的数据直接在进程地址空间内
- 集中式缓存 缓存的数据集中在一台机器上,redis、memcache
- 分布式缓存 缓存的数据分布在多台机器
- 多级缓存 系统中的不同层级的进行数据缓存
##### 缓存的模式
- Cache-Aside：旁路缓存, 首先从缓存读取数据
- Cache-As-SoR （system-of-record）：缓存即数据源 , 读写操作都是针对 Cache
##### 缓存的回收策略
- 基于时间: TTL（Time To Live）：即存活期; TTI（Time To Idle）：即空闲期
- 基于空间
- 基于容量
- 基于引用
- 缓存的常见回收算: FIFO（First In First Out）：先进选出原则; LRU（Least Recently Used）：最基于局部性原理; LFU：（Least Frequently Used）：最近最少被使用的数据最先被淘汰
##### 缓存的一些好实践
- 动静分离
- 慎用大对象
- 过期设置
- 超时设置
- 缓存隔离
- 失败降级
- 容量控制
- 业务导向
- 监控告警

#### 缓存的崩溃与修复
- 缓存穿透 : 1）设置空置或默认值; 2）布隆过滤器：采用布隆过滤器将，将所有可能存在的数据哈希到一个足够大的 bitmap 中
- 缓存雪崩 : 缓存失效时间集中在某段时间; 2）采用取模机制的某缓存实例宕机
- 缓存热点:  key 太热了,这种情况可以通过生成多份缓存到不同节点
####
####
#### references
- <https://mp.weixin.qq.com/s/hsH7LMBEDGe_df9UbfOvbQ>
- <https://docs.microsoft.com/en-us/azure/architecture/performance/>
- <>
- <>
- <>
- <>
- <>
