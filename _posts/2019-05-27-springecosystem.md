---
layout: post
title:  "Spring EcoSystem"
date:   2019-05-27
categories: spring
permalink: /:categories/springecosystem
---

Hey everyone!!!

<p style="text-align: justify;">Did you already hear something about Spring to code applications? Such as me, did you feel confused at some moment with many "kind of springs"?</p>
<p style="text-align: justify;">Here I'd like to show you a macro view of the Spring. I believe from the moment we can understand how all of these are connected it will be easier to choose what you will need to start your projects using Spring. So, let's go!!</p>

<h3>Summary</h3>

<center>
  <iframe width="560" height="315" src="https://www.youtube.com/embed/dXpqA73t3W8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

<br/>
<h3>An intuitive macro view</h3>

<p style="text-align: justify;">There are many <a href="http://spring.io/projects" >Spring Projects</a> and each one can have sub projects.  <a href="http://springtutorials.com/about/" >Amit Sharma</a> in his post <a href="http://springtutorials.com/spring-ecosystem/" >Spring Framework EcoSystem - Introduction of Spring Project</a> splits the Spring Framework Ecosystem into five parts. <strong>Web layer, Common layer, Service layer, Data layer, Foundation.</strong></p>


<a href="http://springtutorials.com/spring-ecosystem/" ><img class="alignnone size-full wp-image-370" src="/img/spring/spring-ecosystem.jpg" alt="spring-ecosystem.jpg" width="992" height="550" /></a> <em>Figure 1 - Reference: Spring Tutorials</em>

<p style="text-align: justify;"><strong>Web Layer</strong>: It is related to front-end. The highlight is the <em><a href="https://spring.io/projects/spring-security" >Spring Security</a>.</em> <em>Figure 1</em> doesn't show dependency but the web layer projects can make use of <em>Spring Security</em>. <em>Spring Security</em> is a framework that control who can interact with your application and at what levels; authentication and authorization, respectively.</p>

<p style="text-align: justify;"><strong>Common Layer</strong>: The <a href="https://spring.io/projects/spring-framework" ><em>Spring Framework</em></a> was created to teams can focus on application-level business logic. It gives support for examples: [1 - CORE] dependency injection (decoupling, management of scopes); [2 - TEST] tests; [3 - DATA ACCESS] transactions, DAO support, JDBC; [4 - Spring MVC], to create web applications and RESTful service and you can see a separation of responsibilities.</p>

<center>
  <a href="https://blog.algaworks.com/aprender-spring-agora/" ><img class="  wp-image-371 aligncenter" src="/img/spring/mcv.png" alt="mcv.png" width="371" height="133" /></a>
  <br/>
  Figure 2 - MVC - Reference: Algawork
</center>

<br/>
<p style="text-align: justify;"><strong>Service Layer</strong>: [1 - <a href="http://spring.io/projects/spring-cloud" >Spring Cloud</a>] "<em>Spring Cloud provides tools for developers to quickly build some of the common patterns in distributed systems". </em>[2 - <a href="https://spring.io/projects/spring-integration" >Spring Integration</a>] "S<em>pring Integration’s primary goal is to provide a simple model for building enterprise integration solutions while maintaining the separation of concerns that is essential for producing maintainable, testable code.</em>"</p>

<p style="text-align: justify;"><strong>Data Layer</strong>: This layer is related to data handling and manipulation. The highlights are <em>Spring Data</em>. The <em><a href="https://spring.io/projects/spring-data" >Spring Data</a></em> give more facilities then the <em>Spring Data Access</em> in <em>Spring Framework</em>. This framework reduces the code by features such <em>repository and custom object-mapping abstractions</em> and <em>dynamic query derivation from repository method names</em>. Using <em>Spring Data</em> also is possible to swap the database with minimal code changes.  <a href="http://spring.io/projects/spring-amqp" ><em>Spring AMQP</em></a> is related to the use of messages in the systems and <a href="https://spring.io/projects/spring-batch" ><em>Spring Batch</em></a> is used to makes the programmer's lives easier when they need to work with batch jobs. <a href="https://spring.io/projects/spring-ldap" ><em>Spring LDAP</em></a> can be used to guarantee the authorization.</p>

<p style="text-align: justify;"><strong>Foundation Layer</strong>: <a href="https://spring.io/projects/platform" ><em>Spring IO Platform</em></a> provides facilities to use different projects or modules together (one platform, many workloads), but the supported life finishes on 9 April 2019. The <em><a href="https://spring.io/projects/spring-boot" >Spring Boot</a></em> makes the programmer more productive because it'll not necessary to be worried about configurations (no requirement for XML configuration; embed Tomcat, Jetty or Undertow directly). <a href="https://projects.spring.io/spring-xd/" ><em>Spring XD</em></a> is related to build and manage big data applications (<em>Spring XD</em> is redesigned as <em><a href="https://cloud.spring.io/spring-cloud-dataflow/">Spring Cloud Data Flow</a></em>).</p>

<center>
  <img class="  wp-image-372 aligncenter" src="/img/spring/springboot.png" alt="springBoot.png" width="290" height="194" />
  <br/>
  Figure 3 - Spring Boot: Reference - DevMedia
</center>

<br/>
<h3>Spring Boot Starters</h3>
<p style="text-align: justify;">Dependency management is an important issue in the projects. To help the developer, Spring Boot and an automation tool such as Maven, can make the process easier. For that, the <a href="https://www.baeldung.com/spring-boot-starters" >Spring Boot Staters</a> were built, and that reduced the number of manually added dependencies just by adding one dependency in pom.xml.</p>
<p style="text-align: justify;">One example is when you wish to build a <strong>WEB</strong> application. It's necessary only one dependency from Spring Boot. This Spring Boot declaration control <a href="https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-web/2.1.0.M3" >other dependencies</a> like Web, MVC, Tomcat. It allows the RESTfull implementation. It’s actually Spring MVC which provides all useful annotations to REST implementation.</p>
<img class="  wp-image-374 aligncenter" src="/img/spring/starterweb.png" alt="starterWeb.png" width="464" height="88" />

Another example is to use <strong>test</strong> libraries. This Spring Boot declaration control <a href="https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-test/2.1.0.RELEASE" >other dependencies</a> like mockito, junit, spring test.

<img class="  wp-image-375 aligncenter" src="/img/spring/startertest.png" alt="starterTest.png" width="436" height="100" />
<p style="text-align: justify;">The <a href="https://www.baeldung.com/spring-boot-devtools" >Spring Boot <strong>DevTool</strong></a><strong> </strong>can help to <a href="https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-devtools/2.1.0.RELEASE" >control</a> autoconfigure, jdb, hibernate core, servlet-api, sprint web. Two important features in DevTool is the automatic restart whenever files change in the classpath and permit a browser refresh when a resource is changed.</p>

<img class="  wp-image-376 aligncenter" src="/img/spring/starterdevtool.png" alt="starterDevtool.png" width="385" height="90" />

To use Spring Data you can use:

<img class="  wp-image-377 aligncenter" src="/img/spring/starterdata.png" alt="starterData.png" width="428" height="78" />

A complete example of pom.xml using Spring Boot you can see <a href="https://github.com/fabiana2611/api-java/blob/master/food-delivery/pom.xml" >here</a>.

<br/>
<h3>Conclusion</h3>
<p style="text-align: justify;">Spring has a big ecosystem that can help your application in several aspects. With a macro view, you can focus on your necessities. <em><strong>Spring Data JPA, Spring Boot, Spring Security, Spring Framework</strong></em> are, certainly, the main concepts that you should have. They are very important to implement a trust application in an easy way.</p>
<p style="text-align: justify;">Understand your requirements and go deep in your studies.!!!</p>

<h3>Posts Related:</h3>
<ul>
	<li><a href="https://fabiana2611.github.io/javaee/javaee" >Java EE</a></li>
	<li><a href="https://www.educba.com/java-ee-vs-spring/" >Java EE vs Spring</a></li>
</ul>
<h3>References</h3>
<ul>
	<li class="p1"><span class="s1"><a href="https://blog.algaworks.com/aprender-spring-agora/" >AlgaWorks</a> - Aprender Spring Agora</span></li>
	<li class="p1"><span class="s1"><a href="https://www.devmedia.com.br/spring-boot-simplificando-o-spring/31979" >DevMedia - Spring Boot</a></span></li>
	<li><a href="http://springtutorials.com/about/" >Spring Tutorials.com</a></li>
	<li><a href="https://www.baeldung.com/spring-boot-starters" >Spring Boot Starters</a></li>
	<li><a href="http://www.springboottutorial.com/spring-boot-starter-parent" >Spring Boot Starter Parent</a></li>
</ul>
