---
layout: post
title:  "Message Queue (AMQ, RabbitMQ)"
date:   2022-12-05
categories: java infra
permalink: /:categories/message-queue
---

<h1>JMS</h2>

<p><a href="https://www.oracle.com/technical-resources/articles/java/intro-java-message-service.html">Java Messaging Service (JMS)</a>: is a enterprise messaging API to handle asynchronous requests or events that will be consumed by an application. <em>JMS falls under middleware, and specifically Message-Oriented Middleware (MOM), which is a relatively low-level of abstraction that runs underneath complementary layers such as database and application adapters, event processing, and business process automation.</em></p>

<p><b>Architecture</b></p>
<ul>
  <li>Provider: JMS implementation</li>
  <li>JMS clients: who send and receive messages</li>
  <li>Messages: object with information (requests or events)</li>
  <li>Administered object" preconfigured JMS object.</li>
</ul>

<p><b>Message Delivery Models</b></p>
<ul>
  <li>Point-to-Point (queue destination): deliver the message to a queue and then to the registered consumer.</li>
  <li>Publish/Subscribe (topic destination): deliver the message to all consumers subscribed to the topic destination. </li>
</ul>

<p><b>Message</b></p>
<ul>
  <li>Header: <em>information that is used for routing and identifying messages</em></li>
  <li>Properties: <em>provide values that clients can use to filter messages</em></li>
  <li>Body: <em>contains the actual data to be exchanged</em></li>
</ul>

<p><b>Sun Java System Message Queue</b>: Sun's implementation to the queue supporting point-to-point and publish/subscribe messaging models and synchronous and asynchronous messaging.</p>

<p><b>Reliable Messaging</b>: JMS can use a <u>persistent messages</u> mode, which guarantees the message is not lost and consumed only once; or <u>non-persistent messages</u> mode, which can the message can be deliverd more then once and can be lost. The second one has better performance.</p>


<br />
<h1>ActiveMQ</h2>

<blockquote>Apache ActiveMQ® is the most popular open source, multi-protocol, Java-based message broker.</blockquote>

<p>A summary of <a href="https://activemq.apache.org/getting-started">how to start</a> the activeMQ is:</p>

<pre>
1. Install
- https://activemq.apache.org/getting-started#Pre-InstallationRequirements
- Ex MAC: $brew install apache-activemq
2. Run
- Ex MAC: $/opt/homebrew/opt/activemq/bin/activemq console
3. Access: http://127.0.0.1:8161/admin/
- Login: admin; PWD: admin
4. Test produce a message:
- https://activemq.apache.org/rest
- $curl -u admin:admin -d "body=message" http://localhost:8161/api/message/TEST?type=queue
- Alternative: $curl -XPOST -d "body=message" http://admin:admin@localhost:8161/api/message?destination=queue://orders.input
5. Test consume:
- https://activemq.apache.org/rest
- wget --user admin --password admin --save-cookies cookies.txt --load-cookies cookies.txt --keep-session-cookies  http://localhost:8161/api/message/TEST\?type\=queue
- Alternative: $curl -XGET http://admin:admin@localhost:8161/api/message?destination=queue://orders.input
6. Stop
Ex MAC: $/opt/homebrew/opt/activemq/bin/activemq stop
</pre>

<p><center>
  <img src="/img/infra/activemq.png" />
</center></p>

<br />
<h3>REFERENCE</h3>

<ul>
  <li><a href="https://www.oracle.com/technical-resources/articles/java/intro-java-message-service.html">Getting Started with Java Message Service (JMS)</a></li>
  <li><a href="https://activemq.apache.org/">Apache ActiveMQ</a></li>
  <li><a href="https://www.udemy.com/course/java-messaging-service-spring-mvc-spring-boot-activemq/">Udemy - Java Messaging Service - Spring MVC, Spring Boot, ActiveMQ</a></li>
  <li><a href="https://activemq.apache.org/using-activemq">Using Apache ActiveMQ</a></li>
  <li><a href="https://activemq.apache.org/connectivity">Connectivity</a></li>
</ul>
