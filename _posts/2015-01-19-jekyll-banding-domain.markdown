---
layout: post
title:  "Jekyll--绑定域名"
date:   2015-01-19 22:34:59
categories: jekyll
tags: jekyll
---

   <p style="text-indent:30px; line-height:25px">自从个人博客搭建完成之后，虽然github给了一个username.github.io这样类型的免费域名，但是这样并没有满足我的追求，最后，今晚终于下定决心，自己去注册一个属于自己的真正域名，
   最终注册了：[cnitzone.com]这个域名，其含义就是：中国IT地带。
   </p>
   <p style="text-indent:30px; line-height:25px">接下来说一下如何绑定域名：</p>

###第一步：注册域名
如何注册域名就不多说了，很多网站可以注册，我这里是在万网注册的；
###第二步：添加主机记录

注册完域名之后，需要对域名进行映射，因此需要添加主机记录，映射到网站的ip上，这里我参考了github官方文档[github-help],
添加主机记录过程如下：</br>
登录万网会员中心-->我的域名-->解析-->进入到解析设置-->添加解析-->输入主机名和记录值(这里的记录值填：192.30.252.153) ，这样主机记录就添加好了。具体操作如下图：
![我的域名]({{ site.url }}/images/mydomain.png)
![解析]({{ site.url }}/images/resolve.png)
![解析设置]({{ site.url }}/images/resolvesetting.png)
###第三步：创建CNAME文件
添加好主机记录之后，需要在本地项目根目录下创建一个CNAME文件，在里面添加上我们的域名，域名格式可以是：example.com 或者 blog.example.com，
添加完之后保存；

###第四步：提交到服务器
添加完CNAME文件之后，需要将本地项目更新到github服务器，这样才可以通过域名来访问
提交到服务器可以用以下命令：
{% highlight ruby linenos %}
cd projectname //进入项目跟目录
git add CNAME  //添加CNAME文件
git commit -a -m "add CNAME" //将CNAME提交到本地仓库
git push origin master //将CNAME更新到服务器的master分支
{% endhighlight %}

[github-help]:      https://help.github.com/articles/my-custom-domain-isn-t-working/
[cnitzone.com]:     http://cnitzone.com