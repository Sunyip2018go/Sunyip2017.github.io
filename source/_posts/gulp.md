---
title: gulp入门
date: 2017-02-28 14:25:19
tags:
categories: gulp
description:
---
gulp作为前端自动化工具，可以大大简化我们的工作流程
<!-- more -->
<The rest of comments | 余下全文>

注意：使用gulp需要安装nodejs

### 1、打开命令行全局安装gulp

```
$ npm install gulp -g
```
**-g**是指全局安装

如果下载速度太慢的话，可以考虑安装淘宝npm镜像：

```
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```
将此代码复制到命令行执行，使用时只要将npm换成cnpm就可以了。
安装完成后，命令行输入 **gulp -v**，如果出现gulp的版本号说明安装成功。

### 2、在项目中安装gulp

在命令行新建项目目录，执行

```
$ mkdir my_gulp_projrct
```
**mkdir**在命令行中是新建文件夹的意思

进入项目目录
```
$ cd my_gulp_project
```
生成package.json
```
$ npm init
```
name：填写你的项目名称，
version：填写你的项目的版本号，
description：填写你的项目描述，
entry point：入口文件，因为进行这一步的时候我们还没有创建gulpfile.js,所以默认的是index.js，我们可以自行填写gulpfile.js (gulpfile.js非常重要，gulpfile.js里面的内容就是告诉gulp我们要进行什么操作)，
test command：留空回车，
git repository：留空回车，
keywords：填写你的项目关键字，
author：可以填写你的名字，
license：默认回车，
出现Is this OK？<yes>回车就可以，然后就在我们的项目目录下创建了package.json文件；
{% qnimg packageJson.png title:package.json 'class' %}

你还可以执行
```
$ npm init -y
```
这样会快速生成package.json文件，当然里面的内容也会为空，像这样：

{% qnimg package_y.png title:快速生成package.json 'class' %}

在项目中安装gulp
```
$ npm install gulp --save-dev
```
--save：自动把模块和版本号添加到package.json中的dependencies部分
--save-dev： 自动把模块和版本号添加到package.json中的devdependencies部分
通俗点讲 --save-dev 是你开发时候依赖的东西，--save 是你发布之后还依赖的东西。
这里说一个小技巧，**--save-dev**可以简写成**-D**
执行完这一步会在项目目录中生成node_modules文件夹，gulp安装在node_modules文件夹内，打开package.json会看到gulp的版本号在里面，以后我们安装的gulp的各种插件也会出现在里面；

### 3、安装gulp插件
    
    npm install 
        gulp-imagemin(图片压缩)  
        gulp-uglify(压缩javascript) 
        gulp-concat(合并javascript) 
        gulp-clean-css(压缩css)  
        browser-sync(页面实时开发) 
        gulp-postcss(css处理) 
        gulp-jshint(检测javacript语法) 
        gulp-rename(重命名)
        gulp-cache(只压缩修改的图片，已经压缩的不再压缩，节省时间)
        gulp-pngquant(深度压缩图片)
        gulp-clean(项目完成后清除多余的文件夹)
        gulp.spritesmith(雪碧图)
    --save-dev
    
### 4、编写gulpfile.js

    //导入工具包 require('node_modules里对应模块')
    var gulp          = require('gulp'),
        imageMin =  require("gulp-imagemin"),
        uglify         =  require('gulp-uglify'),
        concat       =  require('gulp-concat'),
        minifyCss   =  require('gulp-clean-css'),
        browserSync  = require('brower-sync'),
        jshint          =  require('gulp-jshint')，
        cache           = require('gulp-cache'),
        pngquant    = require('gulp-pngquant');
        postcss          = require('gulp-postcss'),
        spritesmith     = require('gulp.spritesmith'),
        clean          =   require('gulp-clean');

    //操作javascript
    gulp.task('js',function(){
        gulp.src('src/js/*.js')
            .pipe(jshint()).    //检测
            pipe(concat('all.js')).     //合并
            pipe(uglify({         //压缩
                    mangle: true, //类型：Boolean 默认：true 是否修改变量名
                    compress: true, //类型：Boolean 默认：true 是否完全压缩
                    preserveComments: 'all'  //保留所有注释
            })).     
        gulp.src(['src/js/index.js','src/js/detail.js']) //多个文件以数组形式传入
        //除了test1.js和test2.js（**匹配src/js的0个或多个子文件夹）
        gulp.src(['src/js/*.js', '!src/js/**/{test1,test2}.js']) 
            pipe(gulp.dest('dist/js'));
    });
    
    //操作图片
    gulp.task('img',function(){
        gulp.src('src/img/*.{png,jpg,gif,ico}')
            .pipe(cache(imageMin({
                progressive:true,
                svgoPlugins:[{removeViewBox:false}], //不要移除svg的viewbox属性
                use:[pngquant()]   //使用pngquant深度压缩png图片的imagemin插件
            })))
            .pipe(gulp.dest('dist/img'))
    });
    
    //实时开发
    gulp.task('browser-sync',function(){
        browserSync({
            files:'**',
            server:{
                baseDir:'./'
            }
        });	
    });
    
    //操作小图片形成雪碧图
    gulp.task('sprites',function(){
        gulp.src('spritesImg/*.png')
            .pipe(spritesmith({
                imgName:'sprite.png',   //保存合并后图片的地址
                cssName：'dist/spritesCss/sprites.css',   //保存合并后css的地址
                padding:5,  //合并时图片之间的距离
                algorithm:'binary-tree',   //注释1
                cssTemplate:'css/handlebarsStr.css'  //注释2
            }))
            .pipe(gulp.dest('dist/spritesImg'))
    })
    
    //操作css
    gulp.task('css',function(){     
        var processors = [];
        gulp.src('./src/*.css')      
            .pipe(postcss(processors))
            .pipe(gulp.dest('./dist/css'));     
        });

    gulp.task('clean', function () {
        return gulp.src('src', {read: false})
                    .pipe(clean());
    });
    
    //定义默认任务
    gulp.task('default',['js','img','browser-sync','css','sprites']);

    //监听src文件夹并执行默认任务
    gulp.watch('src', ['default']);
    
## gulp核心API
    
* gulp.src：获取文件
* gulp.dest：写入文件
* gulp.tasks：注册任务
* gulp.watch：监控文件的改动


