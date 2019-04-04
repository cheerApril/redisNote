
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

