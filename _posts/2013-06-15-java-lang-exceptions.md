---
layout: post
title: java.lang.exception系列
description: 主要是对java.lang下的错误进行收集，以做备忘。
category: blog
tags: java
keywords:java,lang,exception
---

	2013-06-28 10:06:17.473:WARN::handle failed
	java.lang.IllegalArgumentException: !utf8
		at org.eclipse.jetty.util.Utf8StringBuilder.append(Utf8StringBuilder.java:119)
		at org.eclipse.jetty.util.Utf8StringBuilder.append(Utf8StringBuilder.java:49)
		at org.eclipse.jetty.http.HttpURI.toUtf8String(HttpURI.java:488)
		at org.eclipse.jetty.http.HttpURI.toString(HttpURI.java:662)
		at java.lang.String.valueOf(String.java:2826)
		at java.lang.StringBuilder.append(StringBuilder.java:115)
		at org.eclipse.jetty.server.HttpConnection.handleRequest(HttpConnection.java:633)
		at org.eclipse.jetty.server.HttpConnection$RequestHandler.headerComplete(HttpConnection.java:1051)
		at org.eclipse.jetty.http.HttpParser.parseNext(HttpParser.java:590)
		at org.eclipse.jetty.http.HttpParser.parseAvailable(HttpParser.java:212)
		at org.eclipse.jetty.server.HttpConnection.handle(HttpConnection.java:426)
		at org.eclipse.jetty.io.nio.SelectChannelEndPoint.handle(SelectChannelEndPoint.java:508)
		at org.eclipse.jetty.io.nio.SelectChannelEndPoint.access$000(SelectChannelEndPoint.java:34)
		at org.eclipse.jetty.io.nio.SelectChannelEndPoint$1.run(SelectChannelEndPoint.java:40)
		at org.eclipse.jetty.util.thread.QueuedThreadPool$2.run(QueuedThreadPool.java:451)
		at java.lang.Thread.run(Thread.java:662)


这个错误是因为在`Jetty`下传递中文参数到后台,解决办法是不要传递中文参数,或者在start.ini中增加JVM启动参数([参考](http://www.oschina.net/question/174702_32759)):

	-Dorg.eclipse.jetty.util.URI.charset=GBK

----------

	Caused by: java.lang.UnsupportedClassVersionError: www/kobe/pojo/Salesman : Unsupported major.minor version 51.0 (unable to load class www.kobe.pojo.Salesman)

或者

	org.springframework.beans.factory.CannotLoadBeanClassException: Error loading class [com.skysz.app.cmcs.ynt.iface.cpmisexev.dao.hibernate3.OdfToOrgYntDaoImpl] for bean with name 'odfToOrgYntDao' defined in class path resource [spring-ynt.xml]: problem with class file or dependent class; nested exception is java.lang.UnsupportedClassVersionError: Bad version number in .class file

这个错误是因为你使用的JDK和你的编译级别不同，如图：  
你使用的JDK：  
![java-build-path](http://dolphinboy.me/resources/java-build-path.png)

你的编译级别：  
![java-compiler](http://dolphinboy.me/resources/java-compiler.png)

>注意：如果你使用了Maven那么，如果你的父项目和你的子项目使用的JDK不同，那么每次同步代码之后你可能都要重新编译一下项目，有时候重新编译也没用，那你就干脆重启一下Eclipse吧，有可能会莫名其妙的好了。


本文持续更新中...