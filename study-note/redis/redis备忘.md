## redis通用命令

1. KESY 查看符合模板的所有key 因为redis是单线程的所以不建议在生产环境下使用
    
2. DEL 删除一个指定的key
    
3. EXISTS 判断key是否存在
    
4. EXPIRE 给key设置一个有效期
    
    1. -1 代表永远不过期
        
    2. -2 代表已经过期
        
    3. 建议给每个数据都设置一个有效期
        
5. TTL 查看key的剩余时间
    

## reids string类型命令

1. SET
    
2. GET
    
3. MSET
    
4. MGET
    
5. INCR 让一个整形key自增1
    
6. INCRBY 让一个整形key按照自定步长自增1
    
7. INCRBYFLOAT 让一个浮点类型的数字自增并指定步长
    
8. SETNX 添加一个string类型的键值对 前提是这个key不存在 否则不执行
    
    1. SETNX name 1 和 SET name 1 nx 效果是一样的
        
9. SETEX 添加一个string类型的键值对 并指定有效期
    
    1. SETEX name 10 qjf
        

key的结构 ：

redis的key允许有多个单词形成层级结构 多个单词用：隔开 项目名：业务名：类型：id

## redis hash类型命令

1. HSET
    
    1. HSET diary:manager:1 username warmwind
        
    2. HSET diary:manager:1 username warmwind password qq2693387413 HSET也能实现HMSET的功能所以HMSET已经弃用
        
2. HGET
    
3. HMSET 已经弃用
    
4. HMGET
    
5. HMGETALL
    
6. HKEYS
    
7. HVALS
    
8. HINCRBY 让一个hash类型的key字段自动增长
    
9. HSETNX
    

## redis list类型命令

和java的linkedlist类似 支持正向和反向检索，有序，元素可以重复，插入和删除快，查询速度一般

1. LPUSH 从左侧插入一个或多个元素
    
    1. LPUSH users 1 2 3 3 2 1
        
2. LPOP 移除并返回左侧的第一个元素 没有则返回nil
    
    1. LPOP users 1 返回3 元素还剩 2 1
        
3. RPUSH
    
    1. RPUSH users 4 5 6 元素还剩 2 1 4 5 6
        
4. RPOP
    
    1. RPOP users 1 元素还剩 2 1 4 5
        
5. LRANGE 返回一段角标范围内的所有元素
    
    1. LRANGE users 1 2 返回 2 1
        
6. BLPOP/BRPOP 与LPOP和RPOP类似 只不过在没有元素时等待时间
    
7. 用list模拟一个栈
    
    1. 入口和出口在同一边
        
8. 用list模拟一个队列
    
    1. RPUSH LPOP
        
    2. LPUSH RPOP
        
9. 用list模拟一个阻塞队列
    
    1. 入口和出口在不同边
        
    2. 出队采用BLPOP或RLPOP
        

## redis set类型命令

类似java的hashset 可以看作一个value为空的hashMap 因为是个hash所以与hashset类似 无序 ，元素不可重复，查找快，支持交集并集差集等功能

1. string的常见命令
    
    1. SADD 向set中添加一个或多个
        
        1. SADD users a b c
            
    2. SREM 移除set中的指定元素
        
        1. SREM users a 返回无序的 b c
            
    3. SXCARD key 返回set中元素的个数
        
        1. SCARD users 返回set中的元素个数
            
    4. SISMEMBER 判断一个元素是否存在与set中
        
        1. SISMEMBER users a有返回 1 没有返回 0
            
    5. SMEMBERS 获取set中所有的元素
        
        1. 添加的元素无序
            
    6. SINTER k1 k2 求k1和k2的交集
        
    7. SDIFF k1 k2 求k1和k2的差集
        
    8. SUNION k1 k2 求k1和k2的并集
        

## redis sortedSet类型

1. 是一个可排序的set集合 与java的treeset类似但是底层数据结构差别很大，每一个元素都有一个score属性，基于score属性继续排序，底层是一个跳表加上hash 特点是可排序 元素不可重复 查询速度快 经常用来实现排行榜
    
2. ZADD 添加一个或多个元素 如果已经存在则更新score值
    
    1. ZADD students 100 qjf 99 wcy 90 yzp 80 xzl
        
3. ZREM 删除一个或者多个
    
4. ZSCORE 获取指定元素的score值
    
5. ZRANK 获取某一个的排名 返回的排名是从0开始
    
    1. ZREBVRAN 降序
        
6. ZCARD 获取set中的元素个数
    
7. ZCOUNT 统计一定范围i内的所有元素个数
    
8. ZINCRBY 让set中的指定元素自增 并指定步长
    
9. ZRANGE 按照score排序后 获取指定排名范围内的元素
    
10. ZRANGEBYSCORE 按照score排序后 获取指定score范围内的元素
    
11. ZDIFF ZINTER ZUNION 求交集 ，并集， 差集
    
12. 所有的排名都是升序的，如果要降序则在命令的z后面加上REV
    

## Jedis 使用步骤

1. 引入依赖
    
2. 创建redis对象建立连接
    
3. 使用jedis
    
4. 释放jedis