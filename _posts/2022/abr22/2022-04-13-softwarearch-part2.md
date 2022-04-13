---
layout: post
title:  "Fundamentals of Software Architecture - Part II"
date:   2022-04-13
categories: arch
permalink: /:categories/sw-arch-p2
---

<p style="text-align: justify;">Continuing the study of Architecture's fundamentals started in last <a href="https://fabiana2611.github.io/arch/sw-arch">post (Part I)</a>... Here I'll list some styles covered by the <a href="https://fundamentalsofsoftwarearchitecture.com/">book</a>.</p>

<p style="text-align: justify;">The book defines the difference between style and pattern. The style is a kind of the big picture while the <a href="https://fabiana2611.github.io/arch/architecture">patterns</a> are solutions that can be used inside the style. Sometimes it's confusing because many patterns have the name of the styles.</p>

<blockquote>Architecture Style is the overarching structure of how the user interface and backend source are organized and how that source code interact with datastore.</blockquote>

<blockquote>Architecture patterns are lower-level design structures that help form specific solutions within an architecture style. </blockquote>

<p><center>
  <iframe width="560" height="315" src="https://www.youtube.com/embed/I-yBv72RCeA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center></p>

<p style="text-align: justify;">The book classified the styles in two main types: <a href="https://fabiana2611.github.io/arch/architecture#Monolithic">monolithic</a> (e.g Layer, Pipeline, <a href="https://fabiana2611.github.io/arch/architecture#Microkernel">Microkernel</a>) and distributed (e.g. SBA, <a href="https://fabiana2611.github.io/arch/architecture#SOA">SOA</a>, EDA, <a href="https://fabiana2611.github.io/arch/architecture#Microservice">microservice</a>).</p>


<p style="text-align: justify;">The Distributed version has benefits such as performance, scalability, availability. However, there are some points in distributed architecture that should be raising at the moment of the choice: (1) <a href="https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing">Fallacies of distributed computing</a> and (2) the trade-off. The distributed solution comes together with some points of attention: network reliability, latency, bandwidth, security, topology, the admins are necessary to be in touch to make it works, the infrastructure cost.</p>

<p style="text-align: justify;">As challenges to the distributed solution are: service granularity, shared functionality, workflow management, communication protocol, monolithic decomposition, contract management, distributed transaction, database style, architecture style.</p>

<p>None of both approaches is the bad guy. The decision has to be guided by the business.</p>

<table>
  <tr>
    <td>Fallacies of distributed computing</td>
    <td>Challenges of Distributed Architectures</td>
  </tr>
  <tr>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/UZxLYv5RFyI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/sv-3lmrJ2M8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>

  <tr>
    <td>When Should You Replace Your Architecture?</td>
    <td>03 Architecture Refactoring</td>
  </tr>
  <tr>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/nxmxp4_pdm8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/aQlQ3hTB1TU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>
</table>



<h2>Styles</h2>


<h3>Client/Server</h3>

<p style="text-align: justify;">One of the fundamental style is Client/server which has two tiers.</p>

<blockquote>client-server architecture, architecture of a computer network in which many clients (remote processors) request and receive service from a centralized server (host computer).<a href="https://www.britannica.com/technology/client-server-architecture">[1]</a></blockquote>

<p><center>
  <iframe width="360" height="215" src="https://www.youtube.com/embed/L5BlpPU_muY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center></p>

<br/>
<h3>Layered</h3>

<p>The <a href="https://fabiana2611.github.io/arch/architecture#Layered">Layered</a> style is a classical monolithic style.</p>
<ul>
  <li>Good choice of small and simple applications or websites</li>
  <li>can be a starting point when don't know how the arch will be.</li>
  <li>It has highlights regarding over cost and simplicity but it's not very good with deployability, fault tolerance, modularity, and scalability.</li>
</ul>


<p>Some rules:</p>
<ul>
  <li>Closed layer: requests moves top-down</li>
  <li>Separation of concerns: effective roles and responsibility models</li>
  <li>Concepts of isolation: changes made one layer should not impact other layer.</li>
</ul>

<p><center>
  <iframe width="360" height="215" src="https://www.youtube.com/embed/BCXcIllT7Lc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center></p>

<br/>
<h3>Pipeline</h3>

<blockquote>Pipe and Filter is a simple architectural style that connects a number of components that process a stream of data, each connected to the next component in the processing pipeline via a Pipe.<a href="https://www.oreilly.com/library/view/software-architecture-with/9781786468529/ch08s04.html">[2]</a><a href="https://www.oreilly.com/library/view/fundamentals-of-software/9781492043447/ch11.xhtml">[3]</a></blockquote>

<p><em>Filters are components responsible for transform data and process the input they receive. Pipes are connectors for the stream of data being transformed, each connected to the next component in the pipeline.</em><a href="https://syedhasan010.medium.com/pipe-and-filter-architecture-bd7babdb908">[4]</a>. Types of filters are: Producer, Transformer, Tester and Consumer.</p>

<p>One example where it is using is in <a href="https://fabiana2611.github.io/java/stream">Stream from Java</a>.</p>

<p>The highlights of this style is the cost and simplicity. Not good to scalability or fault tolerance.</p>

<table>
  <tr>
    <td><img src="/img/architecture/pipeline.png" width="70%" height="70%" /></td>
    <td><iframe src="https://www.youtube.com/embed/l9AGpQSc4s8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>
</table>

<br/>
<h3>Microkernel</h3>

<p style="text-align: justify;">The <a href="https://fabiana2611.github.io/arch/architecture#Microkernel">Microkernel</a> style has the idea of a core component with the minimal necessary to work and external parts (plugins) with extra functionalities.</p>

<p style="text-align: justify;">The highlights of this style is the cost and simplicity. Not good to scalability or fault tolerance.</p>

<p><center>
  <iframe width="360" height="215" src="https://www.youtube.com/embed/h3icQDMRLd8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center></p>

<br/>
<h3>Service-based Architecture</h3>

<p><em>Both <a href="https://fabiana2611.github.io/arch/architecture#Microservice">microservices</a> architecture and <a href="https://fabiana2611.github.io/arch/architecture#SOA">SOA</a> are considered service-based architectures, meaning that they are architecture patterns that place a heavy emphasis on services as the primary architecture component used to implement and perform business and nonbusiness functionality. "</em><a href="https://www.oreilly.com/library/view/microservices-vs-service-oriented/9781491975657/ch01.html">[5]</a></p>

<ul>
  <li>distributed architectures</li>
  <li>service components accessed remotely</li>
  <li>highlights: scalability, decoupling, and control over development, testing, and deployment</li>
  <li>It is a distributed architecture so it allows change control and easier maintenance, loosely coupled and modular applications</li>
  <li>Trade-off: increased complexity and cost, service contracts, choosing the remote-access protocol, availability of services, security (authenticated and authorized), distributed transactions (ACID), etc.</li>
</ul>

<p><center>
  <iframe src="https://www.youtube.com/embed/xkr5nGJYx_U" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center></p>


<br/>
<h3>Event-Driven Architecture</h3>

<blockquote>An event-driven architecture consists of event producers that generate a stream of events, and event consumers that listen for the events.<a href="https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/event-driven">[2]</a></blockquote>

<p>Some notes about this style:</p>
<ul>
  <li>Popular to distributed asynchronous architectures</li>
  <li>Good performance and scalability</li>
  <li>Can be adapted to small or big applications</li>
  <li>Can be implemented using request-based model where an orchestrator manage the requests</li>
  <li>Can be used inside other style (e.g. microservice)</li>
  <li>Good response to a dynamic user content</li>
  <li>It's hard to have the control of the workflow or error handling</li>
  <li>Hard to test</li>
</ul>

<p style="text-align: justify;">It can be Request-based and event-based. The first one has more control over the workflow (request/response). The second one has high level of responsiveness and scalability.<a href="https://www.techtalksbyanvita.com/post/event-driven-vs-request-driven-rest-architecture">[3]</a></p>


<p>In terms of <b>topology</b> it can be:</p>
<p><u>1 Mediator</u></p>
<ul>
  <li>It has a central part, the mediator to coordinate the workflow</li>
  <li>Can maintain event state and manage error handling, recoverability, and restart capability</li>
  <li>Components: an initiating event, an event queue, an event mediator, event channels, and event processors</li>
  <li>The implementation can have more than one mediator</li>
  <li>Example: Apache Camel</li>
</ul>

<p><u>2 Broker</u></p>
<ul>
  <li>No central event Mediator</li>
  <li>Distributed flow - like a broadcast</li>
  <li>Example: RabbitMQ, ActiveMQ,</li>
  <li>Useful when you have a relatively simple event processing flow and don't need an orchestration</li>
  <li>Components: initiating event, event broker, event processor, and processing event</li>
  <li>The event broker has all of the event channels used within the event flow</li>
  <li>easy to add a new event processor</li>
</ul>

<p>Some <b>Characteristic</b> are:</p>
<ul>
  <li>Asynchronous Capabilities: increasing responsiveness but is hard address error condition</li>
  <li>Error Handling: workflow event pattern used in asynchronous workflow to help in the weakness from this style.  When a error happens the event delegate it to the workflow processor and go to the next message in the queue</li>
  <li>Preventing Data Loss: out-of-box technics to prevent data loss (broker can storage the message, keep messages in the queue with client ID)</li>
  <li>Broadcast Capabilities</li>
  <li>Request-Reply</li>
</ul>

<p><b>Highlights:</b> evolutionary, fault tolerance, performance, scalability</p>
<p><b>Bad points:</b> simplicity, testability, deployability, reliability </p>

<table>
  <tr>
    <td>Request/Reply Pattern</td>
    <td>Importance of Event Driven Architecture</td>
  </tr>
  <tr>
    <td><iframe src="https://www.youtube.com/embed/3bxAm3XIFmk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
    <td><iframe src="https://www.youtube.com/embed/WCoLXZkc33Q" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>
  <tr>
    <td>The Pros and Cons</td>
    <td>Microservices vs Event-Driven Architecture</td>
  </tr>
  <tr>
    <td><iframe src="https://www.youtube.com/embed/M6CDaZ1cxIs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
    <td><iframe src="https://www.youtube.com/embed/M07btP86Ybk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>
</table>

<br/>
<h3>Be continued...</h3>
<p>Space-based Architecture...</p>
<p>Orchestration-Driven Service-Oriented Architecture...</p>
<p>Microservice Architecture...</p>
<p>Microservice Architecture...</p>

<h2>All together</h2>

<p><center>
  <img src="/img/architecture/alltogether1.png" />
  <br />
  <em>From: <a href="https://youtu.be/fS8Ejg3qsJI">Mark's videos</a></em>
</center></p>
<p><center>
  <img src="/img/architecture/alltogether.png" />
  <br />
  <em>From: <a href="https://youtu.be/nxmxp4_pdm8">Mark's videos</a></em>
</center></p>

<h2>Interesting Videos</h2>

<table>
  <tr>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/aQlQ3hTB1TU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/es25987MTzc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>
</table>

<h2>References</h2>
<ul>
  <li><a href="https://fundamentalsofsoftwarearchitecture.com/">Fundamentals of Software Architecture - Mark Richards & Neal Ford</a></li>
  <li><a href="https://developertoarchitect.com/">Developer to Architect</a></li>
  <li><a href="https://www.infoq.com/news/2016/10/service-based-architecture/">Service-Based Architecture as an Alternative to Microservice Architecture</a></li>
  <li><a href="https://solace.com/what-is-event-driven-architecture/">What is Event-Driven Architecture?</a></li>
  <li><a href="https://www.techtalksbyanvita.com/post/event-driven-vs-request-driven-rest-architecture">Event-Driven vs Request-Driven (RESTful) Architecture in Microservices</a></li>
  <li><a href="https://dev.to/desi109/architectural-styles-by-examples-387b">Architectural Styles (by examples)</a></li>
  <li><a href="https://docs.microsoft.com/en-us/azure/architecture/patterns/pipes-and-filters">Pipes and Filters pattern</a></li>
</ul>
