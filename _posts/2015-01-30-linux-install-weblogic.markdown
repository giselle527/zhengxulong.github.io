---
layout: post
title:  "Weblogic--Linux下安装"
date:   2015-01-30 20:34:59
categories: [Weblogic]
tags: weblogic linux
---
weblogic是一款当前比较常用的web应用服务器，在web项目开发过程中，往往需要用到weblogic进行部署项目，当项目开发完毕之后，又需要将项目部署到服务器上，在工作这段时间里，我接触了weblogic，之前都是用tomcat的，
以下是我工作以来接触weblogic整理的一些笔记，现在分享出来。我这里使用的linux Red hat服务器。
准备安装：weblogic10g安装包(wls1034_generic.jar) ，我这里使用的是weblogic10g，具体版本需要根据服务器类型而定，可以自行到oracle官网下载。下载后将安装包上传到linux服务器上，就可以开始安装了。
安装步骤：
###一，安装程序
用SSH连接linux服务器，切换到安装文件所在目录下，执行以下命令：
{% highlight ruby %}
java -jar wls1034_generic.jar 
{% endhighlight %}

即可启动安装过程, 默认启动的是图形界面的安装向导. 命令行方式的安装命令用如下方式启动:
{% highlight ruby %}
java -jar wls1034_generic.jar -mode=console
{% endhighlight %} 
由于linux一般都是不提供图形界面操作的，所以可以执行第二条命令。默认安装在Oracle目录下。
###二，创建域
安装完程序之后，就开始创建域，
创建域步骤：<br/>
>1、进入 cd /Oracle/Middleware/wlserver_10.3/common/bin目录<br/>
>2、用ls命令查看目录下有哪些文件<br/>
>3、执行. /config.sh 文件，创建域<br/>
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Welcome:
--------
Choose between creating and extending a domain. Based on your selection,
the Configuration Wizard guides you through the steps to generate a new or
extend an existing domain.
 ->1|Create a new WebLogic domain
    | Create a WebLogic domain in your projects directory.
   2|Extend an existing WebLogic domain
    | Use this option to add new components to an existing domain and modify |configuration settings.

Enter index number to select OR [Exit][Next]> 1  ##这里选1，Create a new WebLogic domain
{% endhighlight %}
>4、选择域源
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Select Domain Source:
---------------------
Select the source from which the domain will be created. You can create the
domain by selecting from the required components or by selecting from a
list of existing domain templates.
 ->1|Choose Weblogic Platform components
    | You can choose the Weblogic component(s) that you want supported in
    |your domain.
   2|Choose custom template
    | Choose this option if you want to use an existing template. This
    |could be a custom created template using the Template Builder.

Enter index number to select OR [Exit][Previous][Next]>1  ##这里选1，Choose Weblogic Platform components
{% endhighlight %}
>5、设置域信息
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Edit Domain Information:
------------------------
    | Name | Value |
   _|________|_____________|
   1| *Name: | base_domain |

Enter value for "Name" OR [Exit][Previous][Next]> next  ##这里直接输入next即可，也可以输入自定义域，默认是base_domain
{% endhighlight %}

>6、为域选择模板域目录，输入next使用默认的域
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Select the target domain directory for this domain:
---------------------------------------------------
    "Target Location" = [Enter new value or use default
"/home/yinm/Oracle/Middleware/user_projects/domains"]

Enter new Target Location OR [Exit][Previous][Next]>next  ##默认即可
{% endhighlight %}

>7、设置weblogic登录用户名和密码
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Configure Administrator User Name and Password:
-----------------------------------------------
Create a user to be assigned to the Administrator role. This user is the
default administrator used to start development mode servers.
    | Name | Value |
   _|_________________________|_________________________________________|
   1| *Name: | weblogic |
   2| *User password: | |
   3| *Confirm user password: | |
   4| Description: | This user is the default administrator. |
Use above value or select another option:
    1 - Modify "Name"
    2 - Modify "User password"
    3 - Modify "Confirm user password"
    4 - Modify "Description"

Enter option number to select OR [Exit][Previous][Next]> 2  #这里我使用默认的用户名weblogic，直接输入2设置密码
{% endhighlight %}
>8、设置weblogic密码：
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Configure Administrator User Name and Password:
-----------------------------------------------
Create a user to be assigned to the Administrator role. This user is the
default administrator used to start development mode servers.
    "*User password:" = []
Enter new *User password: OR [Exit][Reset][Accept]> 12345678  ##这里是登录weblogic控制台的密码
{% endhighlight %}
>9、设置weblogic确认密码
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Configure Administrator User Name and Password:
-----------------------------------------------
Create a user to be assigned to the Administrator role. This user is the
default administrator used to start development mode servers.
    | Name | Value |
   _|_________________________|_________________________________________|
   1| *Name: | weblogic |
   2| *User password: | ********** |
   3| *Confirm user password: | |
   4| Description: | This user is the default administrator. |
Use above value or select another option:
    1 - Modify "Name"
    2 - Modify "User password"
    3 - Modify "Confirm user password"
    4 - Modify "Description"
    5 - Discard Changes

Enter option number to select OR [Exit][Previous][Next]> 3  ##这里选择3，设置确认密码
{% endhighlight %}
>10、输入weblogic确认密码
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Configure Administrator User Name and Password:
-----------------------------------------------
Create a user to be assigned to the Administrator role. This user is the
default administrator used to start development mode servers.
    "*Confirm user password:" = []
Enter new *Confirm user password: OR [Exit][Reset][Accept]> 12345678  ##记住，确认密码必须与第8步设置的一致
{% endhighlight %}
>11、修改用户名和密码
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Configure Administrator User Name and Password:
-----------------------------------------------
Create a user to be assigned to the Administrator role. This user is the
default administrator used to start development mode servers.
    | Name | Value |
   _|_________________________|_________________________________________|
   1| *Name: | weblogic |
   2| *User password: | ********** |
   3| *Confirm user password: | ********** |
   4| Description: | This user is the default administrator. |
Use above value or select another option:
    1 - Modify "Name"
    2 - Modify "User password"
    3 - Modify "Confirm user password"
    4 - Modify "Description"
    5 - Discard Changes

Enter option number to select OR [Exit][Previous][Next]> next  ##如无线修改，直接输入next即可
{% endhighlight %}
>12、配置域模式
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Domain Mode Configuration:
--------------------------
Enable Development or Production Mode for this domain.
 ->1|Development Mode
   2|Production Mode
Enter index number to select OR [Exit][Previous][Next]> 2  ##这些选择2，Production Mode(生成模式)
{% endhighlight %}
>13、选择JDK
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Java SDK Selection:
-------------------
 ->1|Sun SDK 1.6.0_45 @ /usr/local/jdk1.6.0_45
   2|Other Java SDK

Enter index number to select OR [Exit][Previous][Next]> 1  ##这里选择1
{% endhighlight %}
>14、可选配置
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Select Optional Configuration:
------------------------------
   1|Administration Server [ ]
   2|Managed Servers, Clusters and Machines [ ]
   3|RDBMS Security Store [ ]
    ** Invalid input, only integer selection or page movement command are
    ** accepted: y
Enter index number to select OR [Exit][Previous][Next]> 1#这里选择1
{% endhighlight %}
>15、下一步，输入next
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Select Optional Configuration:
------------------------------
   1|Administration Server [x]
   2|Managed Servers, Clusters and Machines [ ]
   3|RDBMS Security Store [ ]
Enter index number to select OR [Exit][Previous][Next]>next
{% endhighlight %}
>16、设置监听地址
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Configure the Administration Server:
------------------------------------
Each WebLogic Server domain must have one Administration Server. The
Administration Server is used to perform administrative tasks.
    | Name | Value |
   _|__________________|_____________________|
   1| *Name: | AdminServer |
   2| *Listen address: | All Local Addresses |
   3| Listen port: | 7001 |
   4| SSL listen port: | N/A |
   5| SSL enabled: | false |
Use above value or select another option:
    1 - Modify "Name"
    2 - Modify "Listen address"
    3 - Modify "Listen port"
    4 - Modify "SSL enabled"
Enter option number to select OR [Exit][Previous][Next]>2  ##选择2，设置监听地址
{% endhighlight %}
>17、配置监听地址
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Configure the Administration Server:
------------------------------------
Each WebLogic Server domain must have one Administration Server. The
Administration Server is used to perform administrative tasks.
    | Name | Value |
   _|__________________|_____________________|
   1| *Name: | AdminServer |
   2| *Listen address: | All Local Addresses |
   3| Listen port: | 7001 |
   4| SSL listen port: | N/A |
   5| SSL enabled: | false |
Enter value for "Listen address" OR [Exit][Previous][Next]>10.211.*.*  ##这里输入服务器的ip
{% endhighlight %}
>18、配置监听端口
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Configure the Administration Server:
------------------------------------
Each WebLogic Server domain must have one Administration Server. The
Administration Server is used to perform administrative tasks.
    | Name | Value |
   _|__________________|______________|
   1| *Name: | AdminServer |
   2| *Listen address: | 10.211.*.* |
   3| Listen port: | 7001 |
   4| SSL listen port: | N/A |
   5| SSL enabled: | false |
Use above value or select another option:
    1 - Modify "Name"
    2 - Modify "Listen address"
    3 - Modify "Listen port"
    4 - Modify "SSL enabled"
    5 - Discard Changes

Enter option number to select OR [Exit][Previous][Next]> next  ##默认端口是7001，如果无需修改，直接输入next
{% endhighlight %}
>19、创建weblogic域成功
{% highlight ruby %}
<------------------- Fusion Middleware Configuration Wizard ------------------>
Creating Domain...
0%           25%           50%             75%         100%
[---------------|---------------|--------------|--------------]
[****************************************************]
**** Domain Created Successfully! ****
{% endhighlight %}
>20、启动weblogic
{% highlight ruby %}
1、进入  cd /Oracle/Middleware/user_projects/domains/base_domain 目录
2、输入 ./startWebLogic.sh启动weblogic
{% endhighlight %}
