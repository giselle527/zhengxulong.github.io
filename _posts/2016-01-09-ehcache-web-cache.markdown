---
layout: post
title:  "Ehcache缓存入门--页面缓存"
date:   2016-01-09 13:34:59
categories: [Ehcache]
tags: Ehcache
---
<p style="text-indent:30px; line-height:25px">
百度百科解析：
EhCache是一个纯Java的进程内缓存框架，具有快速、精干等特点，是Hibernate中默认的CacheProvider。
Ehcache是一种广泛使用的开源Java分布式缓存。主要面向通用缓存,Java EE和轻量级容器。它具有内存和磁盘存储，缓存加载器,缓存扩展,缓存异常处理程序,一个gzip缓存servlet过滤器,支持REST和SOAP api等特点。
Ehcache缓存有两种方式，一种是页面缓存，一种是数据对象缓存。这次先介绍一下Ehcache的页面缓存功能。
Ehcache缓存使用非常方便，只需要导入两个jar包和一个依赖包。
{% highlight html %}
ehcache-core-2.4.5.jar
ehcache-web-2.0.4.jar  主要用于页面缓存
slf4j-api-1.6.2.jar 依赖包
{% endhighlight %} 
将这三个包导入到项目里面，我这里结合的时候springmvc，所以还需要springmvc所需的其他jar包。这里就不再列出来，不懂的问度娘。
</p>
<p style="text-indent:30px; line-height:25px">
Ehcache页面缓存也分三种方式：
{% highlight html %}
1、SimplePageCachingFilter：整体页面缓存
2、SimplePageFragmentCachingFilter：局部页面缓存
3、SimpleCachingHeadersPageCachingFilter ：提供HTTP 缓存头信息
SimpleCachingHeadersPageCachingFilter用的比较少，所以这里只介绍前面两种缓存方式。
{% endhighlight %} <br/>
</p>
下面介绍如何在springmvc中配置Ehcache页面缓存，首先在src根目录下创建一个ehcache.xml文件，然后配置缓存：
{% highlight html %}
<!-- 页面全部缓存 name默认必须是SimplePageCachingFilter-->
<cache name="SimplePageCachingFilter"
eternal="false"
maxElementsInMemory="100"
overflowToDisk="false"
diskPersistent="false"
timeToIdleSeconds="0"
timeToLiveSeconds="300"
memoryStoreEvictionPolicy="LRU" />
<!--自定义缓存-->
<cache name="testCache"
eternal="false"
maxElementsInMemory="100"
overflowToDisk="false"
diskPersistent="false"
timeToIdleSeconds="0"
timeToLiveSeconds="300"
memoryStoreEvictionPolicy="LRU" />
{% endhighlight %}
然后在application.xml文件下配置创建加载ehcache.xml
{% highlight java %}
<ehcache:annotation-driven />
<ehcache:config cache-manager="cacheManager">
	<ehcache:evict-expired-elements interval="60" />
</ehcache:config>
<bean id="cacheManager" class="org.springframework.cache.ehcache.EhCacheManagerFactoryBean">
    <property name="configLocation"  value="classpath:ehcache.xml"/>
</bean>
{% endhighlight %}
接下来就是如何配置页面缓存了：
</p>
###第一种方式:SimplePageCachingFilter整体页面缓存<br/>
在web.xml文件下，添加缓存拦截器
{% highlight html %}
<!--ehcache 页面缓存过滤器-->
<filter>
    <filter-name>PageCachingFilter</filter-name>
    <filter-class>net.sf.ehcache.constructs.web.filter.SimplePageCachingFilter</filter-class>
<!--init-param 部分，如果是使用默认的配置，可以不用写，默认为SimplePageCachingFilter，如果需要指定自定义的缓存则需要init-param部分是必须指定的，param-value就是自定义的缓存名称-->
    <init-param>
        <param-name>cacheName</param-name>
        <param-value>testCache</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>PageCachingFilter</filter-name>
	<!--配置需要缓存的页面-->
    <url-pattern>/toWebCache</url-pattern>
</filter-mapping>
{% endhighlight %}
接下来测试一下，我的java代码是这样的
{% highlight java %}
    @RequestMapping("/toWebCache")
    public String toWebCache(Model model){
        System.out.println("页面缓存测试");
        String dateTime=String.valueOf(System.currentTimeMillis());
        System.out.println(dateTime);
        model.addAttribute("dateTime",dateTime);
        return "web_cache";//跳转视图
    }
{%endhighlight %}
最后在游览器中访问一下：http://localhost:8080/basic/toWebCache，可以看到如下效果
![我的域名]({{ site.url }}/images/ehcache/ehcache1.png)<br/>
再次刷新页面，可以看到页面数据不变，说明缓存已经起作用了。<br/>
###第二种方式：SimplePageFragmentCachingFilter，页面局部缓存<br/>
还是跟第一种方法一样，需要在ehcache.xml文件配置：
{% highlight java %}
<!--Ehcache页面局部缓存默认缓存-->
<cache name="SimplePageFragmentCachingFilter"
	   eternal="false"
       maxElementsInMemory="100"
       overflowToDisk="false"
       diskPersistent="false"
       timeToIdleSeconds="0"
       timeToLiveSeconds="300"
       memoryStoreEvictionPolicy="LRU" />
{%endhighlight %}
接下来还是在web.xml配置拦截器：
{% highlight html %}
<!--ehcache 页面缓存过滤器 -->
<filter>
    <filter-name>PageCachingFilter</filter-name>
    <filter-class>net.sf.ehcache.constructs.web.filter.SimplePageFragmentCachingFilter</filter-class>
<!--init-param 部分，如果是使用默认的配置，可以不用写，如果需要指定自定义的缓存则需要init-param部分是必须指定的，param-value就是自定义的缓存名称-->
    <init-param>
        <param-name>cacheName</param-name>
        <param-value>testCache</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>PageCachingFilter</filter-name>
<!--要缓存的子页面，就是用
<jsp:include page="/jsp/child_cache.jsp"></jsp:include>
-->
    <url-pattern>/jsp/child_cache.jsp</url-pattern>
    <dispatcher>INCLUDE</dispatcher>
</filter-mapping>
{%endhighlight %}
接下来再测试一下，我的java代码是这样的：
{% highlight java %}
    @RequestMapping("/toChildWebCache")
    public String toChildWebCache(Model model){
        System.out.println("子页面缓存测试");
        String dateTime=String.valueOf(System.currentTimeMillis());
        System.out.println(dateTime);
        model.addAttribute("dateTime",dateTime);
        return "test_cache";
    }
{% endhighlight %}
最后在游览器中访问一下：http://localhost:8080/basic/toChildWebCache，可以看到如下效果 :
![我的域名]({{ site.url }}/images/ehcache/ehcache2.png)<br/>
再次刷新<br/>
![我的域名]({{ site.url }}/images/ehcache/ehcache3.png)<br/>
可以看到子页面的内容不变，而父页面的内容改变了。<br/>
PS：<p style="text-indent:30px; line-height:25px">include的jsp页面在filter中要指定<dispatcher>INCLUDE</dispatcher> ，
如果没有指定任何< dispatcher >元素，默认值是REQUEST就不会拦截了。
 <url-pattern>是要缓存的子页面，就是用<jsp:include page="/jsp/child_cache.jsp"></jsp:include>包含进来的页面。</p>