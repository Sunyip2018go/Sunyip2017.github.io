---
title: dataTables表格插件入门
date: 2017-02-27 09:14:30
tags: javascript
categories: javascript插件
description:
---
Datatables是一款jquery表格插件。它是一个高度灵活的工具，可以将任何HTML表格添加高级的交互功能。
<!-- more -->
<The rest of comments | 余下全文>

### dataTables.js基本用法
** 1. 引入dataTables文件 **
进入dataTables中文官网<http://dataTables.club>，点击**最新版下载**，下载最新版的dataTables文件，当然你也可以使用官网提供的CDN地址;下载完成后在页面引入dataTables的css、js文件，dataTablesjs依赖jQuery，必须先引入jQuery。

本文我们以jquery.dataTables文件为例，如果需要Bootstrap、jqueryUI样式的表格，引入相应的文件就可以。

**2. 初始化table**
编写基本的页面结构：

    <link rel="stylesheet" href="jquery.dataTables.min.css">
    </head>
    <body>
        <table class="td">          //为table设置class或者id
            <thead>
                <tr>
                    <th>姓名</th>
                    <th>年龄</th>
                    <th>性别</th>
                </tr>
            </thead>
        </table>
    <script src="http://cdn.bootcss.com/jquery/2.1.4/jquery.min.js"></script>
    <script src="jquery.dataTables.min.js"></script>
    <script>
        $(".td").DataTable();           //初始化table
    </script>	

运行页面显示效果如下:

{% qnimg initialization.png title:初始化页面 'class:' %}

**3. 修改table配置**

可以看出dataTables默认是英文状态,并且带有**每页显示数据的数量**、**搜索框**、**页脚信息**、**分页器**,首先我们将英文转换成中文：

    <script>
	$(".td").DataTable({
		//设置语言
      "oLanguage": {
        "sLengthMenu": "每页显示 _MENU_ 条记录",
        "sZeroRecords": "抱歉， 没有找到",
        "sInfo": "从 _START_ 到 _END_ /共 _TOTAL_ 条数据",
        "sInfoEmpty": "没有数据",
        "sInfoFiltered": "(从 _MAX_ 条数据中检索)",
        "sZeroRecords": "没有检索到数据",
        "sSearch": "名称:",
        "oPaginate": {
          "sFirst": "首页",
          "sPrevious": "前一页",
          "sNext": "后一页",
          "sLast": "尾页",
        },
      },
	});
</script>

页面变为中文：

{% qnimg initialization_zh.png title:初始化页面 'class:' %}


接下来我们填充一些数据模拟一下：

    	$(function(){
		//模拟数据
	  	var shuju = [
	      	[
	            "小明",
	            "18",
	            "男",
	        ],
	        [
	            "小红",
	            "17",
	            "女",
	        ],
	        [
	            "小青",
	            "28",
	            "女",
	        ],
	        [
	            "小白",
	            "17",
	            "女",
	        ],
	        [
	            "小黄",
	            "15",
	            "男",
	        ],
	        [
	            "小紫",
	            "14",
	            "女",
	        ],
	        [
	            "小天",
	            "21",
	            "男",
	        ],
	        [
	            "小绿",
	            "17",
	            "男",
	        ]

	    ];
		$(".td").DataTable({
			//数据调取
			 "data":shuju,
			//设置语言
	      "oLanguage": {
	        "sLengthMenu": "每页显示 _MENU_ 条记录",
	        "sZeroRecords": "抱歉， 没有找到",
	        "sInfo": "从 _START_ 到 _END_ /共 _TOTAL_ 条数据",
	        "sInfoEmpty": "没有数据",
	        "sInfoFiltered": "(从 _MAX_ 条数据中检索)",
	        "sZeroRecords": "没有检索到数据",
	        "sSearch": "名称:",
	        "oPaginate": {
	          "sFirst": "首页",
	          "sPrevious": "前一页",
	          "sNext": "后一页",
	          "sLast": "尾页",
	        },
	      },
		});
	})
</script>

**这里一定要记得将数据赋值给data属性**

{% qnimg data_arr.png title:数组数据 'class:' %}

除了用数组的方式定义数据，我们还可以使用对象的方式,当然会有一些差别：

    <script>
	$(function(){
		//模拟数据
	  	var shuju = [
	  		{
	  			"name":"小明",
	  			"age":"18",
	  			"sex":"男"
	  		},
	  		{
	  			"name":"小红",
	  			"age":"17",
	  			"sex":"女"
	  		},
	  		{ 
 				"name":"小青",
 				"age":"28",
 				"sex":"女"
	  		},
	  		{
	  			"name":"小白",
	            "age":"17",
	            "sex":"女",
	  		},
	  		{
	            "name":"小紫",
	            "age":"14",
	            "sex":"女",
	        },
	        {
	            "name":"小天",
	            "age":"21",
	            "sex":"男",
	        },
	        {
	            "name":"小绿",
	            "age":"17",
	            "sex":"男",
	        }	
	  	];

		$(".td").DataTable({
			//数据调取
			 "data":shuju,
              //使用对象数组，一定要配置columns，告诉 DataTables 每列对应的属性
			 "columns": [
	            {data:"name"},
	            {data:"age"},
	            {data:"sex"},
            ],
	      "oLanguage": {
	        "sLengthMenu": "每页显示 _MENU_ 条记录",
	        "sZeroRecords": "抱歉， 没有找到",
	        "sInfo": "从 _START_ 到 _END_ /共 _TOTAL_ 条数据",
	        "sInfoEmpty": "没有数据",
	        "sInfoFiltered": "(从 _MAX_ 条数据中检索)",
	        "sZeroRecords": "没有检索到数据",
	        "sSearch": "名称:",
	        "oPaginate": {
	          "sFirst": "首页",
	          "sPrevious": "前一页",
	          "sNext": "后一页",
	          "sLast": "尾页",
	        }
	      }
		})
	})
</script>

columns在dataTables里面是**列**的意思,里面包含几个data就是有几列,每列的数据是data的值决定的。


页面效果和使用数组数据是一样的：

{% qnimg data_obj.png title:对象数据 'class:' %}

实际开发中数据肯定是从后台调取的，小白能力有限，后台那块涉及的不深，在这就不献丑了，接下来我们来修改dataTables的默认的几个选项，只要添加几个属性就可以：

    		$(".td").DataTable({
			//数据调取
			 "data":shuju,
			 "columns": [
	            {data:"name"},
	            {data:"age"},
	            {data:"sex"},
            ],
	      "oLanguage": {
	        "sLengthMenu": "每页显示 _MENU_ 条记录",
	        "sZeroRecords": "抱歉， 没有找到",
	        "sInfo": "从 _START_ 到 _END_ /共 _TOTAL_ 条数据",
	        "sInfoEmpty": "没有数据",
	        "sInfoFiltered": "(从 _MAX_ 条数据中检索)",
	        "sZeroRecords": "没有检索到数据",
	        "sSearch": "名称:",
	        "oPaginate": {
	          "sFirst": "首页",
	          "sPrevious": "前一页",
	          "sNext": "后一页",
	          "sLast": "尾页",
	        }
	      },
          //修改默认选项
	      paging: false,   //分页器关闭
	      searching: false,  //搜索关闭
	      LengthChange: false, //改变每页显示数据数量关闭
	      bInfo: false,//页脚信息
		})
        
页面变为这样：

{% qnimg morenHide.png title:默认选项关闭 'class:' %}

如果你写的页面有好多个表格，并且每个的配置都是一样的，那我们可以使用**$.fn.dataTable.defaults**对象来处理：

    // 默认禁用搜索和排序
		$.extend($.fn.dataTable.defaults, {
    		paging: false,   //分页器关闭
	        searching: false,  //搜索关闭
	        LengthChange: false, //改变每页显示数据数量关闭
	        bInfo: false,//页脚信息
		});

        //dataTables初始化
		$(".td").DataTable({
			//数据调取
			 "data":shuju,
			 "columns": [
	            {data:"name"},
	            {data:"age"},
	            {data:"sex"},
            ],
	      "oLanguage": {
	        "sLengthMenu": "每页显示 _MENU_ 条记录",
	        "sZeroRecords": "抱歉， 没有找到",
	        "sInfo": "从 _START_ 到 _END_ /共 _TOTAL_ 条数据",
	        "sInfoEmpty": "没有数据",
	        "sInfoFiltered": "(从 _MAX_ 条数据中检索)",
	        "sZeroRecords": "没有检索到数据",
	        "sSearch": "名称:",
	        "oPaginate": {
	          "sFirst": "首页",
	          "sPrevious": "前一页",
	          "sNext": "后一页",
	          "sLast": "尾页",
	        }
	      }
		});

**这里一定要注意**$.fn.dataTable.defaults**一定要放在dataTables初始化的前面**

页面效果和单独设置是一样的：

{% qnimg morenHide.png title:默认选项关闭 'class:' %}

当然某一个表格需要某一个功能可以在此dataTables初始化中重新设置为打开

默认选项中的**每页显示数据数量**默认是显示10、25、50、100,我们可以根据自己需求进行设置：

    $(".td").DataTable({
			//数据调取
			 "data":shuju,
			 "columns": [
	            {data:"name"},
	            {data:"age"},
	            {data:"sex"},
            ],
	      "oLanguage": {
	        "sLengthMenu": "每页显示 _MENU_ 条记录",
	        "sZeroRecords": "抱歉， 没有找到",
	        "sInfo": "从 _START_ 到 _END_ /共 _TOTAL_ 条数据",
	        "sInfoEmpty": "没有数据",
	        "sInfoFiltered": "(从 _MAX_ 条数据中检索)",
	        "sZeroRecords": "没有检索到数据",
	        "sSearch": "名称:",
	        "oPaginate": {
	          "sFirst": "首页",
	          "sPrevious": "前一页",
	          "sNext": "后一页",
	          "sLast": "尾页",
	        }
	      },
          //设置每页显示的数据数量
	      "aLengthMenu": [[20, 40, 60, -1], [20, 40, 60, "All"]]
		})
        
如果想要自定义一列表格，我们可以这样：

    <table class="td">
		<thead>
			<tr>
				<th>姓名</th>
				<th>年龄</th>
				<th>性别</th>
				<th></th>
			</tr>
		</thead>
	</table>
在thead中添加一个th，然后

    $(".td").DataTable({
			//数据调取
			 "data":shuju,
			 "columns": [
	            {data:"name"},
	            {data:"age"},
	            {data:"sex"},
	            {
	            	data:null,
	            	"width":"1%",
            		"orderable":false,//禁用排序
            		"defaultContent": "<i>还没有设置</i>"
	            }
            ],
	      "oLanguage": {
	        "sLengthMenu": "每页显示 _MENU_ 条记录",
	        "sZeroRecords": "抱歉， 没有找到",
	        "sInfo": "从 _START_ 到 _END_ /共 _TOTAL_ 条数据",
	        "sInfoEmpty": "没有数据",
	        "sInfoFiltered": "(从 _MAX_ 条数据中检索)",
	        "sZeroRecords": "没有检索到数据",
	        "sSearch": "名称:",
	        "oPaginate": {
	          "sFirst": "首页",
	          "sPrevious": "前一页",
	          "sNext": "后一页",
	          "sLast": "尾页",
	        }
	      },
	      "aLengthMenu": [[20, 40, 60, -1], [20, 40, 60, "All"]]
          
在columns属性中添加一个data,放上你想要放的内容,width是此表格的宽度,orderable是排序设置,defaultContent是要放置的内容。

{% qnimg addTable.png title:添加一行数据 'class' %}

写到这，我发现这个表格的样式简直无法直视，什么鬼啊，所以我决定引入Bootstrap样式。

如果你想修改各个控件的位置，可以使用dom属性：

    $(".td").DataTable({
			//数据调取
			 "data":shuju,
             //dom属性控制各控件位置
			  "dom": '<"top"i>rt<"bottom"flp><"clear">',
			 "columns": [
	            {data:"name"},
	            {data:"age"},
	            {data:"sex"},
	            {
	            	data:null,
	            	"width":"1%",
            		"orderable":false,//禁用排序
            		"defaultContent": "还没有设置"
	            }
            ],

1. `l` 代表 length，左上角的改变每页显示条数控件
2. `f` 代表 filtering，右上角的过滤搜索框控件
3. `t` 代表 table，表格本身
4. `i` 代表 info，左下角的表格信息显示控件
5. `p` 代表 pagination，右下角的分页控件
6. `r` 代表 processing，表格中间的数据加载等待提示框控件
7. `B` 代表 button，Datatables可以提供的按钮控件，默认显示在左上角
8. `< >`代表一个div元素
9. `<"#id" >` 指定了id的div元素
10.`<"class" >`指定了样式名的div元素
11.`<"#id.class" >`指定了id和样式的div元素





    




    














