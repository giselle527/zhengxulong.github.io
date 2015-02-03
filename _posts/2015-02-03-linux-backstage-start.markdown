---
layout: post
title:  "Weblogic--后台启动两种方法"
date:   2015-02-03 23:34:59
categories: [Weblogic]
tags: weblogic linux
---
<p style="font-size:16px;line-height:30px">在上一篇中，已经介绍了如何在linux安装weblogic10g。接下来这一篇简单说一下weblogic后台启动的两种方法。
一般情况下，我们都是通过远程来操作linux服务器的，所以就需要用到一些远程连接工具，我这里使用的是SSH这个工具。
一开始，对linux还不是很了解，所以我都是直接用./startWeblogic.sh这种方式来启动weblogic的，虽然这样是可以启动，但是每当断开与Linux服务器的连接是，weblogic也会随之会被断开。
所以就会造成SSH关闭后，weblogic将无法访问的情况，这个也是我在部署项目的时候遇到的一个问题，后来终于知道，原来需要将weblogic进程调到linux后台进行运行，SSH断开才不会影响weblogic的访问。</br>下面就是weblogic后台启动的两种方法：</br></p>

###方法一：进入到startWeblogic.sh所在目录，键入以下这条命令启动
{% highlight text %}
 nohup ./startWeblogic.sh &
{% endhighlight %}

###方法二:如果是直接用 ./startWeblogic.sh启动时，可以用下面方法将程序调到后台运行，实现交互
{% highlight text %}
按下 "ctrl+z"
输入 "bg"  程序进入后台运行
{% endhighlight %}

 