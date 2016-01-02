---
layout: post
title:  "ajaxSubmit提交获取文件大小"
date:   2016-01-02 13:34:59
categories: [Javascript]
tags: JavaScript
---
<p style="text-indent:30px; line-height:25px">
最近同事问到一个问题，就是在附件上传的时候，当选中附件后，要获取文件大小要怎么弄，
因为文件是在客户端，如果用上一篇介绍的方法的话，虽然可以实现，但是可能会出现我所说的那个问题，
“ automation 服务器不能创建对象”，这样的话需要用户进行ie设置，这样比较麻烦，对用户来说很不方便，
而且如果用户量大的话，根本不可能，后来用了ajaxFileUpload.js这个插件来实现异步上传，但有一个问题，
就是onchange时候提交到后台，获取大小返回后，file变为空，这样需要重新选择文件才可以保存，
这种方法也不行，后来想到了用ajaxSubmit提交表单的方式来获取文件大小，因为ajaxSubmit是无刷新的，
所以提交表单后可以返回文件大小，赋值给文本框，而且file也不会被清空，最后点保存的时候再提交表单，把
文件写入数据库或者服务器上。虽然要通过两次上传才能完成这个表单的提交，但是暂时只想到这种方法。
下面介绍一下如何用ajaxSubmit这个方法来提交表单。
</p>
{% highlight html %}
{% raw %}
//使用ajaxSubmit需要导入的两个脚步
<script type="text/javascript" src="jsp/js/jQuery 1.8.3.js"></script>
<script type="text/javascript" src="/js/js/jquery.form.js"></script>  
{% endraw %}
{% endhighlight %}    
{% highlight html %}
{% raw %}
            $(this).ajaxSubmit({  
                type:"post",  //提交方式 ，有两种：post和get 
                dataType:"json", //后台返回数据类型  
                url:"<%=request.getContextPath()%>/upload/upload.action", //请求url  
                success:function(data){ //提交成功的回调函数  
                    alert(data.result);  
                }  
            });  
{% endraw %}
{% endhighlight %} 