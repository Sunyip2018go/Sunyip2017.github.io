---
title: pjax入门
date: 2017-03-16 10:46:41
tags: pjax
categories: pjax
description:
---
pushState + ajax = pjax,无刷新页面更改页面内容。
<!-- more -->
<The rest of comments | 余下全文>

Pjax的实现原理就是通过点击链接，利用ajax来更新页面需要改变的内容,然后使用HTML5的pushState修改浏览器的URL地址，这样就避免了整个页面的加载，用户体验性好,并且ajax向后台请求的是HTML文件。

接下来通过实例来体验一下：

首先下载pjax文件,这里有个坑，关于pjax网上的教程真的非常多,有两个版本的pjax,用法有点区别,很容易就弄乱了，这里我推荐这个<https://github.com/welefen/pjax>,是国人对pjax的升级版本。
   
首先我们创建一个HTMl文件，引入pjax文件，pjax文件依赖jQuery，记得先引入jQuery。
  
    <div id="box">
           <header>这是头部</header>
            <ul>
                 <li><a href="a1.html" title="index">首页</a></li>
                 <li><a href="a2.html" title="charts">图表</a></li>
                 <li><a href="a3.html" title="table">表格</a></li>
                 <li><a href="a4.html" title="wenzhang">文章</a></li>
             </ul>
            <div id="pjax-container">
                这是首页
            </div>
    </div>
    <script src="http://cdn.bootcss.com/jquery/2.0.0/jquery.min.js"></script>
    <script src="jquery.pjax.js"></script>

在这里我们定义一个id为pjax-container的div作为我们的容器,点击链接后更改的内容就在这个里面显示.
接下来我们编写js部分:
   
    <script>
           $(function(){  
                $.pjax({
                    selector: 'a',//绑定pjax的标签
                    container: '#pjax-container', //内容替换的容器
                    timeout:8000,//超过8秒正常加载
                    show: 'fade',  //展现的动画，支持默认和fade, 可以自定义动画方式，这里为自定义的function即可。
                    cache: false,  //是否使用缓存
                    storage: true,  //是否使用本地存储
                    titleSuffix: '/', //标题后缀
                    filter: function(){},
                    callback: function(){}
                }) 
           })
    </script>

接下来我们编写其余的HTML文件，这些跳转的HTML文件只需要写要展示的内容,不需要写html、head、body等标签,举个例子,a2.html里面的内容是：
  
    <div>这是图表页</div>

 接下来我们运行一下，pjax需要在服务器环境下运行，本地打开没有效果：
 
{% qnimg pjax.gif title:pjax 'class:' %}

当我们点击a标签的时候，页面并没有刷新，右侧中间的内容也替换了，这就是我们想要的。
这里啰嗦一下，说一个小技巧:
    
    <style>
        *{margin:0;padding:0;}
        html,body{width: 100%;height: 100%;}
        /*父容器*/
        #box{overflow: hidden;width: 100%;height: 100%;}
        /*头部*/
        header{font-size:10px;height:80px;text-align:center;line-height:8;background:#ccc;}
        /*右侧高度设置*/
        #pjax-container{min-height:calc(100% - 50px); height: auto !important;}
        /*左侧*/
        ul{margin-bottom:-1000px;padding-bottom:1000px;list-style: none;float:left;background:#ccc}
        li{padding:30px 30px}
        /*右侧*/
        #pjax-container{text-align:center;margin-left:100px;margin-bottom:-1000px;padding-bottom:1000px;height:140px;line-height: 10}
    </style>

左侧和右侧都设置了padding-bottom和margin-bottom，两者一正一负相互抵消，父级设置了overflow：hidden，然后设置右侧的高度,然后左侧的高度就和右边保持一致了，这种方式应用于多栏布局很好用。
   
