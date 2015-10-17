---
layout: post
title:  "js 将json对象解析为字符串"
date:   2015-10-17 13:34:59
categories: [Javascript]
tags: Json
---
<p style="text-indent:30px; line-height:25px">在上一篇中，已经介绍了如何通过js将json字符串转换为json对象，接下来，这一篇将介绍如何将json对象转换为json字符串。
stringify()这个方法就是用于从一个对象解析出字符串.</p>
例如：<br/>
{% highlight java %}
var json = {name:"张三",age:23};
document.write(JSON.stringify(json));
{% endhighlight %} 
输出结果为：<br/>
{% highlight java %}
"{name:"张三",age:23}"
{% endhighlight %} 

PS:将json字符串转换为json对象可以参考上一篇文章:<a href="http://cnitzone.com/blog/2015/04/string-to-json/">《js将json字符串转换为json对象的方法》</a>