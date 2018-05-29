---
layout: post
title: "MySQL 基础入门"
author: "Dzreal"
categories: db
tags: [db]
image: mysql-perform.jpg
---
# MySQL 基础入门

## MySQL 体系结构

```
graph LR
Client-API-->连接管理层
连接管理层 --> SQL层
SQL层 --> 引擎层 
引擎层 --> 物理存储层
```

1. Client-API：Mysql连接器（connectors）  

Include : Native C API, JDBC, ODBC, .NET, PHP, Python, Perl, Ruby, VB...

2. 连接管理层（connection Pool）  

管理连接数
Authentication - Thread Reuse - Connection Limits - Check Memory - Caches

3. SQL层  

    1. SQL Interface（DML，DDL）  

    2. Parser  

    3. Optimizer  

    4. Caches & Buffers

4. 引擎层

Include : InnoDB, MyISAM, Cluster, Archive, Merge, Memory, Partner, Community, Custom

5. 物理存储层

File System : NTFS - NFS, SAN - NAS

Files &Logs : Redo, Undo, Data, Index, Binary, Error, Query, Slow 

