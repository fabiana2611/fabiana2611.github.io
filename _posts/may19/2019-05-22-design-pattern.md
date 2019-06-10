---
layout: post
title:  "Design Pattern"
date:   2019-05-23
categories: bestpractice
permalink: /:categories/design-pattern
---

The design patterns come up to help us with best practices to solve common problems. The patterns can help in the maintenance of the system. However, you should have a code sense to decide when should NOT use them. [Clean Code](https://fabiana2611.github.io/bestpractice/cleancode) is better than a code that makes you look smart. The excess of patter use just because you wanna do that can cause productivity and maintenance troubles. The SIMPLE can be beautiful.

There are a lot of patterns that you can choose an also you will find many blogs to speak about them. Here, I'd like to put together some of them just with the summary. I believe it can facilitate understanding and help us to decide about the next step. I'll list the GoF, Java EE and Microservice patterns.

<br/>
<h3>GoF - Gang of Four</h3>

Four authors wrote a book with a set of patterns which can be used to reuse code. This work separate three categories of patterns. The Refactoring Guru explain in an intuitive way all these patterns. Some great implementations you can find in [tutorialspoint](https://www.tutorialspoint.com/design_pattern/factory_pattern.htm), [HowToDoInJava](https://howtodoinjava.com/gang-of-four-java-design-patterns/) and [StackAbuse](https://stackabuse.com/creational-design-patterns-in-java/).

| Creational |
| :------------- |
|<a href="https://howtodoinjava.com/design-patterns/singleton-design-pattern-in-java/" >Singleton</a> - One instance per JVM <br/> <a href="https://howtodoinjava.com/design-patterns/creational/builder-pattern-in-java/">Builder</a> - Different types of immutable objects <br/> <a href="https://howtodoinjava.com/design-patterns/creational/implementing-factory-design-pattern-in-java/">Factory</a> - Centralized creation objects <br/> <a href="https://howtodoinjava.com/design-patterns/creational/abstract-factory-pattern-in-java/" >Abstract Factory</a> - Abstraction over a group of factories <br/> <a href="https://howtodoinjava.com/design-patterns/creational/prototype-design-pattern-in-java/" >Prototype</a>: create objects with similar states using clone. <br/>|
| <strong>Structural</strong> |
| :------------- |
|<a href="https://howtodoinjava.com/2014/05/10/adapter-design-pattern-in-java/" >Adapter</a>: map an interface to another interface <br/> <a href="https://howtodoinjava.com/design-patterns/structural/bridge-design-pattern/" >Bridge</a>: decouple a class into two parts <br/> <a href="https://howtodoinjava.com/design-patterns/structural/composite-design-pattern/" >Composite</a>: compose the objects into tree structures to represent whole-part hierarchies <br/> <a href="https://howtodoinjava.com/design-patterns/structural/decorator-design-pattern/" >Decorator</a>: facilitate to add new features or behaviours <br/> <a href="https://howtodoinjava.com/design-patterns/structural/facade-design-pattern/" >Facade</a>: unified interface to a set of interfaces in a subsystem <br/> <a href="https://howtodoinjava.com/design-patterns/structural/flyweight-design-pattern/" >Flyweight</a>: a shared object that can be used in multiple contexts simultaneously <a href="https://howtodoinjava.com/design-patterns/structural/proxy-design-pattern/" >Proxy</a>: a proxy object provide a surrogate or placeholder for another object to control access to it |
| <strong>Behavioural</strong> |
| :------------- |
|<a href="https://howtodoinjava.com/design-patterns/behavioral/chain-of-responsibility-design-pattern/" >Chain of Responsibility</a>: request handled by more than one object <br/> <a href="https://howtodoinjava.com/design-patterns/behavioral/command-pattern/" >Command</a>: abstract the business logic into discrete actions which we call commands <br/> <a href="https://howtodoinjava.com/design-patterns/behavioral/iterator-design-pattern/" >Iterator</a>: access the elements of an aggregate object sequentially without exposing its underlying representation <br/> <a href="https://howtodoinjava.com/design-patterns/behavioral/visitor-design-pattern-example-tutorial/" >Visitor</a>: when we want a hierarchy of objects to modify their behaviour but without modifying their source code.<br/> <a href="https://howtodoinjava.com/design-patterns/behavioral/strategy-design-pattern/" >Strategy</a>: choose a specific implementation of algorithm or task in run time <br/> <a href="https://howtodoinjava.com/design-patterns/behavioral/template-method-pattern/" >Template Method</a>: defines the sequential steps to execute a multi-step algorithm <br/> <a href="https://howtodoinjava.com/design-patterns/behavioral/mediator-pattern/" >Mediator</a>: an object that encapsulates how a set of objects interact <a href="https://howtodoinjava.com/design-patterns/behavioral/observer-design-pattern/" >Observer</a>: when one object changes state, all its dependents are notified and updated automatically <br/> <a href="https://howtodoinjava.com/design-patterns/behavioral/state-design-pattern/" >State</a>: allows an object to alter its behaviour when its internal state changes <br/> <a href="https://howtodoinjava.com/design-patterns/behavioral/memento-design-pattern/" >Memento</a>: restore state of an object to a previous state <br/> Interpreter: specifies how to evaluate sentences in a language, programmatically|

<br/>
<h3>Java EE Design Pattern</h3>

The [coreJ2EE Pattern book](http://www.corej2eepatterns.com/) describes all pattern that you can find to develop using an enterprise application. Some of them we use in our development project and others are not usual on day-by-day because they are used in some frameworks and we don't need to be worried about that. You will find great implementations in [StackAbuse](https://stackabuse.com/java-j2ee-design-patterns/) and [tutorialspoint](https://www.tutorialspoint.com/design_pattern/).

| <strong>Presentation Tier</strong> |
| :------------- |
|<a href="https://www.tutorialspoint.com/design_pattern/intercepting_filter_pattern.htm" >Intercepting Filter</a>: pre-processing request.<br/><a href="http://www.corej2eepatterns.com/ContextObject.htm">Context Object</a>: used for maintaining state and for sharing/propagate information across the system layers. <a href="https://www.dre.vanderbilt.edu/~schmidt/PDF/Context-Object-Pattern.pdf" >(i)</a><br/><a href="http://www.corej2eepatterns.com/ViewHelper.htm">View Helper</a> separates the static view from the processing of the business model data <a href="http://www.javaguides.net/2018/08/view-helper-design-pattern-in-java.html" >(i)</a><br/><a href="http://www.corej2eepatterns.com/DispatcherView.htm">Dispatcher View</a>  initial access point for a request (Front Controller + View Helper + Service To Worker) <a href="https://www.javaskool.com/dispatcher-view-design-pattern/" >(i)</a><br/><a href="https://www.tutorialspoint.com/design_pattern/front_controller_pattern.htm" >Front Controller</a>: centralized request handling<br/><a href="http://www.corej2eepatterns.com/ApplicationController.htm">Application Controller</a>: Centralize the flow of the application and screen navigation <a href="https://wiki.genexus.com/commwiki/servlet/wiki?9390,Application+Controller+Pattern" >(i)</a><br/><a href="http://www.corej2eepatterns.com/CompositeView.htm">Composite View</a> Each subview can be included dynamically and the layout of the page can be managed independently of the content <a href="http://www.javaguides.net/2018/08/composite-view-design-pattern-in-java.html" >(i)</a><br/><a href="http://www.corej2eepatterns.com/ServiceToWorker.htm">Service To Worker</a>: centralize control and request handling to retrieve a presentation model before turning control over to the view ( Dispatcher component + Front Controller + View Helper Patterns)<a href="https://www.javaskool.com/service-to-worker-design-pattern/" >(i)</a>|
| <strong>Business Tier</strong> |
| :------------- |
|<a href="https://www.tutorialspoint.com/design_pattern/data_access_object_pattern.htm" >Data Access Object</a> (DAO): used to separate data accessing in a database from business logic.<br/><a href="http://www.corej2eepatterns.com/WebServiceBroker.htm">Web Service Broker</a> expose and broker one or more services using XML and Web protocols <a href="https://www.javaskool.com/web-service-broker-design-pattern/" >(i)</a><br/><a href="http://www.corej2eepatterns.com/ServiceActivator.htm">Service Activator</a> facilitates asynchronous processing for EJB components <a href="https://www.javaskool.com/service-activator-design-pattern/" >(i)</a><br/><a href="http://www.corej2eepatterns.com/DomainStore.htm">Domain Store</a> separating persistence from object model <a href="https://www.javaskool.com/domain-store-design-pattern/" >(i)</a><br/>|
| <strong>Integration Tier</strong> |
| :------------- |
|<a href="https://www.tutorialspoint.com/design_pattern/business_delegate_pattern.htm" >Business Delegate:</a> decouple the presentation layer from the business layer<br/><a href="https://www.tutorialspoint.com/design_pattern/service_locator_pattern.htm" >Service Locator</a>: locate various services using JNDI lookup. Decouple the <em>Service Consumers</em> and the concrete classes<br/><a href="http://www.corej2eepatterns.com/SessionFacade.htm">Session Facade</a> Encapsulates business-tier components.  It's responsible for Locating, creating and modifying the business objects Providing a uniform coarse-grained service access <a href="https://www.javaskool.com/session-facade-design-pattern/" >(i)</a><br/><a href="http://www.corej2eepatterns.com/BusinessObject.htm">Business Object</a> separate business data and logic using an object model. <a href="https://www.javaskool.com/business-object-design-pattern/" >(i)</a><br/><a href="https://www.tutorialspoint.com/design_pattern/composite_entity_pattern.htm" >Composite Entity</a>: it represents a graph of objects. When updated all dependent objects are updated. EJB is the main use. <br/><a href="https://www.tutorialspoint.com/design_pattern/transfer_object_pattern.htm" >Transfer Object</a>: used when you want to send an object with attributes from different sources.<br/><a href="http://www.corej2eepatterns.com/TransferObjectAssembler.htm">T O Assembler</a>: The Transfer Object Assembler aggregates multiple Transfer Objects from various business components and services and returns it to the client. <a href="https://www.javaskool.com/transfer-object-assembler-design-pattern/" >(i)</a><br/>|

The <a href="https://www.tutorialspoint.com/design_pattern/mvc_pattern.htm" >MVC</a> pattern involves all the tiers and because of that also you will find <em><a href="https://www.futurehosting.com/blog/what-is-an-mvc-framework/" >MVC frameworks</a></em>. It is an acronym to Model-View-Controller where Model represents the data, View represents the visualization of the data and the Controller is who handles the communication between View and Model.

<h3>Microservice</h3>

It is a relatively new subject. I could find some patterns related to this theme but there are some patterns that are usual to find about Microservice, which I classified such Common Patterns. The Microsoft also define some others that I list below.

| <strong><a href="http://blog.arungupta.me/microservice-design-patterns/" >Common</a></strong> |
| :------------- |
|<strong>Aggregator: </strong>a simple web page that invokes multiple services to achieve the functionality required by the application<br/> <strong>Proxy: </strong>used where each individual service need not be exposed to the consumer and should instead go through an interface<br/> <strong>Chained: </strong>produce a single consolidated response to the request.<br/><strong>Branch: </strong>allows simultaneous response processing from two, likely mutually exclusive, chains of microservices<br/><strong>Shared Data: </strong>This allows the service to be polyglot, and use the right tool for the right job<br/> <strong>Asynchronous Messaging: </strong>using message queues<br/>|
|<a href="https://vslive.com/Blogs/News-and-Tips/2018/02/Go-Fast-by-Going-Micro-Microservices-Design-Patterns-You-Should-Know.aspx" >Microsoft</a>|
| :------------- |
| <strong>Ambassador: </strong>used to offload common client connectivity tasks<br/><strong>Anti-corruption layer: </strong>implements a façade between new and legacy applications<br/><strong>Backends for Frontends: </strong>creates separate backend services for different types of clients<br/><strong>Bulkhead: </strong> isolates critical resources<br/>
<strong>Gateway Aggregation: </strong>aggregates requests to multiple individual microservices into a single request<br/><strong>Gateway Offloading: </strong>enables each microservice to offload shared service functionality<br/><strong>Gateway Routing: </strong>routes requests to multiple microservices using a single endpoint<br/><strong>Sidecar: </strong>provide isolation and encapsulation of components<br/> <strong>Strangler: </strong>supports incremental migration|

The post <a href="https://dzone.com/articles/design-patterns-for-microservices">Design Pattern for Microservice</a> gives to us a list of classified patterns. Some of them were cited before.

|<strong>Decomposition Patterns</strong>|
|:--------|
|<strong>Decompose by Business Capability:</strong> applying the single responsibility principle<br/><strong>Decompose by Subdomain:</strong> use DDD (Domain-Driven Design) to classes which will not be easy to decompose<br/><strong>Strangler Pattern:</strong> supports incremental migration - it creates two separate applications that live side by side until the refactored application “strangles” or replaces the original application.<br/>|
|<strong>Integration Patterns</strong>|
|:---------|
|<strong>API Gateway Pattern:</strong> helps to address many concerns raised by a microservice implementation, not limited to the ones above<br/><strong>Aggregator Pattern:</strong> aggregate the data from different services and then send the final response to the consumer<br/> <strong>Client-Side UI Composition Pattern: </strong> the UI has to be designed as a skeleton with multiple sections/regions of the screen/page. Each section will make a call to an individual backend microservice to pull the data<br/>|
|<strong>Database Patterns</strong>|
|:-------|
|<strong>Database per Service:</strong> it must be private to that service only. It should be accessed by the microservice API only. It cannot be accessed by other services directly<br/> <strong>Shared Database per Service:</strong> In this pattern, one database can be used by 2 or 3 microservice. It is a pattern to be used when you start to break the application into smaller logical pieces. When this migration finish you should use a database per service.<br/> <strong>Command Query Responsibility Segregation (CQRS)</strong>: it defines a solution to implement queries to retrieve data from different sources. It suggests splitting the application into <em>command side</em> (Create, Update, Delete) and the <em>query side</em> (materialized views) to handle the requests.<br/> <strong>Saga Pattern:</strong> it is used to ensure data consistency across services which can be implemented centralized or not centralized.<br/>|
|<strong>Observability Patterns</strong>|
|:------|
|<strong>Log Aggregation:</strong> a centralized logging service that aggregates logs from each service instance<br/><strong>Performance Metrics:</strong> aggregate the metrics of an application service. The metrics can be <em>pushed</em> to a metrics server or the server can <em>pull</em> the metrics from the services.<br/><strong>Distributed Tracing:</strong> it helps to trace a request end-to-end to troubleshoot the problem<br/><strong>Health Check:</strong> Each service needs to have an endpoint which can be used to check the health of the application<br/>|
|<strong>Cross-Cutting Concern Patterns</strong>|
|:--------|
|<strong>External Configuration:</strong> it avoids code modification for configuration changes<br/><strong>Service Discovery Pattern:</strong> the idea is to publish the service where the consumers can find services.<br/> <strong>Circuit Breaker Pattern:</strong> it avoids cascading service failures and handles failures gracefully. It is based on invoke service via a proxy (electrical circuit breaker) and timeout.<br/> <strong>Blue-Green Deployment Pattern:</strong> implemented to reduce or remove downtime by running two identical production environments, Blue and Green, which one of them is the new version that will replace the other one.<br/>|


<br/>

<h3>References</h3>

<ul>
	<li><a href="https://www.dre.vanderbilt.edu/~schmidt/PDF/Context-Object-Pattern.pdf" >Context Object</a></li>
	<li><a href="https://dzone.com/articles/design-patterns-for-microservices" >Design Pattern for Microservice</a></li>
	<li><a href="https://vslive.com/Blogs/News-and-Tips/2018/02/Go-Fast-by-Going-Micro-Microservices-Design-Patterns-You-Should-Know.aspx" >Go Fast by Going Micro: Microservices Design Patterns You Should Know</a>
</li>
	<li><a href="https://refactoring.guru/design-patterns" >Refactoring Guru</a></li>
	<li><a href="https://www.amazon.com/exec/obidos/ASIN/0201633612" >coreJ2EE</a></li>
	<li><a href="https://howtodoinjava.com/gang-of-four-java-design-patterns/" >HowToDoInJava</a></li>
	<li><a href="https://www.tutorialspoint.com/design_pattern/factory_pattern.htm" >totorialspoint</a></li>
	<li><a href="https://stackabuse.com/creational-design-patterns-in-java/" >StackAbuse</a></li>
</ul>
