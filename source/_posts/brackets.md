---
title: brackets编辑器安装emment
date: 2017-03-08 11:55:46
tags: 编辑器
categories: 编辑器
description:
---
brackets编辑器默认不支持emment,需要我们手动安装
<!-- more -->
<The rest of comments | 余下全文>

** 1. 下载emmet并安装 **

首先我们需要下载最新版的emment文件,找到brackets对应的版本,地址为：<http://emmet.io/download/>,下载完成后不需要解压,打开brackets编辑器,找到**文件**下的**项目扩展器**,将下载的文件拖到对应的区域;

** 2. 下载emmet1.2.1版本 **

通过<http://download.csdn.net/detail/jhlxge/9285313>下载版本，解压，找到里面的**node_modules**文件夹,复制

**3.将emmet1.2.1中的node_modules复制到brackets中**

打开brackets,找到**帮助**下的**显示扩展目录**,点击**user**,打开里面的**brackets-emmet**文件夹将**node_modules**文件夹复制到里面就可以,重启brackets后导航栏会出现**Emmet**.

{% qnimg brackets.png title:emmet 'class:' %}

