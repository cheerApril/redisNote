
<br> redis 官网命令 https://redis.io/commands
<br> redis 常用命令 flushall 删除数据库所有的数据 clear  清屏 
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







