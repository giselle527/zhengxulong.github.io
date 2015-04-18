---
layout: post
title:  "Windows 上搭建Apache FtpServer"
date:   2015-04-18 19:34:59
categories: FtpServer
tags: FtpServer
---

  <p style="text-indent:30px; line-height:25px">因工作需要，最近经常接触到FTP，今天我来介绍一个开源的FTP服务器，那就是Apache FTPServer，Apache FTPServer是一个100％纯Java的FTP服务器。
它的设计是基于现有的开放式协议的完整和便携式FTP服务器引擎解决方案。FTPServer可独立运行作为Windows服务或Unix/ Linux后台程序或是被嵌入在Java应用程序中。</br>
接下来介绍一下如何在Windows环境下安装Apache FTPServer：</p>
###第一步：下载Apache FTPServer</br>
可以到官网下载:http://mina.apache.org/ftpserver-project/downloads.html
目前最新版本是Apache FtpServer 1.0.6 Release，我这里下载的就是1.0.6版本
###第二步：解压Apache FTPServer</br>
将下载下来的压缩包解压到本地，我的是放在D盘根目录下，其目录结构如下图：
![目录结构]({{ site.url }}/images/ftpserver/20150418212047.png)
###第三步:修改D:\apache-ftpserver-1.0.6\res\conf\users.properties这个文件
{% highlight ruby %}
//admin用户
ftpserver.user.admin.userpassword=admin//密码为admin，默认是有加密的，这里我把它改为admin，也是其他密码
ftpserver.user.admin.homedirectory=./res/home  //FTP服务器访问目录默认是./res/home,可以修改为自己想要访问的目录
ftpserver.user.admin.enableflag=true//当前用户可用
ftpserver.user.admin.writepermission=true//具有上传权限
ftpserver.user.admin.maxloginnumber=0//最大登录用户数
ftpserver.user.admin.maxloginperip=0//同IP登录用户数
ftpserver.user.admin.idletime=0//空闲时间
ftpserver.user.admin.uploadrate=0//上传速率限制
ftpserver.user.admin.downloadrate=0//下载速率限制
//匿名用户
ftpserver.user.anonymous.userpassword=
ftpserver.user.anonymous.homedirectory=./res/home
ftpserver.user.anonymous.enableflag=true
ftpserver.user.anonymous.writepermission=false
ftpserver.user.anonymous.maxloginnumber=20
ftpserver.user.anonymous.maxloginperip=2
ftpserver.user.anonymous.idletime=300
ftpserver.user.anonymous.uploadrate=4800
ftpserver.user.anonymous.downloadrate=4800
{% endhighlight %}
PS:如果不希望匿名登录的话，可以将匿名用户这个配置注释掉
###第四步:修改D:\apache-ftpserver-1.0.6\res\conf\ftpd-typical.xml这个文件
{% highlight ruby %}
<server xmlns="http://mina.apache.org/ftpserver/spring/v1"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="
	   http://mina.apache.org/ftpserver/spring/v1 http://mina.apache.org/ftpserver/ftpserver-1.0.xsd	
	   "
	id="myServer">
	<listeners>
		<nio-listener name="default" port="2121">//默认端口是2121，可以修改为自己的端口
		    <ssl>
                <keystore file="./res/ftpserver.jks" password="password" />
            </ssl>
		</nio-listener>
	</listeners>
	<file-user-manager file="./res/conf/users.properties" encrypt-passwords="clear" />//添加encrypt-passwords="clear"，将密码加密方式修改给clear
</server>
{% endhighlight %}
###第五步：启动FTPServer
打开CMD命令窗口，切换到D:\apache-ftpserver-1.0.6\bin这个目录下
输入以下命令：
{% highlight ruby %}
service install
ftpd.bat res/conf/ftpd-typical.xml
{% endhighlight %}
运行结果如下图：</br>
![安装FTPServer]({{ site.url }}/images/ftpserver/20150418213905.jpg)
PS:FTPServer started 说明FTP服务已经启动成功
###第六步:访问FTP
在游览器中，输入ftp://ip:2121进行访问，如果端口修改了，要换成对应的端口，ip就是FTP所在的服务器的ip，访问如下图所示：</br>
![访问FTP]({{ site.url }}/images/ftpserver/20150418214059.png)
