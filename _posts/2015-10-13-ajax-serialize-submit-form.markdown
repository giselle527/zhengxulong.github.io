---
layout: post
title:  "Ajax序列化的方法提交表单"
date:   2015-10-13 19:34:59
categories: jquery
tags: ajax
---
<p style="text-indent:30px; line-height:25px">
可以像猪一样懒，却不能像猪一样懒得心安理得，已经好久没更新博客了，一个是自己懒，一个是已经有两个月是过着没有网的
日子，就算想写博客，也没办法上传。终于搬进新宿舍，终于可以上网了，所以接一下会把这段时间积累的一些小小经验或者遇到的
一些问题，逐个逐个的发布出来，因为已经都保存到云笔记了。接一下先介绍一下如何用ajax序列化的方式提交表单。</p>
<p style="text-indent:30px; line-height:25px">平时我们在做表单提交的时候，经常用到方法就是$("#xxx").submit();,虽然也可以提交，
但是交互效果不好，会刷新页面，给人一种闪过的感觉，
这次介绍一下如何用ajax提交表单，</p>
<form id="saveForm" action="" method="post">
。。。。。一堆input

</form>
ajax表单提交
{% highlight ruby %}
$.ajax({
type:"post",
url:"/xxx/xxx/save.action",//提交路径
dataType:"json",
data:$("#saveForm").serialize(),//序列化表单
success:function(data){
  <!--提交成功后回调方法-->
}

});
{% endhighlight %}
$("#saveForm").serialize(),//序列化表单，会自动转换成这种格式{变量1：值1,变量2:值2.。。。。。}