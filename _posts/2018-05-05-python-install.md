---
layout: post
title: "Python install"
author: "Dzreal"
categories: python
tags: [python]
image: python-main.jpg
---

# python 环境安装相关
#### python的安装
##### 当前python的最新版本：
- python3 : python3.6.4
- python2 : python2.7.14

[python 下载地址](https://www.python.org/downloads/)

tips:

假如在安装过程中，没有勾选添加到path环境变量，需要手动添加path环境变量，以windows环境 && python27为例：
- python27
- python27\Lib\site-packages
- python27\Scripts

python2、python3共存问题
```bash
#用python2运行

py -2 xxx.py 
#用python3运行
py -3 xxx.py
```
---
#### easy_install安装

理论上来说好像安装了python都会自动去安装easy_indstall,假如没有的话，需要手动安装。

[easy_install 下载地址](https://pypi.python.org/pypi/ez_setup)

tips:
- 下载 ez_setup.py 到桌面后，按住键盘的 shift 键，右击鼠标，选中“在此处打开命令窗口”，进入 DOS 界面，输入命令：python ez_setup.py 
- 安装一个包：
    
```bash
easy_install 包名
easy_install "包名 == 包的版本号"
```
- 升级一个包：
```
easy_install -U "包名 >= 包的版本号"
```

---
#### pip安装
理论上来说好像安装了python都会自动去安装pip,假如没有的话，需要手动安装。==前提是先安装easy_install==

[pip 下载地址](https://pypi.python.org/pypi/pip)

tips:
- 下载到桌面，解压，然后，进入存放 setup.py 的目录中，按住键盘的 shift 键，右击鼠标，选中“在此处打开命令窗口”，进入 DOS 界面，输入命令：python setup.py install ，开始安装。
- 安装一个包：
```bash
pip install 包名
pip install 包名 == 包的版本号
    
#用豆瓣源下载包（用豆瓣源下载包比较快速）
pip install -i https://pypi.doubanio.com/simple/ 
    
#python2、python3共存问题
#python2 使用pip
py -2 -m pip install xxx
#或（可能需要将 python/scripts 下的 pip 改成 pip2）
pip2 install xxx 
    
#python3 使用pip
py -3 -m pip install yyy
#或（可能需要将 python/scripts 下的 pip 改成 pip3）
pip3 install yyy

#更新pip 
python -m pip install -U pip
    
```
- 升级一个包：
```bash
#升级到最新版
pip install --upgrade 包名
    
#升级到指定版本
pip install --upgrade 包名 >= 包的版本号
```
- 删除一个包：
```bash
pip uninstall  包名
```
- 其他实用操作
```bash
#列出已安装的包：
pip freeze or pip list

#导出requirements.txt
pip freeze > <目录>/requirements.txt

requirements.txt内容格式为：
APScheduler==2.1.2
Django==1.5.4
MySQL-Connector-Python==2.0.1
MySQL-python==1.2.3
PIL==1.1.7
South==1.0.2
django-grappelli==2.6.3
django-pagination==1.0.7

```
[更多详情](https://www.cnblogs.com/xueweihan/p/4981704.html)
鸣谢！

---
#### wheel安装
有些第三方库需要用wheel才能安装
1. 安装wheel
```bash
pip install wheel
```
2. 下载 .whl 包

[wheel包下载地址](https://www.lfd.uci.edu/~gohlke/pythonlibs/)

**wheel包名字解析**

以pymongo为例：

pymongo‑3.6.0‑cp37‑cp37m‑win32.whl

pymongo‑3.6.0‑cp37‑cp37m‑win_amd64.whl

> wheel 包的命名格式为{distribution}-{version}(-{build tag})?-{python tag}-{abi tag}-{platform tag}.whl

检测版本命令：
```bash
from pip import pep425tags
print(pep425tags.get_supported())
```

执行过程：
```bash
C:\Python3.5\Scripts>python
Python 3.5.2 (v3.5.2:4def2a2901a5, Jun 25 2016, 22:01:18) [MSC v.1900 32 bit (Intel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from pip import pep425tags
>>> print(pep425tags.get_supported())
[('cp35', 'cp35m', 'win32'), ('cp35', 'none', 'win32'), ('py3', 'none', 'win32'), ('cp35', 'none', 'any'), ('cp3', 'none', 'any'), ('py35', 'none', 'any'), ('py3', 'none', 'any'), ('py34', 'none', 'any'), ('py33', 'none', 'any'), ('py32', 'none', 'any'), ('py31', 'none', 'any'), ('py30', 'none', 'any')]
```

3. 用 pip 去安装 wheel 包
```bash
pip install xxx.whl
```

---
#### Pycharm
pycharm是一款强大的python-ide工具

[pycharm 下载地址](https://www.jetbrains.com/pycharm/download/#section=mac)

> 破解方式：点击help→Register→License sever ,输入序列号（不定期会更新）：http://idea.liyang.io

---
#### anaconda

[anaconda 下载地址](https://www.anaconda.com/download/#macos)

tips：

anaconda安装第三方库：

```bash
#法1
pip3.6 install xxx conda install yyy
#法2
#打开Anaconda Prompt
pip install xxx
 ```
 
 ---
#### 关于python2、python3共存问题的其他思路：

##### python2和python3共存解决方案：

**python2路径**：C:\python27 (python 2.7)

**python3路径**：C:\Users\zybang\AppData\Local\Programs\Python\Python35

1、修改python.exe和pythonw.exe为：
```bash
python2.exe，pythonw2.exe
python3.exe，pythonw3.exe
```
2、重装pip：
```bash
python2 -m pip install --upgrade pip --force-reinstall
python3 -m pip install --upgrade pip --force-reinstall
```
Q：假如说一个环境包含python27、python35、python36、anaconda怎么解决安装第三方库？
```bash
pip2 install xxx

pip3 install xxx

pip3.6 install xxx

Anaconda ：
#法1
pip3.6 install xxx conda install yyy
#法2
#打开Anaconda Prompt
pip install xxx

```

---
### python 3大神器
- pip          包管理
- vitualenv    环境
- fabric       部署

#### virtualenv
安装：

```bash
pip install virtualenv

```
创建虚拟环境：
```bash
cd project_dir

virtualenv venv  #创建名为venv的环境（继承系统环境的第三方包）

virtualenv --no-site-packages venv
#创建名为venv的纯净环境（不附带系统环境的第三方包）

virtualenv -p /usr/bin/python2.7 venv 指定使用 python27 解释器的环境
```

激活虚拟环境：
```bash
source venv/bin/activate
#将与全局安装的python隔绝开
```

安装包：
```bash
pip install xxx
#or
pip install -r requrement.txt
```

暂停虚拟环境：
```bash
./venv/bin/deactivate
```

删除虚拟环境：
```bash
rm -rf venv   #linux下
```
windows直接删除venv目录即可


#### 高级操作 virtualenvwrapper
安装：
```bash
pip install virtualenvwrapper
pip install virtualenvwrapper-win　　#Windows使用该命令
```
安装完后的操作：
```bash
#Linux：
# virtualenvwrapper存放虚拟环境目录
export WORKON_HOME=~/Envs

# virtrualenvwrapper会安装到python的bin目录下，所以该路径是python安装目录下bin/virtualenvwrapper.sh
source /usr/local/bin/virtualenvwrapper.sh

Windows：
#创建一个系统环境变量
# WORK_HOME:E:\virtualenv
# tips：不用添加到path变量
# 这样操做之后，以后创建虚拟环境都放在E:\virtualenv
```

使用：
```bash
#创建虚拟环境
mkvirtualenv venv

#指定python版本
mkvirtualenv --python=/usr/local/python3.5.3/bin/python venv   

```
基本命令
```bash
#查看当前虚拟环境目录
workon

#切换虚拟环境
workon xxx

#退出虚拟环境
deactivate

#删除虚拟环境
rmvirtualenv venv

```

#### fabric（远程部署利器）
安装：
```bash
pip install fabric
```
使用：

[详解](http://python.jobbole.com/87241/)

[部署脚本eg](https://www.cnblogs.com/rufus-hua/p/5144210.html)


#### linux下源码安装python3.6.4
```bash
1. wget https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tgz
2. tar -zxvf Python-3.6.3.tar.gz
3. ./configure --prefix=/home/work/python3
4. make && make install 
5. vi .bashrc 
   export PATH=/home/work/python3/bin:$PATH
6. source .bashrc

   
```