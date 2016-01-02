---
layout: post
title:  "js限制上传文件大小和上传类型"
date:   2016-01-02 13:34:00
categories: [Javascript]
tags: JavaScript
---
<p style="text-indent:30px; line-height:25px">新的一年，新的开始，距离上一次发表博客已经有两三个月，真的比猪还懒啊，
所以接下来这一年，会争取经常发布，把学到的东西，总结出来。虽然有些东西网上一搜一堆，但自己在总结的时候也可以学到一些，
所以还是有必要总结收藏起来的。</p>
<p style="text-indent:30px; line-height:25px">
之前在做项目的时候，需要做文件上传功能，而我用的是插件是ajaxFileupload.js异步上次，好像这个插件不支持文件大小限制，所以那时
项目需要限制文件大小，所以只能通过js的方式来获取要上传文件的大小，再进行判断过滤。下面介绍一下如何通过js来获取文件大小，
顺便也说一下如何限制上传文件类型，虽然都很简单，但是总结还是有必要的：
</p>
{% highlight java %}
//判断文件大小方法
function judgeFileSize(){
	var fileSystem = new ActiveXObject("Scripting.FileSystemObject");
	var file = fileSystem.GetFile(filePath);获取要上传文件，filePath是文件路径
	fileSize = file.Size;//获取文件大小
	if(fileSize>=10485760){//判断文件大小，这里我限制的是10M
	alert("附件大小不能超过10M，请重新选择!");
	return false;
	}
}
//判断文件后缀方法
function judgeFileType(){
	var UPLOAD_FILE=$("#UPLOAD_FILE").val();//获取文本域的值
	var fileType=UPLOAD_FILE.substr(UPLOAD_FILE.lastIndexOf(".")+1).toLowerCase();//获取文件后缀
	var filterType="jpg,gif,bmp,png,doc,docx,xlsx,xls,txt,pdf,rar";//定义允许上传的文件后缀
	if(filterType.indexOf(fileType)==-1){
		alert("附件格式不正确,只能上传"+filterType+"格式");
		return false;
	}
}
{% endhighlight %} 
<p style="text-indent:30px; line-height:25px">
PS：IE可能会报这个错误： automation 服务器不能创建对象，以下是解决方法：
1、如果是Scripting.FileSystemObject (FSO 文本文件读写)被关闭了，开启FSO功能即可，在“运行”中执行regsvr32 scrrun.dll即可
2、安全模式设置成“中”，如果javascript脚本中报这个错误，还应将IE的安全设置“不允许运行未标记为安全的activeX控件”启用即可。
</p>