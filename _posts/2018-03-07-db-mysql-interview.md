---
layout: post
title: "db Interview"
author: "Dzreal"
categories: db
tags: [db]
image: db-interview.jpg
---
# 数据库（关系型/非关系型） 面试题汇总

## 自己总结的面试题

**table of contents**
* [1. 【mysql】一条 sql 查询汇总](#1-一条sql查询汇总)


## 1 一条sql查询汇总

1. 给出下列表（图表A），请用一条sql查询出所有学生分别的分数总和，并按分数从大到小进行排列，结果如图表B：

```sql
（图表A）
mysql> select * from user;
+-----+------+--------+-------+
| id  | name | lesson | score |
+-----+------+--------+-------+
| 296 | A    | a      |   100 |
| 297 | A    | b      |    90 |
| 298 | B    | a      |    32 |
| 299 | B    | b      |    21 |
| 300 | C    | a      |   100 |
| 301 | C    | b      |    99 |
+-----+------+--------+-------+

（图表B）
+------+--------+
| name | scores |
+------+--------+
| C    |    199 |
| A    |    190 |
| B    |     53 |
+------+--------+

答案：
mysql> SELECT name, sum(score) AS scores FROM user GROUP BY name ORDER BY scores DESC

```
