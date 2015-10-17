---
layout: post
title:  "jQuery BlockUI 使用"
date:   2015-10-17 13:34:59
categories: [jquery]
tags: BlockUI
---

<p style="text-indent:30px; line-height:25px">jQuery BlockUI插件可以在不锁定浏览器的同时，模拟同步模式下发起Ajax请求的行为。该插件激活时，会阻止用户在页面进行的操作，直到插件被关闭。BlockUI通过向DOM中添加元素实现其外观和组织用户交互的行为。
需要引入：jquery-1.7.2.min.js，jquery.blockUI.js</p>

页面遮罩：

{% highlight java %}
{% raw %}
<script type="text/javascript">
$(document).ajaxStart(blockPage).ajaxStop(unBockPage);
</script>
{% endraw %}
{% endhighlight %} 

也可以在某个事件启动时调用遮罩层:

 {% highlight java %}
{% raw %}
function blockPage(){
 $.blockUI({ message: '<h1><img src="busy.gif" /> Just a moment...</h1>' });
}
function unBockPage(){
  $.unblockUI();
}
{% endraw %}
{% endhighlight %} 

页面元素遮罩示例：

html:
{% highlight java %}
{% raw %}
<script type="text/javascript">
//异步加载数据锁住，加载完成解锁
$(document).ajaxStart(blockSimpleDiv).ajaxStop(closeBlock);
</script>

<!--简表-->
<div id="blockDiv">
    <div id="simpleTable">
    <table class="table2" cellpadding="0" cellspacing="0">
<!--要遮罩的内容-->
    </table>
    </div>
</div>
{% endraw %}
{% endhighlight %} 
JS:
{% highlight java %}
{% raw %}
//加载数据时锁住
function blockSimpleDiv(){
$("#simpleTable").parent().block({
message: '<img style=\"margin-bottom: -3px\" src=\"/basic/library/js/ext/resources/images/default/grid/wait.gif\"><h1>正在加载数据，请稍等...</h1>',//提示信息
overlayCSS: { backgroundColor: '#00f',opacity: 0 },
css: {
border: 'none',
'margin-top': '10px',
'padding-top':'130px',
backgroundColor: '#000',
'-webkit-border-radius': '10px',
'-moz-border-radius': '10px',
opacity: .4,
width:'99%',
height:'260px',
color: '#fff'
}});
}
//加载数据完成解锁
function closeBlock(){
$("#blockDiv").unblock();
}
{% endraw %}
{% endhighlight %} 

PS:BlockUI可以用于页面加载数据是等待，或者文件上传是等待，代码很简单，比较好理解，只要在想要加锁的地方加上block即可