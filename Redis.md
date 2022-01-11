# Redis

- [Redis](#redis)
  - [数据类型](#数据类型)
  - [Redis过期键的删除策略](#redis过期键的删除策略)
  - [RDB](#rdb)
  - [RDB 的缺点](#rdb-的缺点)
  - [AOF](#aof)

- [主页](README.md)

## 数据类型

String、Hash、List、Set、SortedSet、HyperLogLog、Geo、Pub/Sub

Redis单线程为什么这么快

Redis基于Reactor模式开发了网络事件处理器、文件事件处理器file event handler，它是单线程的所以Redis才叫做单线程模型，他采用IO多路复用机制来同时监听多个Socket

## Redis过期键的删除策略

惰性过期：只有当访问一个key 时，才会判断该key是否过期，过期则删除

定期过期：每个一定时间，会扫描一定数量的数据库的expires字典中一定数量的key，并清除其中已过期的key。

持久化机制RDB、AOF

## RDB

RDB 有两种持久化方式：**手动触发**和**自动触发**

- **手动触发**使用以下两个命令：

  - **「save」**：**会阻塞当前 Redis 服务**器响应其他命令，直到 RDB 快照生成完成为止，对于内存 比较大的实例会造成长时间阻塞，所以线上环境不建议使用

  - **「bgsave」**：Redis 主进程会 **fork 一个子进程**，RDB 快照生成有子进程来负责，完成之后，子进程自动结束，bgsave 只会在 fork 子进程的时候短暂的阻塞，这个过程是非常短的，所以推荐使用该命令来手动触发

- **自动触发** RDB 持久化：

在配置中配置了 save 相关配置信息，如我们上面配置文件中的 save 60 10000 ，也可以把它归类为“save m n”格式的配置，表示 m 秒内数据集存在 n 次修改时，会自动触发 bgsave。

在主从情况下，如果从节点执行全量复制操作，主节点自动执行 bgsave 生成 RDB 文件并发送给从节点

执行 debug reload 命令重新加载 Redis 时，也会自动触发 save 操作

默认情况下执行 shutdown 命令时，如果没有开启 AOF 持久化功能则自动执行 bgsave

## RDB 的缺点

- RDB 持久化方式数据**没办法做到实时持久化/秒级持久化**。我们已经知道了 bgsave 命令每次运行都要执行 fork 操作创建子进程，属于重量级操作，频繁执行成本过高。

- RDB 文件使用特定二进制格式保存，Redis 版本演进过程中有多个格式 的 RDB 版本，存在老版本 Redis 服务无法兼容新版 RDB 格式的问题

## AOF

记录redis的写操作，一个是将操作命令追加到 AOF_BUF 缓存区，另一个是 AOF_buf 缓存区数据同步到 AOF 文件