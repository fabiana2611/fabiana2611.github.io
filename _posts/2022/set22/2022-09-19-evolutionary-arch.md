---
layout: post
title:  "Building Evolutionary Architectures"
date:   2022-09-19
categories: arch books
permalink: /:categories/evolutionary
---

<p><center>
  <img src="/img/books/evolarch.png" />
</center></p>

<p style="text-align: justify;">The book brings the idea that, like the code, the architecture can be changed and it is inevitable. Then it develops the learning to live and work with that reality, making the architecture area aware of the organic growth.</p>

<p style="text-align: justify;"><em>One of the keys to building evolutionary architectures lies in determining natural component granularity and coupling between components to fit the capabilities they want to support via the software architecture.</em></p>

<p style="text-align: justify;">The three <a href="https://evolutionaryarchitecture.com/precis.html">evolutionary criteria</a> mention in the book are:</p>

<ul>
  <li>Incremental change: continuous delivery practices and modular architecture allowing small modifications without breaking the application. </li>
  <li>Fitness functions: <em>quantifiable function used to summarise how close a given design solution is to achieving the set aims.</em></li>
  <li>Appropriate coupling: independence of service</li>
</ul>


<h3>Evolutionary point of view in the Architecture Style</h3>

<ul>
  <li><a href="https://fabiana2611.github.io/arch/books/sw-arch-p2#Layered">Layered:</a> Monolith architecture with the advantage of isolation and separation of concerns, then any change in one layer will not affect another layer. Thinking in terms of evolving system it shows difficulties in terms of <em>incremental changes</em>. The changes that cross the layers can be a big challenge. However, the isolation is a positive point in terms of <em>guided change with fitness functions</em>. This architecture have advantages in terms of evolving system  </li>
  <li><a href="https://fabiana2611.github.io/arch/books/sw-arch-p2#Microkernel">Microkernel:</a> Monolith architecture style where there are the core and external parts, plugins. Considering the <em>Incremental change</em> characteristic, it is a good choice if the plugins are independent and can evolve. The same way, the isolation between the core and plugin is a advantage cosidering the <em>guided change with fitness functions</em> Characteristic. In terms of <em>Appropriate coupling</em> it can be desadvantage if the plugins are dependents.</li>
  <li><a href="https://fabiana2611.github.io/arch/books/sw-arch-p2#EDA">Event-Driven Architecture (EDA):</a> Distributed architecture style that uses events to communication. It can be using brokers, without a central element, and mediators, with a central element. Both cases have advantages in the three characteristics. However, the mediator has facilities related to tests and to identifies causes of errors due to the presence of a coordinator. The broker has more advantages in terms of <em>Approriate coupling</em> for having more independent components.</li>
  <li><a href="https://fabiana2611.github.io/arch/books/sw-arch-p2#SOA">Service-Oriented Architecture (SOA):</a> Distributed architecture style that use a service bus (ESB) as coordinator. It doesn't has good points when we talk about the three point used to validate the architecture (<em> incremental change, guided change and appropriate coupling</em>). Any changes need a good coordination and the tests are a challenge.
  <li><a href="https://fabiana2611.github.io/arch/books/sw-arch-p2#ServiceBased">Service-Based Architecture (SBA):</a> It is similar to microservice but with less granularity. In terms of <em>incremental change</em> it has good points like microservices because most part or changes happens by domain. The characteristic <em>guided change with fitness functions and Appropriate coupling</em> it has a negative point comparing with microservice.</li>
  <li><a href="https://fabiana2611.github.io/arch/books/sw-arch-p2#Microservice">Microservice:</a> distributed architecture designed around some directions as Continuous Delivery + logical partitioning, modeled around business domain, isolate features. It has positive points in all aspects of a evolutionary architecture.</li>
  </li>
</ul>


<br />
<h3>Videos</h3>

<table>
  <tr>
    <td><iframe src="https://www.youtube.com/embed/xJj9vgDz33U" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </td>
    <td><iframe src="https://www.youtube.com/embed/8bEsNT7jdC4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </td>
    <td><iframe src="https://www.youtube.com/embed/UV_B-ioocpY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </td>
  </tr>
</table>


<br />
<h3>Be continued...</h3>

<br />
<h3>Reference</h3>

<ul>
  <li><a href="https://www.thoughtworks.com/insights/books/building-evolutionary-architectures">The Book</a></li>
  <li><a href="https://evolutionaryarchitecture.com/">Official Page</a></li>
  <li><a href="https://www.infoq.com/articles/implementing-evolutionary-architecture/">implementing Evolutionary Architecture</a></li>
  <li><a href="https://www.infoq.com/articles/evolutionary-architecture-organizational/">Evolutionary Architecture Organizational</a></li>
  <li><a href="https://www.sqli.nl/en/blog/evolutionary-architecture">Evolutionary Architecture</a></li>
  <li><a href="https://github.com/Netflix/chaosmonkey">ChaosMonkey</a></li>
  <li><a href="https://github.com/Netflix/SimianArmy">SimiaArmy</a></li>
  <li><a href="https://github.blog/2015-12-15-move-fast/">Movie Fast</a></li>
</ul>
