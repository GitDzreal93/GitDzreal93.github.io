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


## 自己总结的面试题

**table of contents**

 * [Python语言特性](#python语言特性)
 * [Python编程题](#python编程题)
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





# python语言特性




# python编程题

## 1.如何去除列表中的重复元素

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

## 2.两个列表如何生成一个对应的字典

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

## 3.python如何生成随机数

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

## 4.字符串逆序和统计字符串中字母出现的次数

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
```

## 5.如何在列表，字典，集合中根据条件筛选数据？

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
all_dict = {f.name() : randint(60,100) for x in range(1,100)}
perfect_dict = {name:score for name, score in all_dict.items() if score > 90} 

# （3）集合
data = [randint(-10,10) for _ in range(10)]
s = set(data)
s1 = { x for x in s if x % 3 == 0 }
```

## 6.如何优雅地操纵tuple的索引（如何给元祖中的索引命名，提高可读性）

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

## 7.对某英文文章的单词，进行词数统计

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

## 8.字典排序
*【题目】* 将全班30名同学的成绩单进行排序(从大到小)

**解答**
```python
from faker import Faker
f = Faker(locale='zh_CN')
all_stu_dict = {f.name() : randint(0,100) for x in range(30)}

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

## 9.如何快速找到多个字典的公共键（key）

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

## 10.如何让字典保持有序

*【题目】* 创建一个字典，让其能够按数据插入的先后顺序排列

**解答**
```python

# 思路：OrderedDict 有序字典,是对字典的补充,他能记录字典的添加顺序,相当于字典和列表的组合,使用之前需要导入依赖类 import collections 

from collections import OrderedDict
d1 = OrderedDict()
d2 = dict()

# 解析：不知道是不是python3的特性，dict创建的字典和OrderedDict创建的字典,都是按插入的时间顺序去排列的,OrderedDict除了和dict类型上有些差别之外，暂时还不明白2者有什么比较大的差异性
```

## 11.猜数字游戏

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

## 12.迭代器和可迭代对象

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

## 13.八大排序算法的python实现

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
