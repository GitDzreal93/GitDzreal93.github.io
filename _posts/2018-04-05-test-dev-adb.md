---
layout: post
title: "Test-Dev adb"
author: "Dzreal"
categories: test-dev
tags: [test-dev]
image: adb-cmd.jpg
---

# 常用 adb 命令


## 优秀文档
    * [adb 命令大全](https://blog.csdn.net/u010375364/article/details/52344120)
    * [adb 安装及命令详解](https://blog.csdn.net/shirakawakanaki/article/details/53432293)


## 工作中用到的 adb 命令
```bash
1 adb -s <serialNum> command     # 指定相应的seriaNum号的设备去执行adb 命令

2 adb devices   # 获取设备连接状态，（1）devices 连接上 （2）offline 未连接成功或无响应 （3）no device 没有设备/模拟器连接

3 adb start-server  # 启动 adb 服务

4 adb kill-server   # 停止 adb 服务

5 adb version   # 查看 adb 版本

6 adb shell     # 进入 adb 命令行

7 adb tcpip 5555    # 启动无线 adb 服务

8 adb connect <device-ip-address>   # 通过 ip地址 连接设备

9 adb install xxx.apk   # 安装安卓app

10 adb install -r xxx.apk   # 覆盖安装安卓app

11 adb uninstall [-k] <packagename> # 卸载应用，-k表示保留数据和缓存 

12 adb logcat | grep xxx    # 查看安卓端上日志

13 adb logcat -c    # 清空日志

14 adb shell getprop ro.product.model # 查看设备型号

15 adb shell wm size # 屏幕分辨率

16 adb shell getprop ro.build.version.release   # 获取安卓系统版本

17 adb shell ; su ; cat /data/misc/wifi/*.conf # 查看连接过的wifi密码

18 adb shell ps     # 查看进程

19 adb kill 'pid'   # 杀死进程

## pm 命令， package manerger 应用管理

1 adb shell pm list packages    # 查看所有应用程序

2 adb shell pm list packages -s     # 只显示系统应用

3 adb shell pm list packages -3     # 只显示第三方应用

4 adb shell pm list packages | grep xxx     # 查看包名包含某字符串的应用

5 adb shell pm clear <packagename>  # 清除应用数据和缓存

6 adb reboot    # 重启手机

7 adb shell ; su    # 查看手机是否已撸特

## am 命令，activity manerger

1 adb shell dumpsys activity activities | grep mFocusedActivity     # 查看前台空间

2 adb shell am start -n com.tencent.mm/.ui.LauncherUI   # 调起一个Activity

3 adb shell am start -n org.mazhuang.boottimemeasure/.MainActivity --es "toast" "hello, world"  #调起一个 activity 并传值

4 adb shell am start "schema://"    # 调起一个schema

5 adb shell am startservice -n com.tencent.mm/.plugin.accountsync.model.AccountAuthenticatorService     # 调起 wx service

6 adb shell am force-stop <pacagename>  # 强制停止应用


## 文件管理

1 adb pull <设备里的文件路径> [电脑上的目录] # 复制文件到电脑

2 adb push <电脑上的文件路径> <设备里的目录>  # 复制文件到设备

## 按键操作

1 adb shell input keyevent 3 # 按 home 键

2 adb shell input keyevent 82 # 按 菜单 键

3 adb shell input keyevent 26 # 按 电源 键

4 adb shell input text hello # 输入文本

5 adb shell screencap -p /sdcard/sc.png # 屏幕截屏

6 adb shell screenrecord /sdcard/filename.mp4 # 屏幕录制

## monkey

1 adb shell monkey -p <packagename> -v 500  # 执行随机monkey，更多见monkey专栏

```