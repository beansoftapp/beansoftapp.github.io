---
id: 3021
title: WEBLOGIC JMS配置入门
date: 2012-09-05T21:38:17+00:00
author: 刘长炯
layout: post
guid: http://www.beansoft.biz/?p=3021
permalink: '/2012/09/05/weblogic-jms%e9%85%8d%e7%bd%ae%e5%85%a5%e9%97%a8/'
views:
  - "3420"
image: /wp-content/uploads/2012/04/WebLogic.png
categories:
  - WebLogic
tags:
  - JMS
  - WebLogic
---
WEBLOGIC JMS 配置.pdf 阅读及下载地址: [https://skydrive.live.com/redir?resid=519B3F7AA2172030!1502](https://skydrive.live.com/redir?resid=519B3F7AA2172030!1502 "https://skydrive.live.com/redir?resid=519B3F7AA2172030!1502")

摘要:

&#160;

WEBLOGIC JMS 配置入门   
作者: BeanSoft   
来源: WebLogic 中文博客   
日期: 2012-8   
目录   
WEBLOGIC JMS 配置入门&#160; &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.&#160; 1   
JMS 概念简介&#160; &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;..&#160; 2   
配置 JMS 队列的步骤(点对点模式):&#160; &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;..&#160; 3   
1.&#160; 配置 JMS 服务器&#160; &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;..&#160; 3   
2. 创建 JMS 系统模块来存放 队列或主题.&#160; &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;.&#160; 6   
3. 创建 子部属.&#160; &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#160; 9   
4. 创建 JMS 连接工厂.&#160; &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;..&#160; 11   
5. 创建 JMS 队列 (点对点消息模式)&#160; &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;..&#160; 16   
6. 创建 JMS 主题&#160; &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#160; 19   
7. 参考资料&#160; &#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;&#8230;..&#160; 22   
本文将会展示如何进行简单的 WebLogic JMS 配置 .   
JMS 概念简介   
JMS 支持两种消息模式: point-to-point (PTP,点对点) 和 publish/subscribe (pub/sub, 发布/订阅). 这些消息模式非常类似, 主要区别简列如下:   
&#160; 点对点消息模式有且只能有一个收件人收到传送的消息.   
&#160; 发布/订阅模式可以将一条消息传送到多个收件人.   
点对点消息模式可以使一个应用程序向另一个发送消息. 点对点消息应用通过使用 Queues(队列) 来发送和接收消息. 队列发送者 (producer,生产者) 向指定的   
队列发送消息. 队列接收者 (consumer,消费者) 从指定的队列接收消息.   
下图展示了点对点消息模式:   
配置 JMS 队列的步骤(点对点模式):   
1.&#160; 配置 JMS 服务器   
a.&#160; 登录进入 WebLogic 管理控制台, 在域结构中选择 服务  消息传送  JMS 服务器.   
JMS 服务器 是队列或主题的管理容器.   
b. 如下图所示, 创建一个 JMS 服务器. 

c. 将 JMS Server 部署目标设置为任意一个 WebLogic Server. 

&#160;

&#8230;&#8230;&#8230;&#8230;&#8230;

转载请注明：[WebLogic Android 博客](http://www.beansoft.biz) &raquo; [WEBLOGIC JMS配置入门](http://www.beansoft.biz/2012/09/05/weblogic-jms%e9%85%8d%e7%bd%ae%e5%85%a5%e9%97%a8/)