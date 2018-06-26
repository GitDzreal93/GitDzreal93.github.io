---
layout: post
title: "Python base"
author: "Dzreal"
categories: python
tags: [python]
image: python-base.jpg
---

# python 基础

### python的运行过程

1. ==源代码== 。xxx.py（.py文件）
2. ==编译== 。执行 python xxx.py，python 解释器把 xxx.py 编译成字节码对象 ==PyCodeObject（包含一些字节码指令），存在内存里==；编译完后，会生成pyc文件（.pyc 文件是字节码对象在硬盘上的表现形式），这样下次运行就不用再次编译
3. ==执行字节码指令==。通过 python 虚拟机（PVM）去执行字节码指令


```graph LR
源代码-->解释器
解释器-->虚拟机
```
---
### 数据类型

变量：自动在栈区分配动态内存，不用定义变量类型\
常量：大写表示

1. 整数 
2. 浮点数
3. 字符串
4. 布尔
5. 空值
6. 列表 : list，一种有序集合，用[]表示
7. 元组 ：tuple，另一种有序集合，用()表示，==一旦初始化之后，就不能修改==
8. 字典 ：dict，存储键值对，用{xxx：yyy}表示
9. 集合 : set，无序和无重复元素的集合，是存储key的集合，s = set(list)

---
### 字符串（str）

表示方法：
- 'xxx'
- "xxx"
- '''xxx'''

字符串操作 （常用的差不多有18个操作）：
```python
#拼接字符串
#(1)字符串 "+" , 拼接字符串
s = "xxx" + "yyy"
#结果：s = "xxxyyy"

#(2)字符串 "*" ，重复之前的字符串n次
s = "abc"*3
#结果：s = "abcabcabc"

#(3)格式化字符串
#s = "hello,my name is PPP, I'm XXX years old" 
#法1：
s = "hello,my name is %s, I'm %d years old" % ('Dzreal', 100)
#法2：
s = "hello,my name is {},I'm {} years old".format('Dzreal', 100)

#(4)字符串切片
s = "qazwsxedc123456"
a = s[1:5:2]
#结果：a = "aw"

#(5)字符串去除空格
s = "   abcdef "
b = s.strip()
#结果：b = "abcdef"
#去除左边空格或其他字符：lstrip()
#去除右边空格或其他字符：rstrip()

#(6)复制字符串
s = "abcde"
a = s
print(id(a))
print(id(s))
#结果：a = "abcde",a 的id和 s 的id一样

#(7)解压字符串
s = "abcdef"
a, b, c, d, e, f = s
#结果：a = "a", b = "b", ... f = "f"

#(8)查找字符串(查找字符并获取该字符对应的索引值)
s = "abcdefg"
a = s.index('a')
b = s.find('a')
c = s.index('x')
d = s.find('x')
#结果：
# a = 0
# b = 0
# c 报错 ValueError: substring not found
# d = -1

# find 和 index 的区别：
# str.index 和str.find 功能相同，区别在于find()查找失败会返回-1，不会影响程序运行。一般用find!=-1或者find>-1来作为判断条件。

#(9)比较字符串（左值>右值：1；左值<右值：-1）
a = '100'
b = '888'
cmp(a,b)
#结果：-1

#(10)检查是否包含指定字符串
in | not in
s = "abcdefg"
'a' in s
's' in s
#结果: 
# True
# False

#(11)字符串长度
s = "abc"
len(s)
#结果：3

#(12)字符串中字母大小写转换
str.lower() #转换为小写
str.upper() #转换为大写
str.swapcase() #大小写转换
str.capitalize() #首字母大写

#(13)将字符串居中，指定长度及填充两边字符
s = "hello"
s.center(10,'*')
#结果：**hello***

#(14)字符串统计(统计某个字符出现的次数)
s = 'aabbbcc'
s.count('a')
#结果：2

#(15)字符串替换(传参：旧str,新str,替换次数)
s = "hello"
s.replace('e','a')
s.replace('l','p',2)
#结果：
# hallo
# heppo

#(16)按某字符分割字符串，并转成数组
s = 'helloxpppxqqqxsssxiii'
s.splite('x',3)
#结果：['hello', 'ppp', 'qqq', 'sssxiii']
#按'x'来切分，因为只切分3次，所以最后的元素里面的x不作为切分，假如不加切分次数，则全局切分

#(17)数组转化为字符串（可以这么理解，每个列表元素用某字符串连接）
s = ''
d = '-'
l = ['a', 'b', 'c']
p = s.join(l)
q = s.join(l)
#结果：p = 'abc', q = 'a-b-c' 

#(18)字符串转化为字典 and 字典转化为字符串
s = "{'a':5,'b':6,'c':7}"
d = eval(s)
s = str(d)
#结果：
#d = {'a':5,'b':6,'c':7}
#s = "{'a':5,'b':6,'c':7}"
```

---
### 列表（list）

表示方法：

l = [1,2,3,4,5]

l = list()

l = []

数组操作：
```python
#(1)定义一个数组
l = list()
l = []

#(2)定义并初始化一个数组
l = [1,2,3,4,5]

#(3)数组末尾添加元素
l.append(i)
# 注意下面这种情况：
lis1 = [1,2,3,4,5]
lis2 = [3,4,5,6,7]
lis1.append(lis2)
# 结果：lis1 = [1,2,3,4,5,[3,4,5,6,7]]

#(4)统计数组中某个元素出现次数
l.count(i)

#(5)列表合并（也可以直接+连接）
l = [1, 2, 3, 4, 5]
p = ['a', 'b', 'c', 'd']
lis = l + p 
l.extend(p)
# 结果: 
# lis = [1, 2, 3, 4, 5, 'a', 'b', 'c', 'd'] 
# l = [1, 2, 3, 4, 5, 'a', 'b', 'c', 'd'] 

#(6)在一定范围内查询元素，并返回索引值
l = ['a','b','c','w']
l.index('a', 0, 3)
#结果:0

#(7)插入元素（必须指定在某个索引位置）
l = ['a','b','c','w']
l.insert(2,'t')
#结果：l = ['a','b', 't', 'c', 'w']

#(8)尾部(右侧)删除元素
l.pop()

#(9)删除某个元素
l.remove('a')

#(10)反转顺序
l.reverse()

#(11)排序
l.sort()

```


---
### 元组（tuple）

---
### 字典（dict）

---
### 集合（set）




