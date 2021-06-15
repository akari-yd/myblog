---
title: linux
date: 2021-05-24 23:51:44
tags:
- linux
category:
- linux
---

# npm
## 更新包
安装npm-check 检查npm是否有更新
` npm install -g npm-check `
检查npm包状态
` npm-check -u -g `
点击空格后可选择要更新的包，然后点击回车即可更新

# screen--服务器后台持续运行程序
原文链接[https://blog.csdn.net/qq_37764129/article/details/103062548]
screen原理是在后台挂起一个程序执行，在断开服务器连接后后台程序依然可以继续执行。

## 安装screen
直接使用指令安装
```
yum install screen#centos
apt-get install screen#ubuntu
```

## 相关指令
1. 创建窗口：` screen -S name `
2. 分离窗口（窗口放到后台） ctrl+a+d
3. 查看所有会话： ` screen ls `
4. 进入会话： ` screen -r name`
5. 杀死会话： ` kill -9 name` 
6. 清楚死去的窗口： ` screen -wipe `
7. 完全退出会话： `exit`

# tar的使用方法
