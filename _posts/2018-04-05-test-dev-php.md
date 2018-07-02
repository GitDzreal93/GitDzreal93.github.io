---
layout: post
title: "Test-Dev PHP-Note"
author: "Dzreal"
categories: test-dev
tags: [test-dev]
image: php-note.jpg
---

# php 笔记本

### PHP 变量作用域
- local（局部）
- global（全局）
- static（静态）

> 备注：

local：**函数内部声明的变量拥有 LOCAL 作用域，只能在函数内部进行访问。**

使用场景：函数内才能访问

global：**函数之外声明的变量拥有 Global 作用域，只能在函数以外进行访问。**

使用场景：全局变量，函数内要是想使用全局变量，有两种方式：
1. global $x -- 用关键字声明全局变量
2. $GLOBALS['x'] -- GLOBALS[index] 数组中存储了所有的全局变量

static：**通常，当函数完成/执行后，会删除所有变量。不过，有时我需要不删除某个局部变量。实现这一点需要更进一步的工作。要完成这一点，请在您首次声明变量时使用 static 关键词**


### PHP 超全局变量

- $GLOBALS  --- 引用全局作用域中可用的全部变量
- [$_SERVER](http://www.w3school.com.cn/php/php_superglobals.asp)  --- 超全局变量保存关于报头、路径和脚本位置的信息。 
- $_REQUEST
- $_POST
- $_GET
- $_FILES
- $_ENV
- $_COOKIE
- $_SESSION



### echo、print、print_r、var_dump、var_export的区别：

> 参考：
- [W3School](http://www.w3school.com.cn/php/php_echo_print.asp)

1. echo - **能够输出一个以上的字符串，不能打印数组，打印数组返回NULL**

示例：
```php
<?php
$txt1="Learn PHP";
$txt2="W3School.com.cn";
$cars=array("Volvo","BMW","SAAB");

echo $txt1;
echo "<br>";                
echo "Study PHP at $txt2";                                              # 输出变量，整个字符串要用“”
echo "My car is a {$cars[0]}";                                          # 输出数组变量要加{}
echo "This", " string", " was", " made", " with multiple parameters.";  # 输出多个字符串

?>
```
2. print - **只能输出一个字符串，并始终返回 1，不能打印数组，打印数组返回NULL**
3. print_r(); - **可以打印变量以及数组**
4. var_dump(); **打印变量的相关信息,包括输出索引和值**
5. var_export(); **输出或返回一个变量的字符串表示,返回值是合法的PHP代码,第二个参数加true,返回变量的表示。也就是，加上true之后，把$a = var_export($s,true)，可以用echo打印出来 $a**

### PHP的数据类型：

字符串、整数、浮点数、逻辑、数组、对象、NULL

### PHP的运算符

```php
// 递增/递减运算符
++$x	//前递增	$x 加一递增，然后返回 $x
$x++	//后递增	返回 $x，然后 $x 加一递增
--$x	//前递减	$x 减一递减，然后返回 $x
$x--	//后递减	返回 $x，然后 $x 减一递减

// == 和 === 的区别：
$x == $y    //如果 $x 和 $y 拥有相同的键/值对，则返回 true。
$x === $y   //如果 $x 和 $y 拥有相同的键/值对，且顺序相同类型相同，则返回 true。
```

### PHP的switch语句
```php
switch (表达式)
{
case 标签1:
  code to be executed if 表达式 = 标签1;
  break;  
case 标签2:
  code to be executed if 表达式 = 标签2;
  break;
default:
  code to be 执行
  if 表达式 is different 
  from both 标签1 and 标签2;
}
```

### PHP的循环
1. while - 只要指定条件为真，则循环代码块
2. do...while - 先执行一次代码块，然后只要指定条件为真则重复循环
3. for - 循环代码块指定次数
4. foreach - 遍历数组中的每个元素并循环代码块

### PHP字符串操作函数

```php

// 返回字符串的长度
echo strlen("hello world!");

// 检索字符串内指定的字符和文本, 返回所要查找的字符串的首字母的位置
echo strpos("hello world!","world");
// 输出 6

// 字符串运算符
// . 串接
$txt1 = "Hello"; $txt2 = $txt1 . " world!";
// $txt2 = "Hello world!"
// .= 串接赋值
$txt1 = "Hello"; $txt1 .= " world!";
// $txt1 = "Hello world!"
```

### PHP数组操作函数

```php

// 数组长度
count($arr);   // 返回数组的长度
sizeof($arr);  // 返回数组的长度

// 数组排序
sort($arr); // 以升序对数组排序
rsort($arr); // 以降序对数组排序
asort($arr); // 根据值，以升序对关联数组进行排序
ksort($arr); // 根据键，以升序对关联数组进行排序
arsort($arr); // 根据值，以降序对关联数组进行排序
krsort($arr); // 根据键，以降序对关联数组进行排序
array_reverse($arr); //数组逆序 
shuffle($arr); //数组乱序操作

// 数组合并
array_combine($arr1, $arr2); // 数组合并
array_merge($arr1, $arr2); // 数组合并

// 数组统计
array_count_values($arr); // 统计数组中所有值出现的次数

// 差集： $arr1 有 $arr2没有的部分
array_diff($arr1, $arr2，..); // 返回两个数组的差集数组（只比较键值）
array_diff_assoc($arr1, $arr2，..); // 返回两个数组的差集数组（比较键名和键值）
array_diff_key($arr1, $arr2，..); // 返回两个数组的差集数组（只比较键名）

// 其他
array_flip($arr); // 键值与键名互换
array_rand($arr, $ele_num); // 随机返回ele_num个元素，需要用新的数组变量接收

// 交集：$arr1 和 $arr2 都有的部分
array_intersect($arr1, $arr2，..); // 返回两个数组的交集（只比较键值）
array_intersect_assoc($arr1, $arr2，..); // 返回两个数组的交集（比较键名和键值）
array_intersect_key($arr1, $arr2，..); // 返回两个数组的交集（只比较键名）

// 数组键名操作
array_keys($arr); // 返回数组中的所有键名
array_keys_exists("key_name",$arr); // 检查某个键名是否存在于数组中

// 出入栈
array_pop($arr); // 删除数组中最后一个元素（出栈）
array_push($arr, $ele, ..); // 数组末尾添加元素（入栈）

// 元素查找
array_search("value", $arr); // 根据键值去查找，返回键名
in_array("value", $arr); // 判断键值是否存在于数组中

// math
array_sum($arr); // 数组元素相加
array_product($arr); // 数组元素相乘

// 数组去重、过滤
array_unique($arr); // 删除数组中的重复值
array_filter($arr, "functionName"); // 用回调函数（自定义的function），过滤数组中的值

```

> 更多↓：

[Array](http://www.w3school.com.cn/php/php_ref_array.asp)

### PHP掌控时间

```php
// 日期
date_diff($date1, $date2, TRUE); // 求两个日期的差值,第三个参数表示，两个时间的差值必须是正数。第三个参数默认参数是False
$date=date_create("2016-09-25"); // 创建时间
date_format($date,"Y/m/d H:i:s"); // 返回格式化的时间
date("Y/m/d H:i:s"，time()); // 格式化本地时间

time(); // 返回当前时间的 Unix 时间戳
microtime(); // 返回当前时间的微秒数
localtime(time(),TRUE); // 返回本地时间
strtotime(); // 将任何英文文本的日期或时间描述解析为 Unix 时间戳


```

> 更多↓：

[data](http://www.w3school.com.cn/php/func_date_date.asp)

### PHP操作数据库
```php

$conn = mysqli_connect(servername,username,password); // 连接数据库

mysql_select_db("my_db", $con); // 选择数据库

$sql = "SELECT * FROM tableName" // sql语句

$result = mysql_query($sql);  // 获取结果集

while($row = mysql_fetch_array($result))
// 从遍历结果集获取每行数据，以数组形式返回
  {
  echo $row['FirstName'] . " " . $row['LastName'];
  }

mysql_close($con); // 关闭连接

```

> 更多↓：

[data](http://www.w3school.com.cn/php/func_date_date.asp)
















