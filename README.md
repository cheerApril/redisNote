
<br> redis 官网命令 https://redis.io/commands
<br> redis 常用命令 flushall 删除数据库所有的数据 clear  清屏 
<br> redis 相关的操作 设置 , 范围查找, INCR更新, 删除
<br>--------------------------------------------------------

<br> 这个版本的是3.0之前的版本,暂时支持的数类型是string, list, set(不重覆的数组), hash(key-value), zset(有序set)
<br> string的常用命令:
<br> ------ GET 获取存储在给定键中的值
<br> ------ SET 设置存储在给定键中的值
<br> ------ DEL 删除存储在给定键重的值 (适用所有类型)
<br> ------ INCR key-name ---- 将键存储的值加上1
<br> ------ DECR key-name ---- 将键存储的值减去1
<br> ------ INCRBY key-name amount 将键存储的值加上整数amount 
<br> ------ DECRBY key-name amount 将键存储的值减去整数amount 
<br> ------ INCRBYFLOAT key-name amount 将键存储的值加上浮点 amount (这个命令在Redis 2.6或以上的版本可用)

<br> ------ INCR ---INCRBYFLOAT 这些参数的操作只能针对于key.value可以解析成十进制或者浮点数,如果这些命令操作的是不存在key值的会,会创建对应的key但是value为0的东西

<br> ------ APPEND key-name value 将值value追加给定检key-name 当前存储的值的末尾
<br> ------ GETRANGE key-name start end 截取偏移量 start到 偏移量end 的值，如果start < end 获取的是""
<br> ------ SETRANGE key-name offset value (不存在的话会创建一个新的key 填充value) 
<br> 1.如果 0 <= offset < key.value.length offset后面的字段替换成value
<br> 2.如果 offset >= key.value.length : offset 到 value.length 的之前的位置会被填充成null,从offset之后增加数据value
<br> 3.offset不能为负数

<br> list(链表 linked-list): 一个列表结果可以有序地存储多个字符串(有序)
<br> list的常用命令:
<br> ------ RPUSH(LPUSH) key value1 value2...将给定值推入列表的右(左)端
<br> ------ LPOP(RPOP) key 从列表的左(右)端弹出一个值,并返回被弹出的值
<br> ------ LRANGE key start stop  获取列表在给定范围上的所有值包括start跟end的值 如果start < end 返回empty list or set;
<br> ------ LINDEX key index 获取列表给定位置上的单个元素 1.如果index是负数就从后面开始算起 2.不存在的数值返回nil
<br> ------ LTRIM key-name start end 
<br> ------ BLPOP key-name [key-name..] timeout 从第一个非空列表中弹出位于最左端的元素或者在timeout秒之内阻塞并等待可弹出的元素出现(如果不存在元素会等待 timeout 秒 返回nil跟等待的时间)
<br> ------ BRPOP key-name [key-name..] timeout 从第一个非空列表中弹出位于最右端的元素或者在timeout秒之内阻塞并等待可弹出的元素出现(如果不存在元素会等待 timeout 秒 返回nil跟等待的时间)
<br> ------ RPOPLPUSH source destination 从source-key 列表中弹出位于最右端的元素,然后将这个元素推入dest-key列表的最最左端,并返回这个推入的元素(如果SOURCE没有就不会推入任何数据)
<br> ------ BRPOPLPUSH source destination timeout 从source-key 列表中弹出位于最右端的元素,然后将这个元素推入dest-key列表的最最左端,并返回这个推入的元素，如果source为空,那么等待timeout秒之后返回nil(如果SOURCE没有就不会推入任何数据)

<br> zet(无序集合) 以无序的方式来存储多个各不相同的元素
<br> ------ SADD key-name item [item] 将一个或多个元素添加到集合里面,并返回被添加元素当中原本并不存在与集合里面的元素数量
<br> ------ SREM key-name item [item] 从集合里面一处一个或多个元素,并返回被移除元素的数量
<br> ------ SISMEMBER key-name item 检查元素item是否存在与集合key-name里 (判断的 set[key] === value 如果是true的话就是存在返回1,否则返回0)
<br> ------ SADD key-name item [item] 将一个或多个元素添加到集合里面,并返回被添加元素当中原本并不存在与集合里面的元素数量
<br> ------ SCARD key-name 返回集合包含的元素的数量
<br> ------ SMEMBERS key-name 返回集合包含的所有的元素
<br> ------ SRANDMEMBER key-name [name] 从集合里面随机地返回一个或多个元素.当count为正数时,命令返回的随机元素不会重复;当count为负数时,命令返回的随机元素可能会出现重覆. (集合不存在的时候返回empty list or set || 如果length > set.length 返回全部);
<br> ------ SPOP key-name[count] 随机地移除集合中的一个或count个元素,并返回被移除的元素(如果count < 0会报错)
<br> ------ SMOVE source-key dest-key item 如果集合source-key包含元素item,那么从集合source-key里面移除元素item，并将元素item添加到集合dest-key中;如果item被成功移除,那么命令返回1,否则返回0. (返回的判断标志是元素item是否被移除了)
<br> 1.如果dest-key 不存在的话,会创建的value item的新的集合set 
<br> 2.如果source-key 不存在返回0

<br> ------ SDIFF key-name [key-name] 返回那些存在与第一个集合,但不存在与其他集合中的元素(数学上的差集运算)[如果不存在的话就跟空集做相关操作]
<br> ------ SDIFFSTORE dest-key key-name [key-name] 将那些存在与第一个集合,但不存在与其他集合中的元素(数学上的差集运算)存储到dest-key键里面(如果dest-key里面已经存在数据的话,无论如何都会覆盖,重新赋值)
<br> ------ SINTER key-name [key-name] 返回那些同时存在与所有集合中的元素(交集运算)
<br> ------ SINTERSTORE dest-key key-name [key-name] j将那些同时存在与所有集合中的元素(交集运算)存储在dest-key(跟上面一样对于已存在的key会重新赋值)
<br> ------ SUNION key-name [key-name] 返回那些至少存在与一个集合中的元素(数学上的并集运算===全返回)
<br> ------ SUNIONSTORE key-name [key-name] 将那些至少存在与一个集合中的元素(数学上的并集运算===全返回)存储在dest-key键里面

<br> hash(散列表) 如果一个hash表的数据,使用set设置的同样的key的话,hash相同key的值会改变成string类型,但是相反操作不行
<br> ------ HSET key field value 在散列里面关联起给定的键值对
<br> ------ HGET key field 获取指定散列键的值
<br> ------ HGETALL key 获取散列包含的所有键值对
<br> ------ HDEL key field [..field] 如果给定键存在与散列里面,那么移除这个键
<br> ------ HMGET key-name key [key...] 从散列里面获取一个或多个值
<br> ------ HMSET key-name key value [key vakue...] 为散列里面的一个或多个键设置值
<br> ------ HLEN key-name 返回散列包含的键值对数量
<br> ------ HEXISTS key-name field  检查给定键是否存在与散列中
<br> ------ HKEYS key-name  返回散列包含的所有键
<br> ------ HVALS key-name  返回散列包含的所有值
<br> ------ HINCRBY key-name field increment 将键key存储的值加上整数increment(如果key活着field 不存在创建一个value为0 的新对象做创建操作)(如果原来的value是浮点数不能进行操作,但是下面的可以进行整数操作)
<br> ------ HINCRBYFLOAT key-name field increment 将键key存储的值加上浮点x数increment(如果key活着field 不存在创建一个value为0 的新对象做创建操作)

<br> 有序集合 zset
<br> ------ ZADD key-name [options] score member [score member....] 将相关的数值添加到有序集合里面
ZADD options (Redis 3.0.2 or greater)
ZADD supports a list of options, specified after the name of the key and before the first score argument. Options are:

XX: Only update elements that already exist. Never add elements.
NX: Don't update already existing elements. Always add new elements.
CH: Modify the return value from the number of new elements added, to the total number of elements changed (CH is an abbreviation of changed). Changed elements are new elements added and elements already existing for which the score was updated. So elements specified in the command line having the same score as they had in the past are not counted. Note: normally the return value of ZADD only counts the number of new elements added.
INCR: When this option is specified ZADD acts like ZINCRBY. Only one score-element pair can be specified in this mode.
<br> ------ ZREM key-name member [..member] 从有序集合里面移除相关的member，并返回移除成员的数量 
<br> ------ ZCARD key-name 返回有序集合包含的成员数量 
<br> ------ ZINCRBY key-name increment member 将member成员的分值加上increment(同样的不存在的话会创建value为0的新的member,然后进行操作)
<br> ------ ZCOUNT key-name min max 返回score介于min和max之间的member数量(min和max都可以为0,如果max < min 永远返回的是0)
<br> ------ ZRANK key-name member 返回成员member在有序集合中的排名 (没有返回nil) (从0开始排序哦)
<br> ------ ZSCORE key-name member 返回成员member在有序集合中的分值 (没有返回nil)
<br> ------ ZRANGE key-name start stop [withscores] 返回有序集合中排名介于start和stop之间的成员,如果给定了可选的withscores选项,那么命令会将成员的分值也一并返回(如果start< stop 返回empty set or list )
<br> ------ ZREVRANK key-name  member 返回有序集合里成员member的排名,成员按照分值从大到小排列(rev--revrse) 跟之前的排序反向排序
<br> ------ ZREVRANGE key-name start stop [withscores] 返回有序集合给定排名范围内成员,成员按照分值从大到少排列.
<br> ------ ZRANGEBYSCORE key-name min max [withscores] [limit offset count] 获取有序集合中分值介于min和max之间的所有成员,并按照分值从大到小的顺序来返回他们
<br> ------ ZREMRANGEBYRANK key-name start stop 移除有序集合中排名介于start和stop之间的所有成员
<br> ------ ZREMRANGEBYSCORE key-name min max 移除有序集合中分值排名介于start和stop之间的所有成员
<br> ------ ZINTERSTORE destination numkeys key [key ...] [WEIGHTS weights [weights ...]] [AGGREGATE SUM|MIN|MAX] 对给定的有序集合执行类似于集合的交集运算
<br> --eg: zinterstore gem 2(这个数只能大于等于后面key的数量不能少于) cheer april weights 1 2 (weights 后面的权重对应于cheer跟April这两个有序集合而且你有多少个key 就要设置多少个) aggregate SUM;(可以跟SET数据类型做交集操作,set里面的value默认为1)
<br> ------ ZUNIONSTORE destination numkeys key [key ...] [WEIGHTS weights [weights ...]] [AGGREGATE SUM|MIN|MAX] 对给定的有序集合执行类似于集合的并集运算

<br> 发布与订阅
<br> ------ subscribe channel [channel...] 订阅给定的一个或多个频道
<br> ------ unsubscribe [channel channel...] 退订给定的一个或多个频道,如果执行时诶呦给定任何频道,那么退订所有频道
<br> ------ publish channel message 向给定频道发送消息
<br> ------ psubscribe pattern [pattern]订阅给定模式相匹配的所有频道 
<br>支持的模式(patterns)有:
<br>h?llo subscribes to hello, hallo and hxllo
<br>h*llo subscribes to hllo and heeeello
<br>h[ae]llo subscribes to hello and hallo, but not hillo
<br>如果想输入普通的字符，可以在前面添加\
<br> ------ punsubscribe [pattern [pattern..] --退订给定的模式,如果执行时没有给定任何模式,那么退订所有模式

<br>sort 命令
<br> ------ sort key [by pattern] [LIMIT OFFSET COUNT] [GET pattern] [ASC|DESC] [ALPHA] STORE destination
<br> ------返回或存储key的list、 set 或sorted set 中的元素。默认是按照数值类型排序的，并且按照两个元素的双精度浮点数类型值进行比较
<br> ------ msyql order by可以当做一样理解,但是肯定有一些不同的
<br> ------ LIMIT是命令 offset 跟 count 是从offset开始返回count个元素的意思 
<br> ------ ASC 升序 DESC 降序 
<br> ------ ALPHA 排序的数据类型是字符串值并且需要按照字典顺序排序
<br> ------ STORE destination 排序之后的数据作为列表保存在destination_key 里面(为了正确实现这种模式，很重要的一点是防止多个客户端同时重建缓存。 此时需要使用一些锁（具体的使用 SETNX)
<br> ------- 在GET BY 里面使用hash的数据类型 SORT mylist BY weight_*->fieldname GET object_*->fieldname 字符串 -> 用于区分key名称和哈希属性的名称。key被替换为上面所记录的，结果key中存储的hash用于获取特定hash的属性

<br>用来处理过期时间的Redis命令
<br> ----- PERSIST key-name -- 移除键的过期时间 
<br> ----- TTL key-name 查看给定键距离过期还有多少秒 (如果key不存在或者已过期，返回 -2 如果key存在并且没有设置过期时间（永久有效），返回 -1)
<br> ----- EXPIRE key-name seconds 让给定键在指定的秒数之后过期 (1 如果成功设置过期时间	0 如果key不存在或者不能设置过期时间。)
<br> ----- EXPRIEAT key-name timestamp 将给定键的过期时间设置给定的UNINX时间戳
<br> ----- PTTL key-name 查看给定键距离过期时间还有多少毫秒
<br> ----- PEXPRIE key-name milliseconds 让给定键在指定的毫秒数之后过期
<br> ----- PEXPIREAT key-name timestamo-milliseconds 将一个毫秒级精度的UNINX时间戳为给定键的过期时间




























