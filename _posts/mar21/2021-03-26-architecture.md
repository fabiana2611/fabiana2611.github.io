---
layout: post
title:  "Architecture"
date:   2021-03-26
categories: foundation
permalink: /:categories/architecture
---

<p style="text-align: justify;"><blockquote>Good architecture is something that supports its own evolution, and is deeply intertwined with programming <a href="https://martinfowler.com/architecture/">[Martin Fowler]</a></blockquote></p>

<p style="text-align: justify;">Here I'll list a set of architecture patterns distributed in three different categories: Landscape, Structure and UI. The first one is a general way to define the solution (as a map of a city), the second one is more specific how to separate parts of the application (as a house), and the third one is related to UI.</p>

<table>

<tr>
<th>Landscape</th>
<th>Structure</th>
<th>UI</th>
</tr>
<tr>
<td>
<li><a href="#Monolithic">Monolithic</a></li>
<li><a href="https://fabiana2611.github.io/foundation/architecture/#NTier">N-Tier</a></li>
<li><a href="https://fabiana2611.github.io/foundation/architecture/#SOA">SOA</a></li>
<li><a href="https://fabiana2611.github.io/foundation/architecture/#Microservice">Microservice</a></li>
<li><a href="https://fabiana2611.github.io/foundation/architecture/#Serveless">Serveless</a></li>
<li><a href="https://fabiana2611.github.io/foundation/architecture/#P2P">Peer-To-Peer</a></li>
</td>
<td>
<li><a href="https://fabiana2611.github.io/foundation/architecture/#Layered">Layered</a></li>
<li><a href="https://fabiana2611.github.io/foundation/architecture/#Microkernel">Microkernel</a></li>
<li><a href="https://fabiana2611.github.io/foundation/architecture/#EventSourcing">Event Sourcing</a></li>
<li><a href="https://fabiana2611.github.io/foundation/architecture/#CQRS">CQRS</a></li>
<li><a href="https://fabiana2611.github.io/foundation/architecture/#Hexagonal">Hexagonal</a></li>
</td>
<td>
<li><a href="https://fabiana2611.github.io/foundation/architecture/#MVC">MVC</a></li>
<li><a href="https://fabiana2611.github.io/foundation/architecture/#MVP">MVP</a></li>
<li><a href="#MVVM">MVVM</a></li>
</td>
</tr>
</table>


<h2>Landscape</h2>

<h1><u id="Monolithic">Monolith</u></h1>

<p style="text-align: justify;">The idea is to have all parts of code together, or self-contained. All parts will create one deployment unit. It is modular software where all components are together to be compiled and executed. It means if one part is updated the whole application should be compiled and deployed again. However, comparing with a modular application, it has better throughput and is easier to test and debug. </p>

<p><center>
  <img src="/img/architecture/monolithic.png" width="190" height="200"/><br/>
  <em>Sources: <a href="https://clockwise.software/blog/monolithic-architecture-vs-microservices-comparison/">Igor Omelchenko (clockwise)</a></em>
</center></p>

<p>
<b> References </b>
<ul>
<li><a href="http://www.codingthearchitecture.com/2014/11/19/what_is_a_monolith.html">Module Monolith</a></li>
<li><a href="https://www.kamilgrzybek.com/design/modular-monolith-primer/">Modular Monolith: A Primer</a></li>
<li><a href="https://microservices.io/patterns/monolithic.html">Pattern: Monolithic Architecture</a></li>
</ul>
</p>

<br/>

<h1><u id="NTier">N-Tier</u></h1>

<blockquote>N-tier application architecture provides a model by which developers can create flexible and reusable applications. A three-tier architecture is typically composed of a presentation tier, a domain logic tier, and a data storage tier.  (Wiki)</blockquote>

<b>Difference between layer and tier:</b> the first one concerns a logical solution, while a tier is a physical solution.

<center><img src="/img/architecture/ntiers.png" width="130" height="200"/></center>

<p>
<b> References </b>
<ul>
<li><a href="https://en.wikipedia.org/wiki/Multitier_architecture#cite_note-3">Wiki</a></li>
<li><a href="https://www.guru99.com/n-tier-architecture-system-concepts-tips.html">N Tier(Multi-Tier), 3-Tier, 2-Tier Architecture with EXAMPLE</a></li>
</ul>
</p>

<br/>

<h1><u id="SOA">SOA</u></h1>

<p style="text-align: justify;">The service-oriented architecture has multiple services where each one is a business activity. Those services can communicate with each other because of a contract standardization, as SOAP. The SOA has ESB (enterprise service bus) to centralize the communication of the services, doing routing, translate data, etc. The services are loosely coupled, scalability, no duplication of functionality. However, cannot be so agile to develop.</p>

<center>
  <img src="/img/architecture/soa.png" width="430" height="300"/><br/>
  <em>Sources: <a href="https://subscription.packtpub.com/book/application_development/9781789133608/1/ch01lvl1sec12/service-oriented-architecture-soa">Packt</a></em>
</center>

<p>
<b> References </b>
<ul>
<li><a href="https://www.ibm.com/cloud/learn/soa">IBM: SOA (Service-Oriented Architecture)</a></li>
<li><a href="https://www.geeksforgeeks.org/service-oriented-architecture/">GeekForGeeks: Service-Oriented Architecture</a></li>
<li><a href="https://www.guru99.com/soa-principles.html">Guru99: Service-Oriented Architecture</a></li>
</ul>
</p>

<br/>

<h1><u id="Microservice">Microservice</u></h1>

<p style="text-align: justify;">It is a natural evolution of the SOA. In this case, the ESB doesn't exist anymore. Microservice can be more agile, easier to develop and deploy new versions. As well, it gives low-coupled modules. Problems in some services will not impact other services. It also comes with some challenges as debug the application and ensure security between the services communication. </p>

<p><center>
  <img src="/img/architecture/microservice.png" width="300" height="300"/><br/>
  <em>Sources: <a href="https://clockwise.software/blog/monolithic-architecture-vs-microservices-comparison/">Igor Omelchenko (clockwise)</a></em>
</center></p>

<p>
<b> References </b>
<ul>
<li><a href="https://microservices.io/patterns/microservices.html">Pattern: Microservice Architecture</a></li>
<li><a href="https://martinfowler.com/articles/microservices.html">Martin Fowler - Microservices</a></li>
<li><a href="https://www.redhat.com/en/topics/microservices/what-are-microservices">RedHat: What are microservices?</a></li>
<li><a href="https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/microservices">Microsoft: Microservices architecture style</a></li>
</ul>
</p>

<br/>

<h1><u id="Serveless">Serveless</u></h1>

<blockquote>
Serverless architectures are application designs that incorporate third-party “Backend as a Service” (BaaS) services, and/or that include custom code run in managed, ephemeral containers on a “Functions as a Service” (FaaS) platform. [Martin Fowler]</blockquote>

<blockquote>Serverless is a cloud-native development model that allows developers to build and run applications without having to manage servers.[RedHat]</blockquote>

<p><em><b>BaaS</b> gives developers access to a variety of third-party services and apps.[RedHat]</em></p>

<p><em><b>Function-as-a-Service (FaaS)</b> is an event-driven computing execution model where developers write logic that is deployed in containers fully managed by a platform, then executed on demand.[RedHat] </em></p>

<p><center>
  <img src="/img/architecture/serveless.png" width="500" height="270"/><br/>
  <em>Source: <a href="https://www.gocd.org/2017/06/26/serverless-architecture-continuous-delivery/">Robin Weston (gocd.org/)</a></em>
</center></p>


<p>
<b> References </b>
<ul>
<li><a href="https://martinfowler.com/articles/serverless.html">Martin Fowler - Serveless</a></li>
<li><a href="https://www.redhat.com/en/topics/cloud-native-apps/what-is-serverless">RedHat - Serveless</a></li>
<li><a href="https://www.gocd.org/2017/06/26/serverless-architecture-continuous-delivery/">Serverless Architectures and Continuous Delivery</a></li>
</ul>
</p>

<br/>

<h1><u id="P2P">Peer-to-Peer</u></h1>

The P2P architecture is a commonly used computer networking architecture where:

<blockquote>The same device acts as a client and as a server in this arrangement. In its pure form, there is no separate server or centralized point of control. This means that every client also simultaneously acts as a server. Therefore all devices connected to peer-to-peer architecture can simultaneously initiate requests and fulfill requests from each other. [ScienceDirect]</blockquote>

<p><center>
  <img src="/img/architecture/p2p.png" width="500" height="300"/><br/>
</center></p>

<p>
<b> References </b>
<ul>
<li><a href="https://www.sciencedirect.com/topics/computer-science/peer-to-peer-architectures">ScienceDirect - Peer-to-Peer Architectures</a></li>
</ul>
</p>


<br/>

<h2>Structure</h2>

<h1><u id="Layered">Layered</u></h1>

<p style="text-align: justify;">The application can have many layers and each one has a distinct responsibility, having as a feature the separation of concerns. Also, the requests go through layers from the direction up to down. The idea is that the layer can go down in the sequence of the layer, but not to call a super layer.  It is easy to organize but needs to write lots of code. </p>

<p style="text-align: justify;"> Generically, there ate five layers, not mandatory. You will decide the best choice for your application.</p>

<center><img src="/img/architecture/layer.png" width="130" height="300"/></center>

<p>
<b> References </b>
<ul>
<li><a href="https://www.oreilly.com/library/view/software-architecture-patterns/9781491971437/ch01.html">Chapter 1. Layered Architecture</a></li>
</ul>
</p>

<br/>

<h1><u id="Microkernel">Microkernel</u></h1>

<p style="text-align: justify;">It is the plugin pattern, where the main part is the core which is connected to many plugins. The idea is to create a package and let it available to be used (product-based application). So, this pattern makes it possible to add new functionality by just plug an extension. This architecture is very flexible, the core and extensions can be developed by different teams, which makes it easy to turn off some functionality in runtime. However, the core API might not fit future plugins and there are no guarantees about the plugins. Also, at the same time might not be so clear what is the core and what is extensions. This pattern can be seen on browser extensions or data processing, for example.</p>

<center><img src="/img/architecture/microkernel.png" width="330" height="300"/></center>

<p>
<b> References </b>
<ul>
<li><a href="https://www.oreilly.com/library/view/software-architecture-patterns/9781491971437/ch03.html">O'Reilly -  Chapter 3. Microkernel Architecture</a></li>
<li><a href="https://www.guru99.com/microkernel-in-operating-systems.html">Guru99 - Microkernel in Operating System: Architecture, Advantages</a></li>
</ul>
</p>

<br/>

<h1><u id="EventSourcing">Event Sourcing</u></h1>

<p>It store events instead current state.This pattern allow track what happen to a entity by events. One use is audit trail.</p>

<blockquote>Event Sourcing ensures that all changes to application state are stored as a sequence of events. Not just can we query these events, we can also use the event log to reconstruct past states, and as a foundation to automatically adjust the state to cope with retroactive changes.[Martin Fowler]</blockquote>

<p><center><img src="/img/architecture/eventsourcing.png" width="690" height="300"/></center></p>

<p>
<b> References </b>
<ul>
<li><a href="https://martinfowler.com/eaaDev/EventSourcing.html">Martin Fowler -  Event Sourcing</a></li>
<li><a href="https://eventuate.io/whyeventsourcing.html">About event sourcing</a></li>
<li><a href="https://arkwright.github.io/event-sourcing.html">May the source be with you</a></li>
<li><a href="https://microservices.io/patterns/data/event-sourcing.html">Pattern: Event sourcing</a></li>
</ul>
</p>

<br/>

<h1><u id="CQRS">Command and Query Responsibility Segregation (CQRS)</u></h1>

<p style="text-align: justify;">This pattern will separate two distinct models: ready/query (get data - return a DTO) and write/command (insert, update, delete - return an event). It allows scenario-specific queries, improving performance and simplifies the queries. It is possible to have a database to read and others to write to improve the performance.</p>

<p><center><img src="/img/architecture/cqrs.png" width="630" height="300"/><br/><em> Source: Martin Fowler</em></center></p>

<p>
<b> References </b>
<ul>
<li><a href="https://henriquesd.medium.com/the-command-and-query-responsibility-segregation-cqrs-pattern-16cb7704c809">The Command and Query Responsibility Segregation (CQRS) Pattern</a></li>
<li><a href="https://martinfowler.com/bliki/CQRS.html">Marting Fowler - CQRS</a></li>
</ul>
</p>

<br/>

<h1><u id="Hexagonal">Hexagonal</u></h1>

<p style="text-align: justify;">The main idea is to separate the business from all technical dependence. The core has the business and the external parts have part of the application with technical dependencies. The border of the core has plugins to allow communication between the external parts and the core.  The plugins are Port represented by interfaces with the rules of the communication. To make the request from the external part match with the plugin there are the Adapters. It is TDD oriented, business-focused, use Separation of Concept.</p>

<p style="text-align: justify;">The external parts can be identify in two sides:</p>
<ul>
  <li>Drivers: Who start the communication with core (GUI, Rest). The Ports used on that side should be mapped in use cases.</li>
  <li>Driven: Who receives requests from the core (Repository, Recipient). The Ports use on this side are called SPI (Service Provider Interface)
</li>
</ul>

<p style="text-align: justify;">The Adapters should be created to each technology. On the driven side you can create mocks to simulate database, for example, and not block the business development. Furthermore, here is used Inversion of Control (IoC) to ensure the concept that the core is independent.</p>

<center><img src="/img/architecture/hexagonal.png" width = "450" height = "200"/><br/>
<em> Sources: <a href="https://reflectoring.io/spring-hexagonal/">Tom Hombergs - reflectoring.io</a></em></center>

<p>
<b> References </b>
<ul>
<li><a href="https://alistair.cockburn.us/hexagonal-architecture/">Hexagonal architecture</a></li>
<li><a href="https://reflectoring.io/spring-hexagonal/">Hexagonal Architecture with Java and Spring</a></li>
</ul>
</p>

<br/>

<br/>

<h2>UI</h2>

<h1><u id="MVC">MVC</u></h1>

<p style="text-align: justify;">This pattern separate the application in three logic parts: Model (Data) , View (interaction with the user), Controller (connection between Model and View). View and Model should not communicate with each other directly but through the Controller. The Controller is responsible for part of the logic. It makes possible independent development to the frontend and backend. The user Interaction is handled by Controller. The code UI is minimal.</p>

<p><center><img src="/img/architecture/mvc.png" width = "330" height = "200"/><br/>
<em> Sources: Guru99</em></center></p>


<p>
<b> References </b>
<ul>
<li><a href="https://www.guru99.com/mvc-tutorial.html">Guru99</a></li>
<li><a href="https://www.tutorialspoint.com/mvc_framework/mvc_framework_introduction.htm">Tutorialpoint</a></li>
</ul>
</p>

<br/>

<h1><u id="MVP">MVP</u></h1>

<p style="text-align: justify;">It is an alternative to MVC because removes logic from Controller, removing the controller idea and adding a mediator, the Presenter, which lets the decisions to View and the logic to Model. It has a passive view. Each Presenter manages one View, different from the Controller which can handle more than one. The user Interaction is handled by View. It has more code in UI.</p>

<p><center><img src="/img/architecture/mvp.png" width = "390" height = "300"/><br/>
<em> Sources: <a href="https://medium.com/android-news/architectural-guidelines-to-follow-for-mvp-pattern-in-android-2374848a0157">Rakshit Soral</a></em></center></p>

<p>
<b> References </b>
<ul>
<li><a href="https://www.geeksforgeeks.org/mvp-model-view-presenter-architecture-pattern-in-android-with-example/">GeekForGeeks</a></li>
<li><a href="https://medium.com/android-news/architectural-guidelines-to-follow-for-mvp-pattern-in-android-2374848a0157">Architectural Guidelines to follow for MVP pattern in Android</a></li>
</ul>
</p>

<br/>

<h1><u>MVVM</u></h1>

<p id="MVVM" style="text-align: justify;">It is a pattern to use more deep the data binding idea, which makes it possible to get data from the model. The difference between ViewModel and Presenter is ViewModel doesn't have references to view. It's great for desktop and mobile applications. The user Interaction is handled by View. The code UI is minimal. </p>

<blockquote>
The view model is responsible for presenting functions, commands, methods, to support the state of the View. It is also accountable to operate the model and activate the events in the View. [Guru99]
</blockquote>

<p><center><img src="/img/architecture/mvvm.png" width = "290" height = "150"/><br/>
<em> Sources: Guru99</em></center></p>

<p>
<b> References </b>
<ul>
<li><a href="https://www.geeksforgeeks.org/mvvm-model-view-viewmodel-architecture-pattern-in-android/">MVVM (Model View ViewModel) Architecture Pattern in Android</a></li>
<li><a href="https://www.guru99.com/mvc-vs-mvvm.html">Guru99 - MVC vs MVVM: Key Differences with Examples</a></li>
</ul>
</p>


<h2>References</h2>

<ul>
  <li><a href="https://martinfowler.com/architecture/">Martin Fowler</a></li>
  <li><a href="https://www.infoq.com/news/2020/01/monolith-architectural-drivers/">Modular Monolithic Architecture, Microservices and Architectural Drivers
</a></li>
  <li><a href="https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html">The Clean Architecture</a></li>
</ul>
