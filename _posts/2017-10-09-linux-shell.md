---
layout: post
title: "Linux Shell"
author: "Dzreal"
categories: linux
tags: [linux]
image: shell.jpg
---

# Shell 编程相关

## 变量

### 变量分类
* **用户自定义变量** 定义不用加$符，调用需要加$符
* **环境变量** 保存和系统操作环境相关的数据，一般是大写表示
* **位置参数变量**（其实是预定义变量的一类）
    * $0 命令本身
    * $1 第一个参数
    * $2 第二个参数
    * $# 命令行传入的所有参数个数
    * $@ 命令行传入的所有参数（假如用for循环打印，每个参数区分对待）
    * $* 命令行传入的所有参数（假如用for循环打印，把所有参数当成一个整体）
* **预定义变量** Bash中已经定义好的变量
    * $? 上一条命令的执行 状态返回值
    * $$ 当前进程的pid号
    * $！后台运行的最后一个进程的pid号  

### 变量详解
**用户自定义变量**（局部变量，只能在当前shell生效）
```bash
y=6    # 变量定义：变量和值之间的等号两边 不能 加空格！！
echo $y     # 变量调用：变量调用要加$符

a=7
b=8
z=$a+$b     # 变量相加，因为变量默认都是字符串类型，所以直接相加不会做数值运算！！
echo $z     # 结果：7+8
y=$(( $a + $b )) # 变量数值运算
echo $y     # 结果：15

x=123
x="$x"456   # 变量叠加：推荐用这种格式写，用下面的格式有可能会多写$
x=${x}456

unset x     # 变量删除
```

**环境变量**（全局变量，能在当前shell和子shell生效）

常用环境变量（调用也要加$符）
* HOSTNAME 主机名
* SHELL 当前的shell
* TERM 终端环境
* HISTSIZE 历史命令条数
* SSH_CLIENT 当前操作环境是用ssh连接的，记录客户端IP
* USER 当前登录的用户

```bash
# 设置环境变量
export x=5
# 或
x=5
export x

# 添加path环境变量
PATH="PATH":/dirname/   # 这样添加只是临时生效，假如机器重启则失效

# PS1环境变量（命令提示符设置）
# \d : 显示日期，格式为"星期 月 日"
# \H ：显示完整的主机名
# \t ；显示24小时制时间，格式："HH:MM:SS"
# \A ：显示24小时制时间，格式："HH:MM"
# \u ：显示当前用户名
# \w ：显示当前所在目录的完整名称
# \W ：显示当前所在目录的最后一个目录
# \$ ：提示符，root用户显示"#",普通用户显示"$"
# 示例：
PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '     # 命令提示符（注意：最后一个'前面有一个 空格！！）
PS2='> '                                                # 命令换行提示符
PS4='+ '

# 查询当前语系
locale
locale -a # 查询系统支持的语系
cat /etc/sysconfig/i18n # 查询系统默认语系的文件

```

**位置参数变量**
```bash
# "$@" 和 "$*" 的区别

#! /bin/bash

for i in 1 2 3 4
    do
        echo $i 
    done

echo -e "\n"        # 输出换行符需要加 -e

for i in "$@"
    do
        echo $i 
    done

echo -e "\n"

for i in "$*"
    do
        echo $i 
    done

# 结果：
# 1     # echo i
# 2
# 3
# 4

# 5     # echo "$@"
# 6
# 7
# 8

# 5 6 7 8       # echo "$*" 
```

**如何写出让他人易用的shell脚本？** （read 的用法）
```bash
#! /bin/bash

read -p "请输入用户名：" -t 30 name  # -p 输入提示 -t 输入限制时间
echo -e "\n"
echo $name

read -p "请输入密码：" -s passwd  # -s 保密输入
echo -e "\n"
echo $passwd

read -p "请确认是否提交 [Y/N]" -n 1 charge
echo -e "\n"
echo $charge
```

### 运算符

#### declare命令

**用法**

declare [+/-] [options] 变量名

* -：给变量设定类型属性
* +：取消变量的类型属性
* -a: 将变量声明成数组型
* -i：将变量声明成整型（最常用）
* -x：将变量声明成环境变量
* -r：将变量声明成只读变量
* -p：显示指定变量的被声明的类型

**例子**
```bash
# 定义整型
a=1
b=2
declare -i c=$a+$b
echo $c

# 定义数组：
arr[0]=1
arr[1]=2
declare -a arr[2]=3

# 调用数组：
echo ${arr}     # 打印数组的第一个元素值
echo ${arr[0]}  # 打印下标为0的元素值
echo $arr[1]    # 打印arr和[1] 结果是：1[1] 注意：打印数组必须要加{}，一定要写成${arr[n]}的形式
echo ${arr[*]}  # 打印数组的所有元素

# 定义环境变量
declare -x c=111
# 等价与
export c=111

# 查询所有变量的属性
declare -p

# 查询指定变量的属性
declare -p 变量名

```
#### 数值运算
1. 使用"declare"进行数值运算
2. "expr"或"let"数值运算工具
3. "$(( 运算式 ))" 或 "$[运算式]"

**例子**


## 正则用法

## 条件判断

## 循环

## 函数