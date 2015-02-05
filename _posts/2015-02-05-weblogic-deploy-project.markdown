---
layout: post
title:  "Weblogic--项目部署"
date:   2015-02-05 22:34:59
categories: [Weblogic]
tags: weblogic linux
---
<p style="font-size:16px;line-height:30px">在上两篇中，分别介绍了linux下安装和启动weblogic，接下来这一篇介绍一下如何部署web项目。
当web项目开发完毕之后，就需要部署到服务器上，这时需要将项目打包成war包，以便发布，下面介绍如何在weblogic下发布web项目：</p>

###第一步：在游览器中地址栏中输入：http://ip:7001/console,打开weblogic控制台登录界面，如下图：

<img  src="/images/weblogic/1.png" />

###第二步：输入用户名和密码进行登录，登录成功后，进入weblogic控制台，如下图：

<img  src="/images/weblogic/2.png" />

###第三步：部署项目
<span style="font-size:16px;">点击左侧导航中的"部署"</span>

<img  src="/images/weblogic/3.png" />

<span style="font-size:16px;">点击"安装"</span>

<img  src="/images/weblogic/4.png" />

<span style="font-size:16px;">找到要发布的项目</span>

<img  src="/images/weblogic/5.jpg" />

<span style="font-size:16px;">一直点击"下一步"，直到完成</span>

<img  src="/images/weblogic/6.jpg" />

<img  src="/images/weblogic/7.png" />

###第四步：启动项目

<span style="font-size:16px;">勾选刚添加的项目，点击"启动"</span>

<img  src="/images/weblogic/8.png" />

<span style="font-size:16px;">点击"是"</span>

<img  src="/images/weblogic/9.png" />

<span style="font-size:16px;">项目部署成功</span>

<img  src="/images/weblogic/10.png" />

<span style="font-size:16px;">PS:未启动前，状态为：准备就绪，启动成功后，状态为：活动，所以看到状态为"活动"说明项目启动成功。</span>

<span style="font-size:16px;">通过以上步骤，项目已经部署成功，这时在游览器地址栏中输入：http://ip:7001/项目名 即可以游览项目了。</span>

