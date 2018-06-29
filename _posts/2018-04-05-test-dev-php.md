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
3. print_r() - **可以打印变量以及数组**
4. var_dump() **打印变量的相关信息,包括输出索引和值**
5. var_export() **输出或返回一个变量的字符串表示,返回值是合法的PHP代码,第二个参数加true,返回变量的表示。也就是，加上true之后，把$a = var_export($s,true)，可以用echo打印出来 $a**

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
$txt1 = "Hello"; $txt2 = $txt1 . " world!"
// $txt2 = "Hello world!"
// .= 串接赋值
$txt1 = "Hello"; $txt1 .= " world!"
// $txt1 = "Hello world!"
```











