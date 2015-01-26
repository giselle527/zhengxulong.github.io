---
layout: post
title:  "Jekyll--文章分类"
date:   2015-01-26 20:34:59
categories: [jekyll]
tags: jekyll
---
在一个博客网站中，往往需要对博文进行分类，所以这时候就需要用到分类属性了，Jekyll提供了两种方式的分类：

####一、当文章只属于一个分类的时候，在文章的头信息中，使用category属性
{% highlight ruby %}
--- 
layout: post
title:  "Jekyll--文章分类" 
category: jekyll 
---
{% endhighlight %}
####二、当文章属于多个分类的时候，在文章的头信息中，使用 categories， categories属性接收一个数组，数组内容即是文章所属分类
{% highlight ruby %}
--- 
layout: post
title: "Jekyll--文章分类" 
categories: [jekyll, test]
---
{% endhighlight %}

输出所有分类
所有的分类信息都被存储在site对象的categories中，所有可以通过liquid的for标签进行输出：
{% highlight ruby %}
{% raw %}
{% for category in site.categories %}
<h2>{{ category | first }}</h2> </span>{{ category | last | size }}</span> 
<ul class="arc-list">
{% for post in category.last %} 
<li>{{ post.date | date:"%d/%m/%Y"}}<a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
</ul> 
{% endfor %}
{% endraw %}
{% endhighlight %} 

其中：<br/>
>* 使用 {% raw %}{{ category | first }}{% endraw %} 输出分类的名称 <br/>
>* 使用 {% raw %}{{ category | last | size }}{% endraw %} 输出该分类下文章的数目 <br/>
>* 遍历category.last输出所有文章的信息，构建到该文章的索引<br/>

PS:在以上{% highlight ruby %}{% raw %}{% 内容 %}、{{ 内容 }}{% endraw %}{% endhighlight %} 中，如果没有采取转义的话，都会被正常输出，所以为了让代码能够原样输出，需要在有{% raw %}{% 内容 %}、{{ 内容 }}{% endraw %}这种格式的地方进行转义，所以在需要转义的地方加上
{% highlight ruby %}{ % raw % }{ % endraw % }{% endhighlight %}即可以输出原样代码了。注意：以上花括号需要跟百分号紧贴在一起，否则不生效.