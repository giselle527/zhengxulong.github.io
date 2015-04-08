---
layout: post
title:  "SpringMVC返回Json数据中文乱码"
date:   2015-04-07 19:34:59
categories: Java
tags: [Java,springMVC]
---
<p style="font-size:16px;line-height:30px">今天，在修改公司项目bug的时候，当SpringMVC返回json数据时，前台js调用之后，显示为“???????”这样乱码，后来查了一下，有以下两种解决方法：</p></br>

方法一：在action中取得response，由他写入响应数据。
{% highlight ruby %}
response.setHeader("Cache-Control", "no-cache"); 
response.setContentType("text/json;charset=UTF-8");
response.setCharacterEncoding("UTF-8");
PrintWriter out = response.getWriter();
out.write(result);
{% endhighlight %}

方法二：在aciton的需要返回json的方法的@requestMaping中设置produces的值
{% highlight ruby %}
@ResponseBody
@RequestMapping(value="/list", produces = "text/html;charset=UTF-8")
public String getBookList(HttpServletResponse response){
      String result = bookService.getBookListFromJson();
	  return result;
}
{% endhighlight %}