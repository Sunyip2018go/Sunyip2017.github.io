---
title: sass入门
date: 2017-02-28 16:36:13
tags: sass
categories: sass
description:
---
成熟、稳定、强大的 CSS 扩展语言解析器
<!-- more -->
<The rest of comments | 余下全文>

### 1、sass安装
 sass依赖ruby，所以先安装ruby，以window为例，进入下载页面<https://rubyinstaller.org/>,下载BubyInstaller,安装的时候记得将Ruby安装在系统的环境变量中：
 
 {% qnimg ruby_az.png title:ruby安装 'class'%}
 
 安装完成后：
 
 {% qnimg ruby_azh.png title:运行ruby 'class'%}
 
 在启动的Ruby命令控制面板中输入下面的命令：
 ```
 gem -v 查看Ruby版本
 ```
```
 $ gem install sass  安装sass
```
{% qnimg sass_az.png title:sass安装 'class'%}

检测sass是否安装成功，输入：
```
 $ sass -v
```

检测sass是否有更新,输入：
```
 $ gem update sass
```
卸载sass,运行：
```
 $ gem uninstall sass 
```