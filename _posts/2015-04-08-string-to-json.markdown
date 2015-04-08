---
layout: post
title:  "js将json字符串转换为json对象的方法"
date:   2015-04-08 19:34:59
categories: JavaScript
tags: [JavaScript,Json]
---

<p style="font-size:16px;line-height:30px">在开发过程中，经常需要前后台数据交互，比较常见的方法就是后台返回一串json字符串，在前台调用的时候，需要将这串字符串解析为json数据，通常有以下几种方法：</p>

1，eval方式解析，比较原始的解析方式了
{% highlight ruby %}
function strToJson(str){ 
     var json = eval('('+ str + ')');   
     return  json; 
}
{% endhighlight %}
PS:注意str两旁的小括号

2，使用全局的JSON对象，比较常见
{% highlight ruby %}
function strToJson(str){
    return JSON.parse(str);
}
{% endhighlight %}
3,new Function形式，比较少见
{% highlight ruby %}
function strToJson(str){
     var json=(new Function("return "+str)){};
     return json;
}
{% endhighlight %}

实际中的一个例子：
{% highlight ruby %}
function parseJSON(str){
 if(typeof(str) === 'object') {
  return str;
 } else {
  if(window.JSON){
   return JSON.parse(str);
  } else {
   return eval('(' + str + ')');
  }
 }
}
{% endhighlight %}