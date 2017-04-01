---
title: 为Hexo编写分类页面
date: 2017-03-08 16:52:46
tags: Hexo
categories: Hexo
description:
---

我用的Hexo主题next默认是没有分类页面的...
<!-- more -->
<The rest of comments | 余下全文>

**1.创建分类页面**

打开 **git Bash**,编写Hexo博客必须使用它,进入博客根目录,运行

 ```
 hexo new page categories
 ```
 会在**source**目录下生成**categories**文件夹,打开里面的**index.md**文件,
    
     ---
    title: 分类
    date: 2017-03-08 16:37:45
    type: "categories"
     ---
     
只要添加**type: "categories"**就可以

这里得说一下,要使用分类选项必须编辑主题的**_config.yml**文件,将 menu 中的 categories: /categories 注释去掉，如下:
   
    menu:
      home: /
      categories: /categories
      #about: /about
      archives: /archives
      tags: /tags
      #sitemap: /sitemap.xml
      #commonweal: /404.html

