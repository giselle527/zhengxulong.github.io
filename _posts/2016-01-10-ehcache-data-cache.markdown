---
layout: post
title:  "Ehcache缓存入门--对象,数据缓存"
date:   2016-01-10 13:34:59
categories: [Ehcache]
tags: Ehcache
---
<p style="text-indent:30px; line-height:25px">
在上一篇文章中，已经介绍了Ehcache页面缓存的实现方式，接下来介绍Ehcache的另外一种缓存方式，对象,数据缓存。
首先介绍一下ehcache.xml配置：
</p>

<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd"
updateCheck="false">
{% highlight text %}
<!--设置缓存文件 .data 的创建路径。
如果该路径是 Java 系统参数，当前虚拟机会重新赋值。
下面的参数这样解释：
user.home – 用户主目录,
user.dir      – 用户当前工作目录
java.io.tmpdir – 默认临时文件路径
path="E:\Ehcache"也可以自定义缓存存储路径
 设置缓存路径的时候,如果指定的不是临时文件路径,那么需要将overflowToDisk 设置为true，缓存结果如下，会生成.data文件-->
<diskStore path="java.io.tmpdir" />
<defaultCache eternal="false"
	          maxElementsInMemory="1000"
              overflowToDisk="false"
			  diskPersistent="false"
			  timeToIdleSeconds="0"
              timeToLiveSeconds="600"
			  memoryStoreEvictionPolicy="LRU" />
<cache name="SimplePageCachingFilter"
       eternal="false"
       maxElementsInMemory="100"
       overflowToDisk="false"
       diskPersistent="false"
       timeToIdleSeconds="0"
       timeToLiveSeconds="300"
       memoryStoreEvictionPolicy="LRU" />
<cache name="testCache"
	   eternal="false"//表示对象永不过期，此时会忽略timeToIdleSeconds和timeToLiveSeconds属性，默认为false  
       maxElementsInMemory="100"//内存中最大缓存对象数
       overflowToDisk="false"//硬盘中最大缓存对象数，若是0表示无穷大
       diskPersistent="false"//是否缓存虚拟机重启其数据
       timeToIdleSeconds="0"//设定允许对象处于空闲状态的最长时间，以秒为单位。当对象自从最近一次被访问后，如果处于空闲状态的时间超过了timeToIdleSeconds属性值，这个对象就会过期，EHCache将把它从缓存中清空。只有当eternal属性为false，该属性才有效。如果该属性值为0，则表示对象可以无限期地处于空闲状态  
       timeToLiveSeconds="300"//设定对象允许存在于缓存中的最长时间，以秒为单位。当对象自从被存放到缓存中后，如果处于缓存中的时间超过了 timeToLiveSeconds属性值，这个对象就会过期，EHCache将把它从缓存中清除。只有当eternal属性为false，该属性才有效。如果该属性值为0，则表示对象可以无限期地存在于缓存中。timeToLiveSeconds必须大于timeToIdleSeconds属性，才有意义  
       memoryStoreEvictionPolicy="LRU"//当达到maxElementsInMemory限制时，Ehcache将会根据指定的策略去清理内存。可选策略有：LRU（最近最少使用，默认策略）、FIFO（先进先出）、LFU（最少访问次数）
/>

{% endhighlight %} 
{% highlight text %}<diskStore path="E:\Ehcache" />{% endhighlight %}配置成指定路径之后，当设定的缓存大小超出范围时，而且设置overflowToDisk="true",则会在指定路径下生成.data缓存文件，效果如下图所示:<br/>
![我的域名]({{ site.url }}/images/ehcache/ehcache4.png)<br/>

实现对象，数据缓存也有两种方式，一种是通过注解的方式，一种是通过java的方式来实现，接下来介绍一下如何用注解的方式实现缓存，
除了上一篇所需的jar包外，使用注解还需要引入另外一个jar包：ehcache-spring-annotations-1.1.2.jar
###第一种方式:通过注解来实现缓存
使用annonation方式需要在spring 的主配置文件中加入以配置，来启动注解。
{% highlight java %}
<bean>
	<context:component-scan base-package="com.cnitzone.sinov.*"/>
	<ehcache:annotation-driven />
    <ehcache:config cache-manager="cacheManager">
        <ehcache:evict-expired-elements interval="60"></ehcache>
    </ehcache:config>
    <bean id="cacheManager" class="org.springframework.cache.ehcache.EhCacheManagerFactoryBean">
        <propertyname="configLocation"  value="classpath:ehcache.xml">
    </bean>
</beans>
{% endhighlight %}
配置完成之后，在Service层的方法上加上：@Cacheable(cacahName="testCache")获取缓存数据或者用@TriggersRemove(cacheName="testCache",removeAll=true)清空缓存数据
{% highlight java %}
	<!--Controller层-->
	@RequestMapping("/testCache")
    public String testCache(Model model,String key,String code){
        String message="";
        if("1".equals(key)){
            message=cacheService.getName(code);
            System.out.println("message="+message);

        }else if("2".equals(key)){
            cacheService.flush();
            message="清空缓存";
        }
        model.addAttribute("message",message);
        return "cache";
{% endhighlight %}
 {% highlight java %}   
	<!--Service层-->
	@Service("cacheService")
	public class CacheServiceImpl implements CacheService {
		@Override
		@Cacheable(cacheName = "testCache")
		public String getName(String code) {
			System.out.println("查询》》》"+code);
			return System.currentTimeMillis()+code;
		}
		@Override
		@TriggersRemove(cacheName="testCache",removeAll=true)
		public void flush(){
			System.out.println("清除缓存!");
		}
	}
{% endhighlight %}
最后在游览器中输入：http://localhost:8080/basic/testCache?key=1&code=java<br/>
![我的域名]({{ site.url }}/images/ehcache/ehcache5.png)<br/>
再次刷新可以看到数据不变
接下来调用清空缓存方法：http://localhost:8080/basic/testCache?key=2&code=java<br/>
![我的域名]({{ site.url }}/images/ehcache/ehcache6.png)<br/>
然后再访问：http://localhost:8080/basic/testCache?key=1&code=java<br/>
![我的域名]({{ site.url }}/images/ehcache/ehcache7.png)<br/>
可以看到数据已经变了
###第二种方式:通过java的方式来实现缓存
通过java实现缓存的方式很简单，归纳起来就以下三个步骤 
{% highlight text %}
第一步：生成CacheManager对象 
第二步：生成Cache对象 
第三步：向Cache对象里添加由key,value组成的键值对的Element元素 
{% endhighlight %}
接下来通过一个简单的例子来看一下如何通过java的方式来实现缓存。<br/>
{% highlight java %}
public static void main(String []args){
    String fileName="G:\\Workspace\\springmvc\\src\\ehcache.xml";
        CacheManager manager=new CacheManager(fileName);//生成CacheManager对象
        String names[]=manager.getCacheNames();//获取所有配置的cache名
        for(int i=0;i<names.length;i++){
            System.out.println("缓存名："+names[i]);
        }
        Cache cache=manager.getCache("testCache");//获取指定配置的缓存
        cache.put(new Element("name","long"));//添加数据到缓存
        Element element=cache.get("name");//从cache中取元素
        System.out.println("element.getValue()="+element.getValue());//获取元素值
        Object obj=element.getObjectValue();//获取元素值
        System.out.println("(String)obj="+(String)obj);
        manager.shutdown();//卸载CacheManager ,关闭Cache
}
{% endhighlight %}
运行结果如下图<br/>
![我的域名]({{ site.url }}/images/ehcache/ehcache8.png)<br/>
在上面的ehcache.xml文件中，我配置了两个缓存，所以这里打印了两个缓存名,另外从缓存中获取数据的方式有两种，一种是通过element.getValue()来获取，一种是通过element.getObjectValue()来获取，记住，后者获取到的是一个Object对象，还需要进行强制类型转换。
