---
layout: post
title:  "记录客户端访问WebService的IP地址"
excerpt: "记录客户端访问WebService的IP地址."
date:   2016-01-11 21:46:21 +0800
categories: J2EE
tags: [J2EE, CXF]
---

在服务端的WebService在被调用时，往往需要记录访问者IP、对IP进行限制或者其进行其他一些记录日志的操作，这时候需要我们对已经写好的接口增加拦截器。

#### 编写拦截器

cxf有2种拦截器，InInterceptor、OutInterceptor，顾名思义，InInterceptor可以处理soap请求消息，OutInterceptor可以处理soap响应消息。所有的拦截器都继承自AbstractPhaseInterceptor<?>，此抽象拦截器实现了Interceptor接口。

我们写的拦截器如下：

{% highlight java lineos %}
package cn.com.dhcc.app.pub.core.interceptor;

import javax.servlet.http.HttpServletRequest;

import org.apache.cxf.interceptor.Fault;
import org.apache.cxf.message.Message;
import org.apache.cxf.phase.AbstractPhaseInterceptor;
import org.apache.cxf.phase.Phase;
import org.apache.cxf.transport.http.AbstractHTTPDestination;
import org.springframework.stereotype.Component;

import cn.com.dhcc.app.core.util.NetUtil;

@Component
public class InLoggingInterceptor extends AbstractPhaseInterceptor<Message> {

	public InLoggingInterceptor() {
    //指定拦截器在哪个阶段被激发,如果在调用之前进行拦截可使用PRE_INVOKE
		super(Phase.RECEIVE);
	}

	@Override
	public void handleMessage(Message message) throws Fault {
		HttpServletRequest request = (HttpServletRequest) message.get(AbstractHTTPDestination.HTTP_REQUEST);
		System.out.println(NetUtil.getRemoteIp(request));
	}

}

{% endhighlight %}

拦截器分为不同的Phase，各个Phase又有自己的拦截器链，参考[http://cxf.apache.org/docs/interceptors.html](http://cxf.apache.org/docs/interceptors.html)。

代码中NetUtil.getRemoteIp这个函数是我们项目中用来获取IP地址的，代码如下：

{% highlight java lineos %}
public static String getRemoteIp(HttpServletRequest request){
   // 获取请求主机IP地址,如果通过代理进来，则透过防火墙获取真实IP地址  
  if(request==null)return null;
      String ip = request.getHeader("X-Forwarded-For");  //通过负载均衡获取真实客户端IP

      if (ip == null || ip.length() == 0 || "unknown".equalsIgnoreCase(ip)) {  
          if (ip == null || ip.length() == 0 || "unknown".equalsIgnoreCase(ip)) {  
              ip = request.getHeader("Proxy-Client-IP");  
          }  
          if (ip == null || ip.length() == 0 || "unknown".equalsIgnoreCase(ip)) {  
              ip = request.getHeader("WL-Proxy-Client-IP");  
          }  
          if (ip == null || ip.length() == 0 || "unknown".equalsIgnoreCase(ip)) {  
              ip = request.getHeader("HTTP_CLIENT_IP");  
          }  
          if (ip == null || ip.length() == 0 || "unknown".equalsIgnoreCase(ip)) {  
              ip = request.getHeader("HTTP_X_FORWARDED_FOR");  
          }  
          if (ip == null || ip.length() == 0 || "unknown".equalsIgnoreCase(ip)) {  
              ip = request.getRemoteAddr();  //非负载均衡下直接获取
          }  
      } else if (ip.length() > 15) {  
          String[] ips = ip.split(",");  
          for (int index = 0; index < ips.length; index++) {  
              String strIp = (String) ips[index];  
              if (!("unknown".equalsIgnoreCase(strIp))) {  
                  ip = strIp;  
                  break;  
              }  
          }  
      }  
      return ip;  
}
{% endhighlight %}


#### 修改配置文件

在完成接口，还没有配置拦截器前，对应的XML文件如下：

{% highlight java lineos %}
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:jaxws="http://cxf.apache.org/jaxws"
	xmlns:p="http://www.springframework.org/schema/p"
	xsi:schemaLocation="
		http://www.springframework.org/schema/beans  
		http://www.springframework.org/schema/beans/spring-beans.xsd
		http://cxf.apache.org/jaxws
		http://cxf.apache.org/schemas/jaxws.xsd">

	<import resource="classpath:META-INF/cxf/cxf.xml" />
	<import resource="classpath:META-INF/cxf/cxf-servlet.xml" />
	<import resource="classpath:META-INF/cxf/cxf-extension-soap.xml"/>

 	<jaxws:endpoint id="uumsServiceImplWs" implementor="#uumsServiceImpl" address="/uums" >  
 	</jaxws:endpoint>
</beans>  
{% endhighlight %}

这时候我们只需要在配置文件中WebService相关便签中增加拦截器：

{% highlight java lineos %}
<jaxws:inInterceptors>  
  <bean class="拦截器的实现类"/>
</jaxws:inInterceptors>
{% endhighlight %}

最后XML文件为：

{% highlight java lineos %}
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:jaxws="http://cxf.apache.org/jaxws"
	xmlns:p="http://www.springframework.org/schema/p"
	xsi:schemaLocation="
		http://www.springframework.org/schema/beans  
		http://www.springframework.org/schema/beans/spring-beans.xsd
		http://cxf.apache.org/jaxws
		http://cxf.apache.org/schemas/jaxws.xsd">

	<import resource="classpath:META-INF/cxf/cxf.xml" />
	<import resource="classpath:META-INF/cxf/cxf-servlet.xml" />
	<import resource="classpath:META-INF/cxf/cxf-extension-soap.xml"/>

 	<jaxws:endpoint id="uumsServiceImplWs" implementor="#uumsServiceImpl" address="/uums" >  
 	 	<jaxws:inInterceptors>  
 	 	 	<bean class="cn.com.dhcc.app.pub.core.interceptor.InLoggingInterceptor"/>
 	 	</jaxws:inInterceptors>
 	</jaxws:endpoint>
</beans>  
{% endhighlight %}
