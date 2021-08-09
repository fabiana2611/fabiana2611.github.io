---
layout: post
title:  "Spring Boot"
date:   2021-08-09
categories: spring
permalink: /:categories/spring-boot
---

<p style="text-align: justify;">Spring Boot is part of <a href="https://fabiana2611.github.io/spring/springecosystem">Spring Ecosystem</a> that will help to manage the first steps to start an application. It handles low-level, predictable set-up for the developers and It has many non-functional features common to large numbers of projects.</p>

<blockquote>Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run". Some Features: (1) Create stand-alone Spring applications (2) Embed Tomcat, Jetty or Undertow directly (no need to deploy WAR files) (3) Provide opinionated 'starter' dependencies to simplify your build configuration <a href="https://spring.io/projects/spring-boot">[1]</a></blockquote>


<p style="text-align: justify;">The Spring Boot manage compatible dependences, excluding dependencies will not be used or finding the right version. It solve JARs as <em>spring-boot-*, spring-context-*, spring-core-* and spring-beans-*</em>. </p>

<p style="text-align: justify;">A good way to manage multiple dependencies is using <em>spring-boot-starter</em>. You don't need inform the version.</p>

<blockquote>Starters are a set of convenient dependency descriptors that you can include in your application. The starters contain a lot of the dependencies that you need to get a project up and running quickly and with a consistent, supported set of managed transitive dependencies.<a href="https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.build-systems.starters">[2]</a></blockquote>

<p style="text-align: justify;">As instance, if you need to use test libraries coordinate by Spring boot you should to use <em>spring-boot-start-test</em>. It will brings <em>spring-test-*, junit-*, mockito-*, </em> etc. Others examples of it are:</p>

<ul>
  <li>spring-boot-start-jdbc</li>
  <li>spring-boot-start-data-jpa</li>
  <li>spring-boot-start-web</li>
  <li>spring-boot-start-batch</li>
</ul>

<p style="text-align: justify;">To run the application is necessary pom.xml (setup dependencies), application.properties (general configurations) and application class to launch the application. A simple way to create an initial app is going the the <a href="http://start.spring.io">start.spring.io</a> and downloading it with all dependencies you believe is necessary. You can do your "Hello World" reading this <a href="https://spring.io/quickstart">quickstart</a>.</p>

<h3>Developer Tool</h3>

<p style="text-align: justify;">The <a href="https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.devtools">DevTools</a> is a collection of tools included by Spring boot to make developer's life easier (spring-boot-devtools). </p>

<p style="text-align: justify;">One feature is it has the cache disabled. Also, it allows the application be restart automatically when files on the classpath are changed.</p>

<p style="text-align: justify;">If you prefer don't have the behaviour to restart the application you can disable it by the line bellow.</p>

<pre>System.setProperty("spring.devtools.restart.enabled", "false");</pre>

<p style="text-align: justify;">In the same direction, there is the LiveReload server used to trigger a browser refresh when the resource is changed. To disable it you can change the property bellow. </p>

<pre>spring.devtools.livereload.enabled</pre>

<h3>Annotation</h3>

<p style="text-align: justify;"><b>@SpringBootApplication</b> identify to Spring framework the main class to be handled by Spring. It allows app to have auto-configuration (@EnableAutoConfiguration), component scan (@ComponentScan) and be able to define extra configuration (@SpringBootConfiguration). Then, when you are using @SpringBootApplication you don't need use the other three annotations.</p>

<p style="text-align: justify;"><b>@EnableAutoConfiguration</b> used to let Spring be responsible for the configuration based on the jar dependencies that you have added. You can combine @SpringBootApplication and @Configuration or @EnableAutoConfiguration and @Configuration, but not @SpringBootApplication and @EnableAutoConfiguration <a href="https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.auto-configuration">[3]</a></p>

<p style="text-align: justify;"><b>@ComponentScan</b><em> enable @Component scan on the package where the application is located</em>.<a href="https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.using-the-springbootapplication-annotation">[4]</a></p>

<p style="text-align: justify;"><b>@SpringBootConfiguration</b><em> enable registration of extra beans in the context or the import of additional configuration classes</em>.<a href="https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.using-the-springbootapplication-annotation">[4]</a></p>

<p style="text-align: justify;"><b>@Configuration</b> is used to identify the class will define the configuration to the application. Even be possible configure using XML, Spring is Java-based configuration.</p>

<p style="text-align: justify;"><b>@Import</b> is used to add other configuration classes. If you are using XML you should use <b>@ImportResource</b>.</p>

<p style="text-align: justify;"><b>@SpringBootTest:</b> To integration test you can use @SpringBootTest(classes=Application.class) to load specified configuration. That annotation will searches for @SpringBootConfiguration class and creates application context for the test.</p>


<h3>Spring Boot Features</h3>

<p><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.spring-application">SpringApplication</a></p>

<ul>
  <li>SpringApplication.run can be used to start the application inside the main method.</li>
  <li>It make possible the application start lazily. Which means the beans will be initialized by demand. It will reduce the time to start the application.</li>
  <li>It's possible to be <a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.spring-application.customizing-spring-application">customized</a>.</li>
  <li><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.spring-application.fluent-builder-api">SpringApplicationBuilder</a> will give support to use ApplicationContext hierarchy.</li>
  <li>It makes possible tracking the application startup sequence using  ApplicationStartup.</li>
</ul>

<p><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.external-config">Externalized Configuration</a></p>

<blockquote>Spring Boot lets you externalize your configuration so that you can work with the same application code in different environments.</blockquote>

<p style="text-align: justify;">One example is using the annotation @Value that has the property value injected into the bean. That value can comes from application.properties which can has different values by environment (e.g. application-prod.properties). In the same direction is possible to use <a  href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.external-config.typesafe-configuration-properties.java-bean-binding">JavaBean properties</a> by the use of @ConfigurationProperties and define properties to be used.</p>


<p><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.profiles">Profile</a></p>

<blockquote>Spring Profiles provide a way to segregate parts of your application configuration and make it be available only in certain environments. Any @Component, @Configuration or @ConfigurationProperties can be marked with @Profile to limit when it is loaded</blockquote>

<p><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.logging">Logging</a></p>

<p style="text-align: justify;">The internal logging use is done by the use of Commons Logging with default configurations for Java Util Logging, Log4J2, and Logback. If you are using the starters you will use Logback. It's possible to do all the configuration about the logs as color, text, export to a file, etc.</p>

<p><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.internationalization">Internationalization</a></p>

<blockquote>Spring Boot supports localized messages so that your application can cater to users of different language preferences. By default, Spring Boot looks for the presence of a messages resource bundle at the root of the classpath.</blockquote>

<p><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.json">JSON</a></p>

<p style="text-align: justify;">Spring Boot provides integration with three JSON mapping libraries: Gson, Jackson, JSON-B.</p>

<p><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.developing-web-applications">WEB Development</a></p>

<p style="text-align: justify;">Spring Boot is Well prepared to web application development. It has embedded servers (e.g. Tomcat, Jetty). Inside the pom you can <em>use spring-boot-starter-web</em> or <em>spring-boot-starter-webflux</em>. Also, It provides auto-configuration for Spring MVC. However, if you are using REST then you can use one of the JAX-RS implementation that Spring support as Jersey instead the Spring MVC.</p>

<p><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.security">Security</a></p>

<blockquote>If Spring Security is on the classpath, then web applications are secured by default. Spring Boot relies on Spring Security’s content-negotiation strategy to determine whether to use httpBasic or formLogin. To add method-level security to a web application, you can also add @EnableGlobalMethodSecurity with your desired settings. </blockquote>

<p style="text-align: justify;"><em>MVC Security: The default security configuration is implemented in SecurityAutoConfiguration and UserDetailsServiceAutoConfiguration.</em></p>

<p style="text-align: justify;"><em>WebFlux Security: Similar to Spring MVC applications, you can secure your WebFlux applications by adding the spring-boot-starter-security dependency. The default security configuration is implemented in ReactiveSecurityAutoConfiguration and UserDetailsServiceAutoConfiguration.</em></p>

<p style="text-align: justify;"><em>OAuth2: it is a widely used authorization framework that is supported by Spring. If you have spring-security-oauth2-client on your classpath, you can take advantage of some auto-configuration to set up an OAuth2/Open ID Connect clients. </em></p>

<p><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.testing">Testing</a></p>

<blockquote>Spring Boot provides a number of utilities and annotations to help when testing your application. Test support is provided by two modules: spring-boot-test contains core items, and spring-boot-test-autoconfigure supports auto-configuration for tests. Most developers use the spring-boot-starter-test “Starter”, which imports both Spring Boot test modules as well as JUnit Jupiter, AssertJ, Hamcrest, and a number of other useful libraries.</blockquote>

<p><b>Auto-configuration</b></p>

Spring boot has auto-configuration support to many resources as <a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.sql.datasource.embedded">embedded Database Support</a> (H2, HSQL, and Derby), JdbcTemplate, <a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.email">sending Email</a> and <a href="https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.spring-session">Spring Session</a>.

<p><b>Spring Boot Actuator: Production-ready Features</b></p>

<p>Spring has many resources to help you to monitor your application. You can monitor the endpoints, HTTP, JMX, using logs, audit. If you need monitor your application click <a href="https://docs.spring.io/spring-boot/docs/current/reference/html/actuator.html#actuator.metrics">here</a> to go deep.

<h3>Conclusion</h3>

<p>Your project is not dependent on Spring Boot. You can use many parts of the framework in a separate way. However, Spring Boot gives productivity to the development.</p>

<p><center>
  <iframe width="560" height="315" src="https://www.youtube.com/embed/ABjV1bObFW8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
  <br /><em>From Algaworks</em>
</center></p>


<h3>References</h3>

<ul>
	<li><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/">Spring Boot Reference Documentation</a></li>
  <li><a href="https://blog.algaworks.com/spring-boot/" >O que é Spring Boot?</a></li>
  <li><a href="https://www.baeldung.com/spring-vs-spring-boot" >A Comparison Between Spring and Spring Boot</a></li>
  <li><a href="https://www.javatpoint.com/spring-boot-tutorial" >Spring Boot Tutorial</a></li>
  <li><a href="https://www.youtube.com/watch?v=OHn1jLHGptw&list=PL8iIphQOyG-DHLpEx1TPItqJamy08fs1D" >Curso Spring Boot : Criando uma aplicação Java Web</a></li>
</ul>
