
一. redis 数据类型有哪些?

	a.字符串;b.列表;c.集合;d.有序集合;e.哈希;
	
二. 为什么Redis需要把所有数据存储在内存中?
	
	Redis为了达到最快的读写速度将数据都读到内存中，并通过异步的方式将数据写入磁盘。每秒可以处理超过10万次的读写操作,是已知性能最快的Key-Value DB。
	所以redis具有快速和数据持久化的特征。如果不将数据放在内存中，磁盘I/O速度为严重影响redis的性能。
	在内存越来越便宜的今天，redis将会越来越受欢迎。 如果设置了最大使用的内存，则数据已有记录数达到内存限值后不能继续插入新值。

三. redis与memcache的区别?

	1.在存储位置上，memcache存储在内存中，redis存储在内存中，也可以存储在磁盘中，达到持久化的功能，当断电时，memecache数据会全部丢失，
	 而redis可以利用快照或AOF将数据写入磁盘，当来电时候，从磁盘中读取数据写入内存中，当物理内存使用完可以将数据存储在磁盘；
	2.存储数据类型上，memcache多数存储字符串，redis可以存储多种数据类型，如字符串、列表、hash、集合、有序集合；
	3.存储数据大小上，memcache存储单个value值最大100M，而redis最大值为1G；
	4.redis只支持单核，memcache可支持多核；
	5.memcache支持分布式，redis支持主从；
	
四. 为什么单线程的 Redis 比多线程的 Memcached 效率要高得多？
	
	1. 纯内存操作
	2. 核心是基于非阻塞的 IO 多路复用机制
	3. 单线程反而避免了多线程的频繁上下文切换问题

五. 使用过Redis分布式锁么，它是怎么实现的？
	
	先拿setnx来争抢锁，抢到之后，再用expire给锁加一个过期时间防止锁忘记了释放。
	如果在setnx之后执行expire之前进程意外crash或者要重启维护了，那会怎么样？
	set指令有非常复杂的参数，这个应该是可以同时把setnx和expire合成一条指令来用的！
	
六. redis 常用命令？
        string: get,set,del,incr,append（常规key-value缓存应用）
	list  : rpush,lpush,rpop,lpop,lrange,lindex,ltrim（消息队列系统）
	set   ：sadd，srem，scard，spop；（交集，并集，差集：(Set)）
	hash  ：hmget，hmset,hmdel,hmlen,hexists（存储部分变更数据，如用户信息等。）
	zset  :zadd key score member,zcard,zcount key min max,zrank key member,zrange key start stop,zscore key member
	       (有序集合比set增加了权重值可以用于排行榜之类的)
