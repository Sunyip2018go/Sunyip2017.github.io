---
title: Hexo添加多说评论
date: 2017-03-13 13:17:09
tags: Hexo
categories: Hexo
description:
---
为Hexo添加多说评论，方便交流。
<!-- more -->
<The rest of comments | 余下全文>


** 1. 注册多说 **

登录此站点<http://duoshuo.com/create-site/>,通过第三方登录,**创建站点**,特别强调一下,在填写**多说域名**时一定记住填写的内容。


** 2. 修改配置 **


在_config.yml中添加多说的配置：

    duoshuo_shortname: 你站点的short_name


然后修改主题themes\landscape\layout\_partial\article.ejs,将里面的内容替换成：
    
     <% if (!index && post.comments && config.duoshuo_shortname){ %>
          <section id="comments">
            <!-- 多说评论框 start -->
            <div class="ds-thread" data-thread-key="<%= post.layout %>-<%= post.slug %>" data-title="<%= post.title %>" data-url="<%= page.permalink %>"></div>
            <!-- 多说评论框 end -->
            <!-- 多说公共JS代码 start (一个网页只需插入一次) -->
            <script type="text/javascript">
            var duoshuoQuery = {short_name:'<%= config.duoshuo_shortname %>'};
              (function() {
                var ds = document.createElement('script');
                ds.type = 'text/javascript';ds.async = true;
                ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
                ds.charset = 'UTF-8';
                (document.getElementsByTagName('head')[0] 
                 || document.getElementsByTagName('body')[0]).appendChild(ds);
              })();
              </script>
            <!-- 多说公共JS代码 end -->
          </section>
    <% } %>