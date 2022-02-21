---
layout: post
title:  "Spring Integration"
date:   "2021-09-25"
category: "spring"
permalink: /:categories/spring-integration
---

<p style="text-align: justify;">The Spring gives a great support to build enterprise applications making the developers more productive and improve the testability and portability of the application. Sprint Integration comes to help in this goal.</p>

<blockquote>
Spring Integration extends the Spring programming model into the messaging domain and builds upon Spring’s existing enterprise integration support to provide an even higher level of abstraction. It supports <b>message-driven architectures</b> where inversion of control applies to runtime concerns, such as when certain business logic should run and where the response should be sent. It supports <b>routing and transformation of messages</b> so that different transports and different data formats can be integrated without impacting testability. In other words, the messaging and integration concerns are handled by the framework. Business components are further isolated from the infrastructure, and developers are relieved of complex integration responsibilities. <a href="https://docs.spring.io/spring-integration/docs/current/reference/html/overview.html#overview-background">[1]</a>
</blockquote>

<p style="text-align: justify;">The Spring follows a layered architecture (vertical perspective) to separate the concerning and to promote a low coupling. The message-drive architecture used by Spring add a horizontal perspective. And they are not mutually exclusive.</p>

<p>The message system has filters and pipes:</p>
<ul>
	<li><em>The <b>filters</b> represent any components capable of producing or consuming messages. Managed within a layer that is logically above the application’s service layer, interacting with those services through interfaces in much the same way that a web tier would.</em></li>
	<li><em>The <b>pipes</b> transport the messages between filters. It should be encapsulated in a layer whose contracts are defined as interfaces. </em></li>
</ul>

<p><center>
	<img src="/img/spring/filterpipes.png"/><br />
</center></p>

<br/>
<h1>Main components</h1>

<ul>
	<li><b>Message:</b> generic wrapper for any Java object combined with metadata  (header + payload)</li>
	<li><b>Message Channel:</b> it is the pipe that receive the message from a producer and send to a unique consumer or send the message in a broadcast way.</li>
	<li><b>Message Endpoint:</b> It is the filter. It handles the message and it is mapped to message channels. It isolates the application code from the infrastructure. It is part of Enterprise Integration Patterns. Here are types of endpoints:
		<ul>
			<li><u>Message Transformer</u> changes the message (content, header or structure)</li>
			<li><u>Message Filter</u> verifies is the message can continue its flow or not to the output channel.</li>
			<li><u>Message Router</u> selects the right channel to the message.</li>
			<li><u>Splitter</u> splits the message and send to its output channel</li>
			<li><u>Aggregator</u> receives multiple messages and combine them to a single message.</li>
			<li><u>Service Activator</u> connects a service instance to the message system.</li>
			<li><u>Channel Adapter</u> connects a message channel to a system or transport</li>
		</ul>
		</li>
</ul>


<p><center>
	<img src="/img/spring/messagearch.png"/><br />
	<em>From Spring Doc <a href="https://docs.spring.io/spring-integration/docs/current/reference/html/overview.html#overview-components">[2]</a></em>
</center></p>


<br/>
<h1>Play List</h1>

<table>
	<tr>
		<th><a href="https://www.youtube.com/watch?v=oQ2CBtYrSYo&list=PLO0KWyajXMh6HbVTnf7YqwbEeZU6kuKJa&index=1">Simple Programming</a></th>
		<th><a href="https://www.youtube.com/watch?v=icIosLjHu3I&list=PLr2Nvl0YJxI5-QasO8XY5m8Fy34kG-YF2" >Intertech</a></th>
	</tr>
	<tr>
		<td><iframe width="100%" height="250" src="https://www.youtube.com/embed/lla5jtKIn10" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
		<td><iframe width="100%" height="250" src="https://www.youtube.com/embed/icIosLjHu3I" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
	</tr>
</table>

{% highlight ruby %}
{% endhighlight %}


<h3>References</h3>

<ul>
	<li><a href="https://docs.spring.io/spring-integration/docs/current/reference/html/overview.html#overview" >Overview of Spring Integration Framework</a></li>
  <li><a href="https://www.enterpriseintegrationpatterns.com/docs/jaoo_hohpeg_enterpriseintegrationpatterns.pdf" >Enterprise Integration Patterns</a></li>
	<li><a href="https://www.baeldung.com/spring-integration" >Introduction to Spring Integration</a></li>
</ul>
