---
layout: post
title: "MySQL 性能相关"
author: "Dzreal"
categories: db
tags: [db]
image: mysql-perform.jpg
---
# MySQL 性能相关

### 影响数据库性能的因素
1、**SQL查询速度（mysql不支持多CPU并发运算，每个SQL只能用到一个CPU**\
**QPS**:每秒钟处理的查询量（同时处理SQL的数量）\
**TPS**:每秒钟处理的事务数\
2、 **服务器硬件**\
**并发量**：同一时刻，对数据库服务器请求的数量。\
**连接量**：同一时刻，与数据库服务器的连接数（mysql config里的max_connection决定，默认为100），一般会造成超过此数量的用户无法连接数据库，造成错误500。\
3、 **网卡流量**\
风险：网卡IO会被占满（千兆网卡=1000Mb/8 约=100MB）\
解决办法：
    1. 减少从服务器的数量（从服务器从主服务器中复制日志，造成网络流量变大）
    2. 进行分级缓存（避免前端Web服务器突然一下子缓存太多）
    3. 避免使用”select  *“进行查询
    4. 分离业务网络和服务器网络
4、 **磁盘IO**\
风险：
    1. 磁盘IO性能突然下降，解决办法（使用更快的磁盘设备）。
    2. 其他大量消耗磁盘性能的计划任务（调整计划任务，做好磁盘维护）
5、 **大表**\
特点：
    1. 记录行数巨大，单表超过1000W行
    2. 表数据文件巨大，超过10G

大表对查询的影响：
慢查询：超过指定时间的SQL语句查询\
慢查询语句：EXPLAIN SELECT语句\
*举个例子*：
```
# 查看慢查询的时间，假如查询超过3s，就是慢查询
mysql> show variables like "long%";
+-----------------+----------+
| Variable_name   | Value    |
+-----------------+----------+
| long_query_time | 3.000000 |
+-----------------+----------+
1 row in set (0.02 sec)

# 这是用来举例子的表
mysql> desc device_operation_sendrecord;
+-------------+-------------+------+-----+---------+----------------+
| Field       | Type        | Null | Key | Default | Extra          |
+-------------+-------------+------+-----+---------+----------------+
| create_time | datetime(6) | NO   |     | NULL    |                |
| modify_time | datetime(6) | NO   |     | NULL    |                |
| send_id     | int(11)     | NO   | PRI | NULL    | auto_increment |
| send_time   | datetime(6) | NO   |     | NULL    |                |
| send_status | varchar(10) | NO   |     | NULL    |                |
| device_id   | int(11)     | YES  | MUL | NULL    |                |
+-------------+-------------+------+-----+---------+----------------+
6 rows in set (0.88 sec)

# 慢查询的例子：
mysql> explain select * from device_operation_sendrecord where send_status like '%s%'\G;
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: device_operation_sendrecord
         type: ALL                              # 检索方式：ALL 表示全表扫描，通常ALL不好
possible_keys: NULL                             # 显示可能应用在这张表的索引（但可能没有使用索引）
          key: NULL                             # 实际使用的索引，若为NULL，则表示没有使用索引
      key_len: NULL                             # 索引长度
          ref: NULL
         rows: 403                              # sql语句扫描的长度
        Extra: Using where                      # sql语句额外开销
1 row in set (0.04 sec)

# 使用了索引主键查询
mysql> explain select * from device_operation_sendrecord where send_id = 6\G;
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: device_operation_sendrecord
         type: const
possible_keys: PRIMARY
          key: PRIMARY
      key_len: 4
          ref: const
         rows: 1
        Extra: NULL
1 row in set (0.03 sec)
```
慢查询工具：
    1. hook，在服务端sql语句执行前触发hook（explain select）
    2. 对queryset进行分析，检出有可能产生慢查询的sql语句
    3. 向RD、QA自动发送慢查询报警邮件

大表对DDL操作的影响：
    1. 建立索引需要很长时间。
    2. 修改表结构需要长时间锁表，造成主从延迟，影响正常数据库操作。

解决大表问题：
- 分库分表：
难点：
    1. 分库主键的选择
    2. 分表后跨分区数据的查询和操作

- 大表历史数据归档：
减少前后端业务的影响
难点：
    1. 归档时间点选择
    2. 如何进行归档操作

- 分库分表有哪几种形式？优势和劣势分别是什么？
*TODO*

6、 **大事务**\
大事务：运行时间比较长，操作数据比较多\
事务开启：BEGIN;\
事务关闭：COMMIT;\
事务的概念：
    1. 事务是数据库系统区别于其他一切文件系统的重要特性之一。
    2. 事务是一组具有原子性的SQL语句，或是一个独立的工作单元。\
特点：原子性、一致性、隔离性和持久性（ACID）

**脏读**：脏读就是指当一个事务正在访问数据，并且对数据进行了修改，而这种修改还没有提交到数据库中，这时，另外一个事务也访问这个数据，然后使用了这个数据。（未提交 读）\
**不可重复读**：是指在一个事务内，多次读同一数据。在这个事务还没有结束时，另外一个事务也访问该同一数据。那么，在第一个事务中的两 次读数据之间，由于第二个事务的修改，那么第一个事务两次读到的的数据可能是不一样的。这样就发生了在一个事务内两次读到的数据是不一样的，（不可重复读）\
**幻读**：是指当事务不是独立执行时发生的一种现象，例如第一个事务对一个表中的数据进行了修改，这种修改涉及到表中的全部数据行。 同时，第二个事务也修改这个表中的数据，这种修改是向表中插入一行新数据。那么，以后就会发生操作第一个事务的用户发现表中还有 没有修改的 数据行，就好象 发生了幻觉一样。

大事务的风险：
    1. 锁定太多数据，造成大量阻塞和锁超时
    2. 回滚需要的时间比较长
    3. 执行时间长，容易造成主从延时

处理大事务：
    1. 避免一次处理太多数据（分批次处理）
    2. 移出不必要的事务中的SELECT操作
