---
layout: post
title: "MySQL 入门知识"
author: "Dzreal"
categories: db
tags: [db]
image: mysql-base.jpg
---
# MySQL 入门知识

## MySQL 体系结构

```
graph LR
Client-API <--> 连接管理层 <--> SQL层 <--> 引擎层 <--> 物理存储层
```

1. Client-API：Mysql连接器（connectors）  

包括 : Native C API, JDBC, ODBC, .NET, PHP, Python, Perl, Ruby, VB...

2. 连接管理层（connection Pool）  

管理连接数
Authentication - Thread Reuse - Connection Limits - Check Memory - Caches

3. SQL层  

    1. SQL Interface（DML，DDL）  

    2. Parser  

    3. Optimizer  

    4. Caches & Buffers

4. 引擎层

包括 : InnoDB, MyISAM, Cluster, Archive, Merge, Memory, Partner, Community, Custom

5. 物理存储层

File System : NTFS - NFS, SAN - NAS

Files &Logs : Redo, Undo, Data, Index, Binary, Error, Query, Slow 


## MySQL 存储引擎的差异

特点 | Myisam | NDB | Memory |InnoDb
:-:  | :-: | :-: | :-: | :-:
存储限制 | 没有 | 没有 | 有 | 64TB 
事务安全 |      | 支持 |     | 支持
锁机制   | 表锁 | 页锁 | 表锁 | 行锁
B树索引  | 支持 | 支持 | 支持 | 支持
哈希索引 |      |      | 支持 | 支持
全文索引 | 支持 |      |      | 
集群索引 |      |      |      | 支持
数据缓存 |      |      | 支持 | 支持
索引缓存 | 支持 |      | 支持 | 支持
数据可压缩 | 支持 |    |      |     
空间使用 |  低  |  低  |  N/A | 高    
内存使用 |  低  |  低  |  中等 | 高    
批量插入的速度 | 高  | 高  | 高  | 低 
支持外键 |      |      |      | 支持    


## MySQL 主从延迟时间计算

从库上执行
```
SHOW SLAVE STATUS\G;  #查看从库状态
```

behind_master_sconds = IO线程的时间戳 - SQL线程的时间戳

完整主从延迟 = behind_master_sconds + Master_slave_trans_delay

## MySQL 常见连接错误  

2003：Can't connect to MySQL server ##一般是网络超时  

2006：Server has gone away ## dbproxy在重启时/client端超时  

2013：Lost connection … during query ##可能dbproxy在重启

