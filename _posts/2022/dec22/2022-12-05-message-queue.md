---
layout: post
title:  "Message Queue"
date:   2022-12-05
categories: java infra
permalink: /:categories/message-queue
---

<h1>JMS</h1>

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
<h1>ActiveMQ</h1>

<blockquote>Apache ActiveMQ® is the most popular open source, multi-protocol, Java-based message broker.</blockquote>

<p>A summary of <a href="https://activemq.apache.org/getting-started">how to start</a> the activeMQ is:</p>

<ol>
  <li><a href="https://activemq.apache.org/getting-started#Pre-InstallationRequirements">Install</a>
    <ul>
      <li>Ex MAC: $brew install apache-activemq</li>
    </ul>
  </li>
  <li>Run
    <ul>
      <li>Ex MAC: $/opt/homebrew/opt/activemq/bin/activemq console</li>
    </ul>
  </li>
  <li>Access: http://127.0.0.1:8161/admin/
    <ul>
      <li>Login: admin; PWD: admin</li>
    </ul>
  </li>
  <li><a href="https://activemq.apache.org/rest">Test produce a message</a>
    <ul>
      <li>$curl -u admin:admin -d "body=message" http://localhost:8161/api/message/TEST?type=queue</li>
      <li>Alternative: $curl -XPOST -d "body=message" http://admin:admin@localhost:8161/api/message?destination=queue://orders.input</li>
    </ul>
  </li>
  <li><a href="https://activemq.apache.org/rest">Test consume a message</a>
    <ul>
      <li>wget --user admin --password admin --save-cookies cookies.txt --load-cookies cookies.txt --keep-session-cookies  http://localhost:8161/api/message/TEST\?type\=queue</li>
      <li>Alternative: $curl -XGET http://admin:admin@localhost:8161/api/message?destination=queue://orders.input</li>
    </ul>
  </li>
  <li>Stop
    <ul>
      <li>Ex MAC: $/opt/homebrew/opt/activemq/bin/activemq stop</li>
    </ul>
  </li>
</ol>

<p>The figure shows the first moment with the produced message (right side) and then value '0' to message after to be consumed.</p>

<p><center>
  <img src="/img/infra/activemq.png" />
</center></p>

<h1>Example</h1>

<p>Here is an <a href="https://activemq.apache.org/hello-world">example</a> of an implementation how to produce and consume a message to and from queue.</p>

<p><center>
  <img src="/img/infra/activemq_example.png" />
</center></p>

<p>An alternative is to use jmsTemplate. Here is an example for Producer.</p>

{% highlight ruby %}
JmsTemplate jmsTemplate = new JmsTemplate();
		jmsTemplate.setConnectionFactory(connectionFactory);

jmsTemplate.send(queue, new MessageCreator() {    			
  @Override
  public Message createMessage(Session session) throws JMSException {
    ObjectMessage message = session.createObjectMessage(messageStr);
      return message;
    }
});    
{% endhighlight %}

<p>Attention the URI used as parameter to ActiveMQConnectionFactory. It is beginning by "vm". It is the <a href="https://activemq.apache.org/topologies">topology</a> that can be:</p>

<ul>
  <li>VM (vm://localhost/foo): manage different JMS groups inside the same JVM</li>
  <li>Client-Server (tcp://somehost:port): connect the message Broker using TCP, SSL, NIO, etc.</li>
  <li>Embedded Broker: <em>communcation between the client and server (broker) are all within the same JVM and so do not use real networking</em></li>
  <li>Peer to Peer: <em>This allows peer based clusters to be created where there is no server - just clients connecting together.</em></li>
  <li>JXTA (jxta://hostname:port): <em>use the full JXTA stack for negotiating NAT and across firewalls and so forth for creating a true peer based JMS network.</em></li>
</ul>


<br />
<h3>REFERENCE</h3>

<ul>
  <li><a href="https://www.oracle.com/technical-resources/articles/java/intro-java-message-service.html">Getting Started with Java Message Service (JMS)</a></li>
  <li><a href="https://activemq.apache.org/">Apache ActiveMQ</a></li>
  <li><a href="https://www.udemy.com/course/java-messaging-service-spring-mvc-spring-boot-activemq/">Udemy - Java Messaging Service - Spring MVC, Spring Boot, ActiveMQ</a></li>
  <li><a href="https://activemq.apache.org/using-activemq">Using Apache ActiveMQ</a></li>
  <li><a href="https://activemq.apache.org/connectivity">Connectivity</a></li>
</ul>
