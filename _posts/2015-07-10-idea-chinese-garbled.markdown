---
layout: post
title:  "Intellij IDEA 导入项目中文乱码"
date:   2015-07-10 19:34:59
categories: 开发工具
tags: IDEA
---
 <p style="text-indent:30px; line-height:25px">用Intellij IDEA已经有一个多月了，确实很好用，开发效率又很高，在一次开发中，从eclipse导入项目到IDEA，发现在IDEA打开出现了中文乱码，所有的中文注释都变成了乱码，这是因为IDEA默认创建的项目编码是UTF-8，而我的项目编码是GBK所导致的。
解决的方法比较简单，下面说一下解决方法：</br>
在File->settings->Editor->File Encodings，将编码设置为GBK就可以了.</p>
![idea14中文乱码]({{ site.url }}/images/idea/clipboard9.png)
![idea14中文乱码]({{ site.url }}/images/idea/clipboard10.png)

