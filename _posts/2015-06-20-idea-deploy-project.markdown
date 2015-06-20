---
layout: post
title:  "Intellij IDEA 部署项目"
date:   2015-06-20 19:34:59
categories: 开发工具
tags: IDEA
---

   <p style="text-indent:30px; line-height:25px">作为一名java程序猿，对于ide最熟悉不过的就是eclipse和myeclipse了，但是最近在开发过程中，eclipse总是无故的报错，非要重启才可以使用，严重影响开发效率，
  在同事的推荐下，开始接触了Intellij IDEA，这也是一款非常优秀的java ide，受到很多程序猿的青睐，下面介绍一下如何在Intellij IDEA14中部署项目：</p>
###第一步：
  File->open 导入项目
  按F12设置项目
  Project->Project SDK->选中JDK版本
  ![sdk]({{ site.url }}/images/idea/clipboard.png)
  PS:在Project name 输入项目名，在Project SDK选择安装的jdk版本
###第二步：
  选择Modules->Sources->Add Content Root
  ![Content Root]({{ site.url }}/images/idea/clipboard2.png)
###第三步：
  选择Libraries->添加jar包
  ![jar]({{ site.url }}/images/idea/clipboard3.png)
  
  自从用来idea之后，感觉其真的很方便，界面也很酷，功能也很强大，性能也很好。在下一篇中将介绍如何实现idea热部署。