---
title: vue中使用sass
date: 2017-03-21 16:06:35
tags: vue sass
categories: vue sass
description:
---
最近正在用Vue2.0+elementUI写一个后台管理系统，css部分打算用sass来写，就上网查了一下，配置成功，写一下心得。
<!-- more -->
<The rest of comments | 余下全文>

**项目目录安装sass依赖**

进入你的项目目录运行

 ```
 npm install sass-loader css-loader style-loader --save-dev
 ```
 我安装的时候报错node-sass版本的问题,那我们需要重新安装node-sass模块
 
```
npm install node-sass@latest
```

成功后我们修改webpack文件,我的项目使用vue-cli脚手架,所以修改的是webpack.base.conf.js文件,在 module中添加这行代码：

      {
         test: /\.scss$/,
         loader:'style!css!sass'
      }

接下来将我们的vue文件中的style标签修改为：

    <style lang="scss" scoped>
    </style>
    
    
参考： _韩小妖 vue.js 使用sass <http://www.jianshu.com/p/92dbc92e775d>
