---
layout: post
title: log4j源码学习
date: 2015-10-25 17:53
tags:
  - tech
  - java
  - log4j

---
#log4j分析
###配置文件加载
在启动的时候org.apache.log4j.LogManager中的static方法会加载log4j的配置文件,如果指定了log4j.configuration,则从指定的文件加载,否则就先读取log4j.xml格式的配置文件,如果没有再读取log4j.properties的文件,如果需要测试此特性,可以在运行的时候加上`-Dlog4j.configuration=aa.properties`即可.  

在很多情况下是结合spring使用的,在web.xml中的配置文件如下:

```xml
	<context-param>
		<param-name>log4jConfigLocation</param-name>
		<param-value>classpath:log4j.xml</param-value>
	</context-param>

	<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>
			classpath:spring-master-all.xml
		</param-value>
	</context-param>

	<listener>
		<listener-class>org.springframework.web.util.Log4jConfigListener</listener-class>
	</listener>
```

从源代码中可以看出就是调用log4j的PropertyConfigurator.configure方法.  

```java
	public static void initLogging(String location) throws FileNotFoundException {
		String resolvedLocation = SystemPropertyUtils.resolvePlaceholders(location);
		URL url = ResourceUtils.getURL(resolvedLocation);
		if (ResourceUtils.URL_PROTOCOL_FILE.equals(url.getProtocol()) && !ResourceUtils.getFile(url).exists()) {
			throw new FileNotFoundException("Log4j config file [" + resolvedLocation + "] not found");
		}

		if (resolvedLocation.toLowerCase().endsWith(XML_FILE_EXTENSION)) {
			DOMConfigurator.configure(url);
		}
		else {
			PropertyConfigurator.configure(url);
		}
	}
```
