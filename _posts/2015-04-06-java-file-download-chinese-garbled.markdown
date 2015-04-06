---
layout: post
title:  "Java文件下载中文乱码"
date:   2015-04-06 19:34:59
categories: Java
tags: Java
---
<p style="font-size:16px;line-height:30px">好长时间没有写博客了，三月份忙于找工作，终于在四月一号成功的上班了，新公司感觉还不错，希望在这里可以得到锻炼，成长。</br>
刚上班第三天，同事就给分配了任务，其实就是修复一下bug，还好，不是很难，都是比较常见的，所以很快就解决了，下面整理一下这几天遇到的一些问题。</p></br>

<p style="font-size:16px;line-height:30px">用java实现下载时，当文件名是中文时，下载下来的文件名就会出现乱码，因此需要进行转码：</br>
方法一：response.setHeader("Content-Disposition", "attachment; filename=" + java.net.URLEncoder.encode(fileName, "UTF-8"));</br>
方法二：response.setHeader( "Content-Disposition", "attachment;filename=" + new String( fileName.getBytes("gb2312"), "ISO8859-1" ) ); </br>