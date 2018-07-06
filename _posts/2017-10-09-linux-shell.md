---
layout: post
title: "Linux Shell"
author: "Dzreal"
categories: linux
tags: [linux]
image: shell.jpg
---

# Linux 常用命令一览

（
    tips:本文只会提到作者日常工作中运用到的命令，假如没有使用过，不确定用途的，不会记录在此~
    东西比较多比较杂，可以用 Ctrl+F 查询一下有没有相关命令，若没有的话，陆续会补充。 
）



### 查看目录下的文件
```
ls                      # 列举查看当前目录下的文件（不包括隐藏文件）
ls -a                   # 列举出所有文件（包括隐藏文件）
ls -l                   # 列举出所有文件，以详细列表的形式输出
ls dir/                 # 列举某个目录下的文件

```

### 查看当前目录

```
pwd                     

```

### 切换目录
```
cd dir/                 # 切换到目标目录下
cd ..                   # 切换到上级目录
cd -                    # 切换到history上一个目录
cd                      # 切换到 /home/xxx/ 切换到当前权限下的用户目录下
cd ~                    # 切换到 /home/xxx/ 切换到当前权限下的用户目录下
```

### 删除
```
rm                      # 删除文件（不可删除目录）
rm -r                   # 递归删除文件（可删除目录）
rm -rf                  # 递归删除并忽略提示
```

### 移动/重命名
```
mv oldFile newFile      # 重命名文件
mv file dir/            # 移动文件
```

### 用户权限相关
```
useradd user            # 创建用户
useradd -g user         # 指定用户所在用户组
useradd -d /home/user user  # 创建用户，并为用户生成用户目录（高频用法）
userdel user            # 删除用户
userdel -r user         # 删除用户，并删除用户目录
passwd user             # 创建用户密码
passwd -d user          # 删除用户密码

groupadd group          # 创建用户组

# 让普通用户拥有root权限的操作步骤：
1.root登录
2.adduser user
3.passwd  user
4.修改/etc/passwd即可，把用户名的ID和ID组修改成0。

chmod 777 file（dir/）   # 把该文件或目录的权限设为全部用户可读可写可执行

# 文件权限扫盲
-rw-r--r--              # 可以拆分成 - rw- r-- r--  
                        # 第一个"-"代表文件类型，若是"-"，则是文件;若是"d"，则是目录
                        # 第一组"rw-",代表文件所属用户的权限,该用户具有对文件的读写权限，没有执行权限
                        # 第二组"r--",代表文件所属组的权限，该组的用户可以读，但是不能写和执行
                        # 第三组"r--",代表其他用户的权限，其他用户可以读，但是不能写和执行
                        # r=读取属性　值＝4
                        # w=写入属性　值＝2
                        # x=执行属性　值＝1

chown group:user file       # 将文件的所属用户改为user，所属组改为group
chown -R group:user dir/    # 将dir/目录下的所有文件，所属用户改为user，所属组改为group    

chgrp -R group dir/     # 将dir目录下的所有文件的用户组改为group，-R是递归处理

```
### 创建文件
```               
touch file              # 创建空文件
vim file                # 创建文件并进行编辑
vi file                 # 创建文件并进行编辑（同vim）
echo "xxx" > file       # 创建文件并插入字符串
echo "yyy" >> file      # 创建文件并追加字符串
```

### 创建目录
```
mkdir dir/              # 创建目录
rmdir dir/              # 删除空目录
```

### 复制文件
```
cp srcFile newFile      # 复制文件，并命名新文件
cp srcFile dir/         # 复制文件到目标目录下
scp user@ip:file dir/   # 将远程机器的文件，复制到本机某个位置
scp -r user@ip:dir/ dir/ # 将远程机器的目录，复制到本机某个位置

# 软链接（有点像windows的快捷方式）
1.保存了其代表的文件的绝对路径，是另外一种文件，在硬盘上有独立的区块，访问时替换自身路径。
2.删除了源文件之后，打开软链接文件会报错
3.修改软链接文件，源文件也会修改

ln -s srcFile softFile  # 创建软链接

# 硬链接
1.与普通文件没什么不同，inode 都指向同一个文件在硬盘中的区块
2.删除了源文件之后，打开硬链接的文件不会报错
3.修改硬链接文件，源文件也会修改

ln srcFile hardFile     # 创建硬链接
```
附录：
1. [硬链接和软连接的区别](https://blog.csdn.net/bobyuan888/article/details/78874913)

### 查看/编辑文件
```
cat  file               # 显示文件内容

more file               # 分页显示文件内容
    Enter               # 向下n行，需要定义。默认为1行
    Ctrl+F              # 向下滚动一屏
    空格键               # 向下滚动一屏
    Ctrl+B              # 返回上一屏
    =                   # 输出当前行的行号
    :f                  # 输出文件名和当前行的行号
    V                   # 调用vi编辑器
    !命令               # 调用Shell，并执行命令 
    q                   # 退出more

less file               # 分页显示文件内容（ less 比 more 更强大方便，且 less 在查看之前不会加载整个文件。）
    -i                  # 忽略搜索时的大小写
    -m                  # 显示类似more命令的百分比
    -N                  # 显示每行的行号
    /字符串              # 向下搜索“字符串”的功能
    ?字符串              # 向上搜索“字符串”的功能
    n                   # 重复前一个搜索（与 / 或 ? 有关，需要配合 / 或 ? 使用）
    N                   # 反向重复前一个搜索（与 / 或 ? 有关，需要配合 / 或 ? 使用）
    f                   # 向后翻一页
    d                   # 向后翻半页
    b                   # 向前翻一页
    u                   # 向前滚动半页
    y                   # 向前滚动一行
    空格键               # 滚动一页    （和more相同）
    回车键               #  滚动一行   （和more相同）
    [pagedown]          # 向下翻动一页
    [pageup]            # 向上翻动一页
    Q                   # 退出less 命令

vim file                # 编辑文件或查看文件
    -O                  # 分屏显示2个文件的内容（竖屏显示）
    -o                  # 分屏显示2个文件的内容（横屏显示）

    :set nu             # 显示行号
    :set nonu           # 不显示行号
    :q                  # 退出（若文件有编辑改动，退出时会有询问）
    :q!                 # 不保存退出
    :w                  # 保存
    :x                  # 保存并退出（假如文件被修改，才变更文件修改时间）
    :wq                 # 保存并退出，并变更文件修改时间（不论文件是否真的有更改）
    :wqa                # 全部保存并退出（用于同时打开查看多个文件）
    :qa!                # 全部不保存并退出
    :行号               # 跳转到相应行
    :s/srcStr/newStr    # 将 当前行 的 第一个 srcStr用newStr替换
    :s/srcStr/newStr/g  # 将 当前行 的 全部 srcStr用newStr替换
    :s#srcStr#newStr    # 用 # 其实和 / 一样，都是用来分割，但是用#的话，字符串里如果有 / ， / 不会作为分隔符
    :%s/srcStr/newStr   # 全文的srcStr用newStr替换

    a                   # 光标移动到下一个字符处，并进入编辑模式
    i                   # 光标不移动，并进入编辑模式
    o                   # 在本行下面另起一行，光标移动到下一行的开头，并进入编辑模式
    ngg                 # 跳到n行
    dd                  # 删除1行
    ndd                 # 删除n行
    yy                  # 复制1行
    nyy                 # 复制n行
    p                   # 粘贴
    u                   # 撤销
    [pagedown]          # 向下翻动一页
    [pageup]            # 向上翻动一页
    
tail file               # 显示文件最后10行
    -n                  # 显示文件最后n行
    -f                  # 动态显示文件末尾

head file               # 显示文件开头10行（查看日志用得最多）
    -n                  # 显示文件开头n行

# 常考面试题：
    # （1）查看文件的 300-399 行
    sed -n '300, 500p' file

```

### 查找
```
find                    # 查找文件
    find dir/ -name file     # 根据文件名查找文件，文件名可使用正则表达式
    find dir/ -user username # 根据用户名查找文件，查找一个目录下该用户权限的文件
    find dir/ -size +100M    # 根据文件大小查找文件，（数据块数，通常一块等于512）

locate                  # 定位文件
    locate file         # 根据数据库记录查找，有时候新创建的文件查找不到，有些Linux发行版不支持

which                   # 查找 命令 的执行者(就是说谁能够执行这个命令)
    which command       # 显示的结果如果是bin，则表示所有用户都可以执行，若是sbin，则表示root用户才能执行该命令

whereis                 # 除了可以查找 命令 的绝对路径，还可以显示别名记录

grep                    # 超级强大的查找（过滤）工具
    grep str file       # 查找文件下的str字符串
    grep -rn str dir/   # 查看某个目录下的所有包含str的行，并显示行号（使用频率超高）
    tail -f log | grep str      # 常用 tail 配合 grep ，用于动态查看log时，滤出关键信息，只显示匹配str的行
    tail -f log | grep -v str   # 不显示str的行
    tail -f log | grep str1 | grep str2     # 同时满足 str1 和 str2 才显示出来
    tail -f log | grep -E "str1|str2"       # 满足 str1 或 str2 都会显示出来
    tail -f log | grep str --color          # 搜出结果的同时高亮字符串
    grep -o 'str' file | wc -l              # 查询字符串在文件中出现的次数
```

### 查看系统相关的信息
```
# 打印当前系统相关信息
uname -a                # 全部输出

# 查看Linux内核版本
cat /proc/version

# 查看Linux版本
lsb_release -a

# 查看进程管理
top                     # 类似windows的资源管理器，可以查看cpu、内存的占用情况
htop                    # 比top要高级好用，但可能需要安装
ps -ef | grep process   # 查看进程的使用情况（非常高频）

# 查看网络相关
ifconfig                # 查看网口配置
netstat -ntpl | grep 端口号  # 查看端口占用情况
hostname -i             # 查看本机ip地址
cat /etc/resolv.conf    # 查看本机dns服务器配置
ping ip(domain)         # 查看网络是否ping通，或也可以通过域名查询ip
telnet ip port          # 查看tcp服务是否通

# 查看cpu/内存/硬盘空间占用
ps auxw|head -1;ps auxw|sort -rn -k3|head -10   # CPU占用最多的前10个进程：  
ps auxw|head -1;ps auxw|sort -rn -k4|head -10   # 内存消耗最多的前10个进程
ps auxw|head -1;ps auxw|sort -rn -k5|head -10   # 虚拟内存使用最多的前10个进程
dstat -g -l -m -s --top-mem     # 动态查看当前占用内存最高的进程
dstat -g -l -m -s --top-cpu     # 动态查看当前占用cpu最高的进程
dstat -g -l -m -s --top-io      # 动态查看当前占用io最高的进程
df -lh                          # 磁盘空间使用率
du -sh                          # 一个目录下的所有文件大小
```
附：
1. [htop相关用法解读](https://www.cnblogs.com/lazyfang/p/7650010.html)
2. [dstat相关用法解读](https://linux.cn/article-3215-1.html)


### 别名的使用
```
# 修改别名
vim ~/.bashrc       # 修改.bashrc文件
    alias keymap = 'command'
    alias grep='grep --color=auto'
    alias ls='ls -a'
sourse ~/.bashrc    # 即时生效
```

### [vim用法详解]()
### [awk用法详解]()
### [sed用法详解]()
### [xarg用法详解]()
### [shell编程语法]()