---
layout: post
title:  "Intellij IDEA 安装jrebel实现热部署"
date:   2015-06-20 19:34:59
categories: 开发工具
tags: IDEA
---

   <p style="text-indent:30px; line-height:25px">刚从eclipse转Intellij IDEA，总会碰到各种问题,上一篇中已经介绍了如何在idea中部署项目，接下来这一篇将介绍如何在Intellij idea14中安装和破解JRebel：</p>
###第一步：Intellij Idea14破解
 Intellij Idea14是一个收费工具，其可以免费试用30天，有收费，就会有破解，网上有Intellij Idea14的注册机，有这里用的是在百度贴吧上找到的一个注册码，感谢吧主的无私奉献</br>
{% highlight ruby %}
用户名：Java吧专属
注册码：80459-K3G4P-P2YWP-PL1CL-KZR5O-JM0I0
{% endhighlight %}
  ![idea14破解]({{ site.url }}/images/idea/clipboard4.png)
  
###第二步：安装JRebel插件
 打开Intellij，进入 Intellij IDEA - Preferences - Plugins -Browse repositories...
  ![JRebel安装]({{ site.url }}/images/idea/clipboard5.png)
  搜索jre，可以看到JRebel插件，选择安装
  ![JRebel安装]({{ site.url }}/images/idea/clipboard6.png)
  安装完毕之后，可以看到多了两个图标，点击其中一个图标，完成注册，获得14天的试用期，
   ![JRebel安装]({{ site.url }}/images/idea/clipboard7.png)
###第三步：破解JRebel
  下载破解文件： [jrebel.jar和jrebel.lic][jrebel.jar和jrebel.lic]</br>
  替换jar包和licence文件。 </br>
  将本机C:/Users/Administrator/.jrebel/jrebel.lic替换为下载的jrebel.lic；</br>
  将本机 C:/Users/Administrator/.IntelliJIdea14/config/plugins/jr-ide-idea/lib/jrebel</br>
   C:/Users/Administrator/.IntelliJIdea14/config/plugins/jr-ide-idea/lib/jrebel6</br>
  替换为下载的jrebel.jar
  重启Intellij
   ![JRebel破解]({{ site.url }}/images/idea/clipboard8.png)
   如果重启之后看到上面图片的情况，说明已经破解成功。</br>
   PS:
   >1、如果启动时报 “ java.lang.OutOfMemoryError: PermGen space ” ，需设置VM options，我的设置“-XX:MaxPermSize=1024m”</br>
   >2、JReble无需配置就可以实现热重启，前提是需要将Tomcat的配置“On frame deactivation”从”Do nothing”改成”Update classes and resources”。
 [jrebel.jar和jrebel.lic]:      http://download.csdn.net/detail/ablipan/8751029