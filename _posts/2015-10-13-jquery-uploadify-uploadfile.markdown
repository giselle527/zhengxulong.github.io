---
layout: post
title:  "jquery uploadify实现文件上传"
date:   2015-10-13 19:34:59
categories: jquery
tags: uploadify
---
 <p style="text-indent:30px; line-height:25px">最近在做项目的时候，经常要用到文件上传功能，以前，做文件上传，都是用最原始最笨的方法，后来看到人家用插件，感觉还蛮方便，所以也改用插件了，今天要介绍的这个插件是比较常见的jquery uploadify，使用很方便，只需要通过简单的配置，就可以实现文件上传了，而且还可以带进度条，也可以取消，
下面介绍一下如何配置uploadify</p>
首先需要在页面上引入插件和样式：
{% raw %}
uploadify.css"<!--uploadify 样式--><br/>
jquery-1.7.2.min.js<!--jquery 插件--><br/>
jquery.uploadify.min.js<!--uploadify 插件--><br/>
{% endraw %}
第二，jsp页面上需要引入两个空间，一个是用于游览本地文件的，一个是用来显示进度条的：如下所示
{% raw %}
<input type="file" id="sxzp" name="sxzp" onclick=""><br/>
<div id="file_queue" style="float: left;margin-left: 10px;z-index: 99;"></div><br/>
{% endraw %}
第三，将uploadify绑定到file控件上，

{% raw %}
$("#sxzp").uploadify({<br/>
   'queueID': 'file_queue',<!--queueID控制进度条--><br/>
'auto': true,<!--是否自动上传文件--><br/>
   'method': "post",<!--提交方式--><br/>
   'height': 20,<!--按钮高度--><br/>
'width': 100,<!--按钮宽度--><br/>
'swf': '<%=request.getContextPath()%>/tools/uploadify/uploadify.swf', <!-- uploadify flash文件的路径--><br/>
'uploader': '<%=request.getContextPath()%>/xmfk/qbxs/jsp/uploadFile.jsp?systemid=${systemid}',<!--上传文件的提交地址--><br/>
'rollover': true,<br/>
'fileTypeDesc': '请选择jpg,jpge,gif,png格式的文件',<!--文件类型描述--><br/>
'fileTypeExts': '*.jpg;*.jpge;*.gif;*.png;',<!--文件扩展名过滤--><br/>
'fileSizeLimit': '1024KB',<!--文件大小限制，格式为1KB或1MB--><br/>
'buttonText': '附件上传',<!--按钮显示的文字--><br/>
'uploadLimit': 100,<!--可以上传文件的最大数量--><br/>
'successTimeout': 5,<br/>
'requeueErrors': false,<br/>
'multi': false,<!--是否允许多文件上传--><br/>
'progressData': 'percentage',<!--进度条显示，百分比--><br/>
'removeTimeout': 1,<br/>
'removeCompleted': true,<!--上传成功后移除进度条--><br/>
'queueSizeLimit': 999,<br/>
'onUploadSuccess': function (file, data, response) {<br/>
     <!--文件上传成功做处理的方法，一般是图片回显--><br/>
   },<br/>
'onError': function (event, ID, fileObj, errorObj) {<br/>
alert(errorObj.type + ' Error: ' + errorObj.info);<br/>
},<br/>
'onInit': function () {<br/>

},<br/>
'onUploadStart' : function(file) {<br/>
   }<br/>

});<br/>
{% endraw %}

PS:uploadify官方下载地址：http://www.uploadify.com/
