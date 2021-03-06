---
layout: post
title: "Python Interview"
author: "Dzreal"
categories: python
tags: [python]
image: interview.jpg
---

# python面试题相关

**table of contents**

1. [github上 5280+star 的面试题](https://github.com/taizilongxu/interview_python#1-python%E7%9A%84%E5%87%BD%E6%95%B0%E5%8F%82%E6%95%B0%E4%BC%A0%E9%80%92)
2. [python面试题 300 道](https://www.cnblogs.com/wupeiqi/p/9078770.html)
3. [django 后端开发面试题](https://blog.csdn.net/ayocross/article/details/56509840?utm_source=itdadao&utm_medium=referral)
4. [自己总结的面试题](#自己总结的面试题)

---

## 自己总结的面试题

**table of contents**
* [1. 如何去除列表中的重复元素](#1-如何去除列表中的重复元素)
* [2. 两个列表如何生成一个对应的字典](#2-两个列表如何生成一个对应的字典)
* [3. python 如何生成随机数](#3-python如何生成随机数)
* [4. 字符串逆序和统计字符串中字母出现的次数](#4-字符串逆序和统计字符串中字母出现的次数)
* [5. 如何在列表，字典，集合中根据条件筛选数据？](#5-如何在列表，字典，集合中根据条件筛选数据？)
* [6. 如何优雅地操纵tuple的索引（如何给元祖中的索引命名，提高可读性）](#6-如何优雅地操纵tuple的索引（如何给元祖中的索引命名，提高可读性）)
* [8. 字典排序](#8-字典排序)
* [9. 如何快速找到多个字典的公共键（key）](#9-如何快速找到多个字典的公共键（key）)
* [10. 如何让字典保持有序](#10-如何让字典保持有序)
* [11. 猜数字游戏](#11-猜数字游戏)
* [12. 迭代器和可迭代对象](#12-迭代器和可迭代对象)
* [13. 【算法】八大排序算法的python实现](#13-八大排序算法的python实现)
* [14. 【算法】费波拉契数列的python实现（多种方法实现）](#14-费波拉契数列的python实现)
* [15. python的字典合并](#15-python的字典合并)
* [16. python的socket编程](#16-python的socket编程)
* [17. 【程序设计】在有序列表里面，查找某个值的位置](#17-【程序设计】在有序列表里面，查找某个值的位置)
* [18. 【程序设计】判断一个字符串中的 "{", "}" 是不是成对出现的](#18-【程序设计】判断一个字符串中的“括号”是不是成对出现的)
* [19. 【程序设计】修改某个文本文件中的某个字符串](#19-【程序设计】修改某个文本文件中的某个字符串)
* [20. python的赋值、浅拷贝和深拷贝的区别](#20-python的赋值、浅拷贝和深拷贝的区别)
* [21. 【程序设计】返回字符串中第一个不重复的字母和位置](#21-【程序设计】返回字符串中第一个不重复的字母和位置)
* [22. 【程序设计】求一个数字列表里，相邻两数乘积最高的值，及这两个数分别是多少](#22-【程序设计】求一个数字列表里，相邻两数乘积最高的值，及这两个数分别是多少)





---

## 1 如何去除列表中的重复元素

*【题目】* 给出一个列表：lis = [4,2,1,3,4,2,3,1,3,2,2,2]，去除列表中的重复元素。

**解答**
```python
lis = [4,2,1,3,4,2,3,1,3,2,2,2]

# 解法1:
lis1 = list(set(l))

# 结果：lis1 = [1,2,3,4], 这样会改变列表的原有顺序

# 解法2：
lis2 = []
for i in l:
    if i not in lis2:
        lis2.append(i)

# 结果：lis2 = [4,2,1,3], 这样保持了原有的顺序
```   

## 2 两个列表如何生成一个对应的字典

*【题目】* 给出

l1 = ['Ben', 'Funn', 'Mike', 'Ronaldo']

l2 = [17, 18, 18, 16]

合并两个列表，生成 d =  {'Ben': 17, 'Funn': 18, 'Mike': 18, 'Ronaldo': 16}

**解答**
```python
l1 = ['Ben', 'Funn', 'Mike', 'Ronaldo']
l2 = [17, 18, 18, 16]
d = dict(zip(l1, l2))
# 结果: d =  {'Ben': 17, 'Funn': 18, 'Mike': 18, 'Ronaldo': 16}

# 反之，一个字典如何生成两个列表？
# 解法：用zip(*)函数，zip(*)会生成一个zip对象，即把[(a,b),(c,d),(e,f)]拆分成[(a,c,e)(b,d,f)],（此处只是伪代码帮助理解，实际上可能实现的过程并不是如此）
l1 = list(list(zip(*d.items()))[0])
l2 = list(list(zip(*d.items()))[1])

# 结果：
# l1 = ['Ben', 'Funn', 'Mike', 'Ronaldo']
# l2 = [17, 18, 18, 16]

```

## 3 python如何生成随机数

*【题目】* 利用 python 生成随机数

**解答** 
```python
import random
random.random()	#没有参数，随机生成一个0-1之间的浮点数
random.randint(n, m)	#随机在n-m之间生成一个整数, 注意：n不能比m大，否则会报错
random.randrange(n, m, 2)	#在n-m之间随机生成一个偶数
random.randrange(n, m, 1)	#在n-m之间随机生成一个奇数
random.choice(list/str/tuple)	#在序列中随机抽取一个元素
random.shuffle(list/str/tuple)		#随机将一个序列的的顺序打乱
```

## 4 字符串逆序和统计字符串中字母出现的次数

*【题目】*

(1)s = 'I love python'，怎么实现逆序（output = 'nohtyp evol I'）。

(2)进阶：如何实现(output = python love I)

(3)如何统计s中的每个字母的出现的次数。

**解答**
```python
# (1)题
s = 'I love python'
# 解法1：通过索引的方法
s = [::-1]
# 解法2：借助列表翻转
li = []
for i in s:
    li.append(i)
li.reverse()
s = ''.join(li)
# 结果：s = 'nohtyp evol I' , 这里再提一下list转str的用法：
# 不能直接用 s = str(li), 否则生成的是 "['n', 'o', 'h', 't', 'y', 'p', ' ', 'e', 'v', 'o', 'l', ' ', 'I']" 与预期不符
# 应该用 ''.join(list)，这样做的话，意思是：在li中每一个元素后面加上''，即每个元素用''连接生成新的字符串，另外，''里面不能加空格，否则会生成：'n o h t y p   e v o l   I'，中间会加上空格

#（2）题
s = 'I love python'
li = s.split(' ')
li.reverse()
s = ''.join(li)
# 结果：s = ['python', 'love', 'I'] , 解题思路：先把字符串转化为数组，然后数组反转，再转化为字符串

#（3）题
s = 'I love python'
# 解法1
from collections import Counter
d = dict(Counter(s))
# 结果：d = {'I': 1, ' ': 2, 'l': 1, 'o': 2, 'v': 1, 'e': 1, 'p': 1, 'y': 1, 't': 1, 'h': 1, 'n': 1}
# 假如说想要去掉空格的统计,只需要 d.pop(' ')即可，结果是：
# {'I': 1, 'l': 1, 'o': 2, 'v': 1, 'e': 1, 'p': 1, 'y': 1, 't': 1, 'h': 1, 'n': 1}

# 解法2
d = {}
for i in s:
    d[i] = s.count(i)

# 结果：d = {'I': 1, ' ': 2, 'l': 1, 'o': 2, 'v': 1, 'e': 1, 'p': 1, 'y': 1, 't': 1, 'h': 1, 'n': 1}

# 解法3
from collections import defaultdict
s = 'I love python'
d = defaultdict(int)
for i in range(len(s)):
    d[s[i]] += 1
# 结果：defaultdict(<class 'int'>, {'I': 1, ' ': 2, 'l': 1, 'o': 2, 'v': 1, 'e': 1, 'p': 1, 'y': 1, 't': 1, 'h': 1, 'n': 1})   
```

## 5 如何在列表，字典，集合中根据条件筛选数据？

*【题目】*

(1)（列表）：创建一个随机列表（-10,10）之间，并过滤出负数

(2)（字典）：创建一个随机生成学生分数的字典，并过滤出分数高于90的学生。

(3)（集合）：筛出集合中能被3整除的元素：

**解答**：
```python
# （1）列表
from random import randint
li = [randint(-10,10) for _ in range(10)]
# 解法1 -- 过滤法    （可采纳）
li1 = list(filter(lambda x:x>=0 , li))
# 解法2 -- 列表生成式 （最快）	
li2 = [i for i in li if i >= 0]
# 解法3 -- 迭代       （最慢且最不方便，不建议使用）
li3 = []
for i in li:
    if i >= 0:
        li3.append(i)

# （2）字典
# 创建一个随机生成学生分数的字典，这里采用的是faker库来随机生成中文学生名，并用字典生成式过滤出分数大于90的学生
from faker import Faker
f = Faker(locale='zh_CN')
all_dict = {f.name() : randint(60,100) for _ in range(1,100)}
perfect_dict = {name:score for name, score in all_dict.items() if score > 90} 

# （3）集合
data = [randint(-10,10) for _ in range(10)]
s = set(data)
s1 = { x for x in s if x % 3 == 0 }
```

## 6 如何优雅地操纵tuple的索引（如何给元祖中的索引命名，提高可读性）

*【题目】*  假设有一个学生系统，里面的数据格式是：

（名字，年龄，性别，邮箱地址）

例如：student =（'Dzreal', 24, 'male', 'dzreal_93@126.com'）

假如用索引 tup[0] 获取学生名字的话，可读性会比较差，如何解决？

**解答**
```python
# 解法1：枚举的方式
# 假设：
student_A =('Dzreal', 24, 'male', 'dzreal_93@126.com')

NAME = 0
AGE = 1
SEX = 2
EMAIL = 3
# 通常，枚举还可以这么写：NAME, AGE, SEX, EMAIL = range(4)

print(studentA[NAME])
# 结果：Dzreal

# 解法2：采用collections库的namedtuple，其实自己去创建一个学生类也是可以的
Student = namedtuple('Student', ['name', 'age', 'sex', 'mail'])
student_A = Student('Dzreal', 24, 'male', 'dzreal_93@126.com')
print(student_A.name)
# 结果：Dzreal
```

## 7 对某英文文章的单词，进行词数统计

*【题目】* 假设有一篇英文文章：English.txt，求出现次数最高的10个单词，并且这10个单词中每个单词出现的频数

**解法**
```python
# 采用正则表达式进行分词操作，再用collections库的Counter进行词频统计
import re
from collections import Counter

txt = open('English.txt', 'r').read()
res = re.split('\W+', txt)		#用正则表达式的split对txt整个字符串的单词进行分割(\W+表示特殊字符，差不多和[^a-zA-Z0-9_]等价，而\w+和[a-zA-Z0-9_]等价)，split返回值是数组，用法和str.split差不多
all_counter = Counter(res) 	#用Counter统计出现单词的次数
top10 = all_counter.most_common(10)			#对出现次数最多的10个单词进行统计
print(top10)
# 结果：[('in', 6), ('to', 5), ('subway', 5), ('the', 4), ('a', 3), ('app', 3), ('on', 3), ('city', 3), ('by', 3), ('have', 3)]

# tips：假如是中文文档，可以用jieba分词
```

## 8 字典排序
*【题目】* 将全班30名同学的成绩单进行排序(从大到小)

**解答**
```python
from faker import Faker
f = Faker(locale='zh_CN')
all_stu_dict = {f.name() : randint(0,100) for _ in range(30)}

# 思路：用sorted()函数去派去，sorted()函数适用于可迭代对象：sorted(iterable, cmd=None, key=None, reverse=False)
# cmp 是用于比较的函数，比较什么由key 决定
# key 是列表元素的某个属性或函数进行作为关键字，有默认值，迭代集合中的一项
# reverse = True 表示降序， reverse= False 表示升序

# 解法1 化为元祖，根据元祖中分数，去进行排序，缺点:key和value的值会颠倒
tup = zip(all_stu_dict.values(), all_stu_dict.keys())
rank = sorted(tup, reverse=True)

# 解法2 直接用sorted，并且制定规则来排序
rank = sorted(all_stu_dict.items(), key=lambda x:x[1], reverse=True)
```

## 9 如何快速找到多个字典的公共键（key）

*【题目】* 世界杯小组赛，每轮比赛球员进球统计如下：

第一轮：{'C罗':3, '格里兹曼':2, '内马尔':1, '博格巴':1}

第一轮：{'C罗':2, '格里兹曼':0, '内马尔':0,'梅西':2}

第一轮：{'C罗':4, '内马尔':2, '库蒂尼奥':2, '姆巴佩':2}

统计每轮比赛都有进球的球员

**解答**
```python
d1 = {'C罗': 3, '格里兹曼': 2, '内马尔': 1, '博格巴': 1}
d2 = {'C罗': 2, '格里兹曼': 0, '内马尔': 0, '梅西': 2}
d3 = {'C罗': 4, '内马尔': 2, '库蒂尼奥': 2, '姆巴佩': 2}

# 解法1  迭代（效率最低）
shooter_list = []
for shooter in d1:
    if shooter in d2 and shooter in d3:
        shooter_list.append(shooter)

# 解法2 利用map分别取出每轮进球的球员名字，再用reduce对每轮都进球的球员进行取交集
all_shooters = map(dict.keys, [d1, d2, d3])
shooter_list = reduce(lambda a, b: a & b, all_shooters)
```

## 10 如何让字典保持有序

*【题目】* 创建一个字典，让其能够按数据插入的先后顺序排列

**解答**
```python

# 思路：OrderedDict 有序字典,是对字典的补充,他能记录字典的添加顺序,相当于字典和列表的组合,使用之前需要导入依赖类 import collections 

from collections import OrderedDict
d1 = OrderedDict()
d2 = dict()

# 解析：不知道是不是python3的特性，dict创建的字典和OrderedDict创建的字典,都是按插入的时间顺序去排列的,OrderedDict除了和dict类型上有些差别之外，暂时还不明白2者有什么比较大的差异性
```

## 11 猜数字游戏

*【题目】* 制作一个简单的猜数字游戏，添加历史记录功能(最多N条)，显示用户最近猜过的数字

**解答**
```python
from random import randint
from collections import deque

N = randint(0, 100)
history = deque([], 5)
k = 0


def guess(k):
    if k == N:
        print('You are right!')
        return True

    if k <= N:
        print('{0} is smaller-than N'.format(k))
    else:
        print('{0} is greater-than N'.format(k))
    return False


if __name__ == '__main__':
    while True:
        line = input("please input a number:")

        if line.isdigit():
            k = int(line)
            try:
                history.append(k)
            except Exception as e:
                pass
        else:
            print('param error')
            
        if guess(k):
            break

        if line == 'history' or line == 'h?':
            for i in history:
                print(i)

```

## 12 迭代器和可迭代对象

*【题目】* 分别写一个迭代器和可迭代对象，获取某个城市的气温

**解答**
```python
import requests
from collections import Iterable, Iterator


class WeatherIterator(Iterator):
    def __init__(self, cities):
        self.cities = cities
        self.index = 0

    def __next__(self):
        if self.index == len(self.cities):
            raise StopIteration
        city = self.cities[self.index]
        self.index += 1
        return self.getWeather(city)

    def getWeather(self, city):
        r = requests.get('http://wthrcdn.etouch.cn/weather_mini?city=' + city)
        data = r.json()['data']['forecast'][0]
        return '{}:{} , {}'.format(city, data['low'], data['high'])


class WeatherIterable(Iterable):
    def __init__(self, cities):
        self.cities = cities

    def __iter__(self):
        return WeatherIterator(self.cities)


if __name__ == '__main__':
    target_citys = [u'北京', u'上海', u'广州', u'长春', u'南宁', '深圳']
    
    # 迭代器
    weather_iter = WeatherIterator(target_citys)
    print(weather_iter.__next__())
    print(weather_iter.__next__())
    
    # 可迭代对象
    for info in WeatherIterable(target_citys):
        print(info)
```

## 13 八大排序算法的python实现

*【题目】* 代码实现如下所示的所有排序算法（内部排序【数据记录在内存的排序】）

- （1）（直接）插入排序  【插入排序】
- （2）希尔排序         【插入排序】
- （3）（直接）选择排序  【选择排序】
- （4）冒泡排序         【交换排序】
- （5）归并排序         【归并排序】   
- （6）快速排序         【交换排序】
- （7）堆排序           【选择排序】
- （8）基数排序         【基数排序】

**解答**
> python 实现的八大排序 ：http://python.jobbole.com/82270/

> 详解（虽然不是用Python实现）：https://www.cnblogs.com/RainyBear/p/5258483.html

> 时间复杂度、原理相关 ：https://blog.csdn.net/yuxin6866/article/details/52771739


![总结](http://cricode.qiniudn.com/sort_table.jpg)


```python
# （1）插入排序
# 工作原理：通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。

def insert_sort(lists):
    # 插入排序
    count = len(lists)
    for i in range(1, count):
        key = lists[i]
        j = i - 1
        while j >= 0:
            if lists[j] > key:
                lists[j + 1] = lists[j]
                lists[j] = key
            j -= 1
    return lists


#（2）希尔排序(shell sort)
# 工作原理：直接插入排序的增强版本，也叫缩小增量排序

def shell_sort(lists):
    # 希尔排序
    count = len(lists)
    step = 2
    group = count / step
    while group > 0:
        for i in range(0, group):
            j = i + group
            while j < count:
                k = j - group
                key = lists[j]
                while k >= 0:
                    if lists[k] > key:
                        lists[k + group] = lists[k]
                        lists[k] = key
                    k -= group
                j += group
        group /= step
    return lists


# （3）选择排序
# 工作原理：
# 1）首先在未排序序列中找到最小（大）元素，存放到排序序列的起始位置
# 2）再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。
# 3）重复第二步，直到所有元素均排序完毕。

def select_sort(lists):
    # 选择排序
    count = len(lists)
    for i in range(0, count):
        min = i
        for j in range(i + 1, count):
            if lists[min] > lists[j]:
                min = j
        lists[min], lists[i] = lists[i], lists[min]
    return lists


# （4）冒泡排序
# 工作原理：它重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来。走访数列的工作是重复地进行直到没有再需要交换，也就是说该数列已经排序完成。最后的数是最大的数

def bubble_sort(lists):
    # 冒泡排序
    count = len(lists)
    for i in range(0, count):
        for j in range(i + 1, count):
            if lists[i] > lists[j]:
                lists[i], lists[j] = lists[j], lists[i]
    return lists


# （5）归并排序
# 工作原理：归并排序是建立在归并操作上的一种有效的排序算法,该算法是采用分治法（Divide and Conquer）的一个非常典型的应用。将已有序的子序列合并，得到完全有序的序列；即先使每个子序列有序，再使子序列段间有序。若将两个有序表合并成一个有序表，称为二路归并。

def merge(left, right):
    i, j = 0, 0
    result = []
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result += left[i:]
    result += right[j:]
    return result
 
def merge_sort(lists):
    # 归并排序
    if len(lists) <= 1:
        return lists
    num = len(lists) / 2
    left = merge_sort(lists[:num])
    right = merge_sort(lists[num:])
    return merge(left, right)


#（6）快速排序
# 工作原理：通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

def quick_sort(lists, left, right):
    # 快速排序
    if left >= right:
        return lists
    key = lists[left]
    low = left
    high = right
    while left < right:
        while left < right and lists[right] >= key:
            right -= 1
        lists[left] = lists[right]
        while left < right and lists[left] <= key:
            left += 1
        lists[right] = lists[left]
    lists[right] = key
    quick_sort(lists, low, left - 1)
    quick_sort(lists, left + 1, high)
    return lists


# （7）堆排序
# 工作原理：（Heapsort）是指利用堆这种数据结构所设计的一种排序算法。堆积是一个近似完全二叉树的结构，并同时满足堆积的性质：即子结点的键值或索引总是小于（或者大于）它的父节点。

def adjust_heap(lists, i, size):
    lchild = 2 * i + 1
    rchild = 2 * i + 2
    max = i
    if i < size / 2:
        if lchild < size and lists[lchild] > lists[max]:
            max = lchild
        if rchild < size and lists[rchild] > lists[max]:
            max = rchild
        if max != i:
            lists[max], lists[i] = lists[i], lists[max]
            adjust_heap(lists, max, size)
 
def build_heap(lists, size):
    for i in range(0, (size/2))[::-1]:
        adjust_heap(lists, i, size)
 
def heap_sort(lists):
    size = len(lists)
    build_heap(lists, size)
    for i in range(0, size)[::-1]:
        lists[0], lists[i] = lists[i], lists[0]
        adjust_heap(lists, 0, i)


# （8）基数排序（桶排）
# 工作原理：基数排序（radix sort）属于“分配式排序”（distribution sort），又称“桶子法”（bucket sort）或bin sort，顾名思义，它是透过键值的部份资讯，将要排序的元素分配至某些“桶”中，藉以达到排序的作用，基数排序法是属于稳定性的排序，其时间复杂度为O (nlog(r)m)，其中r为所采取的基数，而m为堆数，在某些时候，基数排序法的效率高于其它的稳定性排序法。

import math
def radix_sort(lists, radix=10):
    k = int(math.ceil(math.log(max(lists), radix)))
    bucket = [[] for i in range(radix)]
    for i in range(1, k+1):
        for j in lists:
            bucket[j/(radix**(i-1)) % (radix**i)].append(j)
        del lists[:]
        for z in bucket:
            lists += z
            del z[:]
    return lists
```

## 14 费波拉契数列的python实现

*【题目】* 斐波那契数列（Fibonacci sequence），又称黄金分割数列、因数学家列昂纳多·斐波那契（Leonardoda Fibonacci）以兔子繁殖为例子而引入，故又称为“兔子数列”，指的是这样一个数列：1、1、2、3、5、8、13、21、34、……
基于python用多种方式，生成费波拉契数列。

**解答**
```python
# （1）递归法 返回 idx 位的数值，缺点：只能返回某个值
def fib_recursion(idx):
    if idx <= 2:
        return 1
    else:
        return fib_recursion(idx-1) + fib_recursion(idx-2)

# （2）迭代法 返回 idx 位之前的fib数列
def fib_iteration(idx):
    re_list = []
    n,a,b = 0,0,1
    while n < idx:
        res_list.append(b)
        a,b = b, a+b
        n += 1
    return res_list

# （3）生成器法 
def fib_generator(idx):
    n,a,b = 0,0,1
    while n < idx:
        yield b
        a,b = b, a+b
        n += 1

fib_obj = fib_generator(5)
for i in fib_obj:
    print(i)

```

## 15 python的字典合并

**参考** [python字典合并](https://blog.csdn.net/jerry_1126/article/details/73017270)

主要思路：
- 借助dict(list(d1.items()) + list(d2.items())的方法,注意：list(d1.items()) + list(d2.items())拼成一个新的**列表**
- 借助字典的update()方法：d1.update(d2)
- 借助字典的dict(d1, **d2)方法
- 借助字典的常规处理方法（采用迭代的方式）

## 16 python的socket编程

**解答**

服务端要做的工作：
- 创建socket
- 绑定端口
- 监听端口
- 接收消息
- 发送消息

服务端要做的工作：
- 创建socket
- 连接socket
- 发送消息
- 接收消息

```python

# 客户端
import socket
client = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
client.connect(('127.0.0.1', 8000))
while True:
    re_data = input()
    client.send(re_data.encode("utf8"))
    data = client.recv(1024)
    print(data.decode("utf8"))


# 服务端
import socket
import threading

server = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
server.bind(('0.0.0.0', 8000))
server.listen()


def handle_sock(sock, addr):
    while True:
        data = sock.recv(1024)
        print(data.decode("utf8"))
        re_data = input()
        sock.send(re_data.encode("utf8"))

#获取从客户端发送的数据
#一次获取1k的数据
while True:
    sock, addr = server.accept()

    #用线程去处理新接收的连接(用户)
    client_thread = threading.Thread(target=handle_sock, args=(sock, addr))
    client_thread.start()

```

## 17 【程序设计】在有序列表里面，查找某个值的位置

*【题目】* 设计一个程序（函数），已知一个值（n = 5）和一个有序列表（L = [1,2,3,4,5,6]），求一个值在在这个有序列表中的位置。并对这个程序进行测试用例的设计。

**解答**



## 18 【程序设计】判断一个字符串中的“括号”是不是成对出现的

*【题目】* 给出字符串 s = "12312{}{111{222}}{{[22]}}"，判断字符串s中的 括号 是不是成对出现的

**解答**

```python

s = "12312{}{111{222}}{{[22]}}"

def judge_brackets(target_str):
    left_list = []
    right_list = []
    for i in target_str:
        if i == '{' or i == '(' or i == '[':
            left_list.append(i)
        if (i == '}' or i == ')' or i == ']'):
            if left_list != []:
                left_list.pop()
            else:
                right_list.append(i)

    if left_list != [] or right_list != []:
        return "括号不是成对出现的"

    return "括号是成对出现的"


p = judge_brackets(s)
print(p)

# 结果：括号是成对出现的
```


## 19 【程序设计】修改某个文本文件中的某个字符串

*【题目】* 文本文件 English.txt 打开如下所示：

>  Paypal is a great site and is used by many to send and receive money. Unfortunately some dishonest people are using the Popularity of Paypal to line their own pockets with gold at the expense of unsuspecting Pay Pal members. These paypal Scam Artists will try to get your Paypal ID and password so they can Login then Clean out your Paypal Account of all funds. Paypal is fully aware of this problem and is doing everything possible to stop this. Unfortunately if someone logs into an account with a valid Id and Password it is very **hard** for Paypal or any other secure site for that matter to stop it. As a Consumer you need to be educated so you can protect yourself.

用任意方式，把 **hard** 替换成 **soft**

**解答**

用 Linux sed 命令

```bash

sed -i "s/hard/soft/g" English.txt

```

用python的方式去解

```python

name = os.path.join(path,'English.txt')

def update_txt(file, old_str, new_str):
    file_data = ''
    with open(file, "r", encoding='utf-8') as f:
        for line in f:
            if old_str in line:
                line = line.replace(old_str, new_str)
            file_data += line
    with open(file,"w",encoding="utf-8") as f:
        f.write(file_data)

update_txt(name,'hard','soft')

```

## 20 python的赋值、浅拷贝和深拷贝的区别

**解答**

**赋值** 只是复制了新对象的引用，不会开辟新的内存空间。详细请看例子：

```python
# 不可变对象
a = "abcde"
b = a 
print(id(a), id(b))
# 结果： 2274644971848 2274644971848 两个变量的id是一致的
a = "xyz"
print((id(a), id(b)), (a, b))
# 结果：(1970541080680, 1970540237128) ('xyz', 'abcde')，因为字符串是不可变对象，改变之后要开辟新的内存空间，相当于创建了新的内存区块，并且a引用了新的内存区块，所以id这时候就不相等了。

# 可变对象
a = [1,2,3,4,5]
b = a
print(id(a), id(b))
# 结果：1861111211144 1861111211144
c.append(6)
print((id(a), id(b)), (a, b))
# 结果：(1861111211144, 1861111211144) ([1, 2, 3, 4, 5, 6], [1, 2, 3, 4, 5, 6])，因为列表是可变对象，添加元素之后，并不会开辟新的内存区块，所以这时候两个变量仍然还是指向同一区块，id是相等的
```

**浅拷贝** 创建一个新的组合对象(所以id会不同)，这个新对象与原对象共享内存中的子对象。能够拷贝所有元素的引用，但不拷贝元素的对象。详细看例子：

```python
import copy

a = "abcde"
b = copy.copy(a)
print((id(a), id(b)), (a, b))
# 结果：(1911642247496, 1911642247496) ('abcde', 'abcde')，这里有一个十分重要的点，int、string等不可变对象，假如值特别小的话，python内部有一个优化机制，让其不会开辟新的内存空间，所以这种浅拷贝，id是相等的

a = [1,2,3,4,5]
b = copy.copy(a)
print((id(a), id(b)), (a, b))
# 结果：(2005329935816, 2005329935752) ([1, 2, 3, 4, 5], [1, 2, 3, 4, 5])，不可变对象的浅拷贝，拷贝了所有元素的引用，id是不相同的
a.append(6)
print((id(a), id(b)), (a, b))
# 结果：(2687650790856, 2687650790792) ([1, 2, 3, 4, 5, 6], [1, 2, 3, 4, 5])，因为 int 也是不可变对象，进行浅拷贝之后，新增元素也会开辟新的内存空间，所以两个变量的值和id都是不同的。

a = [1,2,3,4,[5,6,7]]
b = copy.copy(a)
print((id(a), id(b)), (a, b))
# 结果：(2773194341768, 2773194763784) ([1, 2, 3, 4, [5, 6, 7]], [1, 2, 3, 4, [5, 6, 7]])
a[4].append(8)
print((id(a), id(b)), (a, b))
# 结果：(2015617514888, 2015617937032) ([1, 2, 3, 4, [5, 6, 7, 8]], [1, 2, 3, 4, [5, 6, 7, 8]])，拷贝到元素的引用，a[4]指向一个数组(不可变对象)，当这个元素的值改变时，没有开辟新的内存空间，所以这个元素还是指向同一个内存区块。
```

**浅拷贝** 创建一个新的组合对象，同时递归地拷贝所有子对象，新的组合对象与原对象没有任何关联。虽然实际上会共享不可变的子对象，但不影响它们的相互独立性。看例子：

```python
import copy


a = "abcde"
b = copy.deepcopy(a)
print((id(a), id(b)), (a, b))
# 结果：(1684255592776, 1684255592776) ('abcde', 'abcde')，和浅拷贝一样

a = [1,2,3,4,5]
b = copy.deepcopy(a)
print((id(a), id(b)), (a, b))
# 结果：(1684258061768, 1684258061704) ([1, 2, 3, 4, 5], [1, 2, 3, 4, 5])，和浅拷贝差不多
a.append(6)
print((id(a), id(b)), (a, b))
# 结果：(1684258061768, 1684258061704) ([1, 2, 3, 4, 5, 6], [1, 2, 3, 4, 5])，和浅拷贝差不多

a = [1,2,3,4,[5,6,7]]
b = copy.deepcopy(a)
print((id(a), id(b)), (a, b))
# 结果：(1684258485064, 1684258061768) ([1, 2, 3, 4, [5, 6, 7]], [1, 2, 3, 4, [5, 6, 7]])
a[4].append(8)
print((id(a), id(b)), (a, b))
# 结果：(1684258485064, 1684258061768) ([1, 2, 3, 4, [5, 6, 7, 8]], [1, 2, 3, 4, [5, 6, 7]])，因为递归拷贝了子对象，所以这个例子可以看出和浅拷贝的区别所在，因为深拷贝递归的把元素的子元素也拷贝了一份，所以新的组合对象和原组合对象实际上看起来是不再有关联的
```

## 21 【程序设计】返回字符串中第一个不重复的字母和位置

**解答**

```python

def first_char(str):
    d = {}
    for i in range(len(str)):
        # 累计字符的出现次数
        if str[i] in d:
            d[str[i]] += 1
        # 只出现一次，key对应的value就记1次
        else:
            d[str[i]] = 1
    for i in range(len(str)):
        if d[str[i]] == 1:
            return '第一个不重复的字符串是{},索引是{}'.format(str[i], i)

    return "没有不重复的字符串"


if __name__ == '__main__':
    s = "wwqqoogg"
    res = first_char(s)
    print(res)

```

## 22 【程序设计】求一个数字列表里，相邻两数乘积最高的值，及这两个数分别是多少?

*【题目】* 给出L = [2, 4, 6, 3, 9, 11, -12] , 求相邻两数乘积最大的值，并返回这两个相乘的数。

**解答**

```python

L = [2, 4, 6, 3, 9, 4, -12]

def multi_max(lis):
    L1 = []
    for i in range(1, len(lis)):
        j = i - 1
        multi = lis[i] * lis[j]
        L1.append((multi, lis[i], lis[j]))
        # max函数是取第一个元素做比较，也就是说按multi最大来排
    return max(L1)

multi, left, right = multi_max(L)
print(multi, left, right)

```




