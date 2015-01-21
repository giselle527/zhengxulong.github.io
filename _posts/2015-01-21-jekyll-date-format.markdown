---
layout: post
title:  "Jekyll--日期格式化"
date:   2015-01-21 20:34:59
categories: jekyll
tags: jekyll
---
Jekyll在页面上使用{% highlight ruby %}\{\{ page.date \}\}{% endhighlight %}
来显示日期的，但有时候，为了让日期格式更好看，需要对日期进行格式化，下面我整理了一些Jekyll日期格式化的例子：

1、格式一(默认):{% highlight ruby %}\{\{ page.date \}\}{% endhighlight %}
输出结果为：
{% highlight ruby %}
{{ page.date }}
{% endhighlight %}

2、格式二:{% highlight ruby %} \{ \{ page.date | date: '%B %d, %Y' \}\}{% endhighlight %}
输出结果为：
{% highlight ruby %}
{{ page.date | date: '%B %d, %Y' }}
{% endhighlight %}

3、格式三:{% highlight ruby %}\{\{ page.date | date_to_string \}\}{% endhighlight %}
输出结果为：
{% highlight ruby %}
{{page.date | date_to_string}}
{% endhighlight %}

4、格式四:{% highlight ruby %}\{\{ page.date | date_to_xmlschema \}\}{% endhighlight %}
输出结果为：
{% highlight ruby %}
{{ page.date | date_to_xmlschema }}
{% endhighlight %}

5、格式五:{% highlight ruby %}\{\{ page.date | date_to_rfc822 \}\}{% endhighlight %}
输出结果为：
{% highlight ruby %}
{{ page.date | date_to_rfc822 }}
{% endhighlight %}

6、格式六:{% highlight ruby %}\{\{ page.date | date: "%Y-%m-%d" \}\}{% endhighlight %}
输出结果为：
{% highlight ruby %}
{{ page.date | date: "%Y-%m-%d" }}
{% endhighlight %}

7、格式七:{% highlight ruby %}\{\{ page.date | date: "%m/%d/%Y" \}\}{% endhighlight %}
输出结果为：
{% highlight ruby %}
{{ page.date | date: "%m/%d/%Y" }}
{% endhighlight %}

更多日期格式，请参考：[Jekyll Date Formatting Examples]

[Jekyll Date Formatting Examples]: http://alanwsmith.com/jekyll-liquid-date-formatting-examples