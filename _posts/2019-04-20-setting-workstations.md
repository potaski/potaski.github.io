---
layout: post
title:  "Ubuntu工作环境配置"
categories: 办公用品
tags: wsl linux npm gem jekyll python
author: ZhangWei
---

* content
{:toc}

> 离职咯，电脑按规定被IT服务小哥格掉了，只能重新部署工作环境了

## 常用环境

linux桌面真的不太适合安稳办公的群体，一直以来在桌面平台都是站windows

以前只能windows+vmware配合来用，后面win10出了wsl，真香，不用维护虚拟机那一套东西了、

vscode的terminal可以支持直接打开wsl，十分方便，但是python解释器却还不能用wsl上的，碰到某些特殊库没有提示还要报错，sad

前段时间又迁移回到pycharm，马云家买了个专业版，配合wsl做远程调试，美滋滋

好了，基本就是以下几点要素

- windows10 & ubuntu18.04（wsl）
- pycharm perfessional（马云家）

## wsl开启sshd服务

只要下面几行命令

```shell
# sudo 到 root
vim /etc/ssh/sshd_config
# ListenAddress 设为 127.0.0.1
# PasswordAuthentication 设为 yes
/usr/bin/ssh-keygen -A
mkdir /var/run/sshd
/usr/sbin/sshd
```

## 修改ubuntu配色

ssh上去发现显示windows文件目录亮瞎眼（以前怎么没发觉）

```shell
dircolors -p > ~/.dircolors
vim ~/.dircolors
# 把dir的华丽花哨的取消
# STICKY_OTHER_WRITABLE 33;00 # dir that is sticky and other-writable (+t,o+w)
# OTHER_WRITABLE 33;00 # dir that is other-writable (o+w) and not sticky
```

附颜色代码参考：
 
```shell
00 — Normal (no color, no bold) 
01 — Bold    //粗体
文字颜色 
30 — Black   //黑色
31 — Red     //红色
32 — Green   //绿色
33 — Yellow  //黄色
34 — Blue    //蓝色
35 — Magenta //洋红色
36 — Cyan    //蓝绿色
37 — White   //白色
背景颜色 
40 — Black 
41 — Red 
42 — Green 
43 — Yellow 
44 — Blue 
45 — Magenta 
46 — Cyan 
47 – White
```

## ubuntu镜像切到清华源

https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/

再更新一下

```shell
sudo apt update 
```

## nodejs和npm安装

https://nodejs.org/en/download/package-manager/

```shell
sudo apt install nodejs npm
```

## ruby和jekyll安装

```shell
sudo apt install ruby ruby-dev
sudo gem install jekyll jekyll-paginate bundler
```

尝试在本地启动本项目

```shell
cd potaski.github.io
jekyll clean
jekyll b; jekyll s
```

搞定

## python安装

加个py3，并配置清华大学的源

```shell
sudo apt install python3 python3-dev python3-pip
# 执行pip3还报错的...
vim /usr/bin/pip3
# 改为
# from pip import __main__ 和
# sys.exit(__main__.main())
pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple pip -U
pip3 config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```


## 另外记录几个好用的工具

terminal工具：[cmder](https://cmder.net/)

keepass工具：[keeweb](https://keeweb.info/)  # 比keepass原版相对“潮”一点