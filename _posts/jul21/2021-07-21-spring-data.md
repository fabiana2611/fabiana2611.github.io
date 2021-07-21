---
layout: post
title:  "Spring Data"
date:   2021-07-21
categories: spring
permalink: /:categories/spring-data
---

<p style="text-align: justify;">The Spring Data is part of the <a href="https://fabiana2611.github.io/spring/springecosystem">Spring Ecosystem</a> that is responsible for the persistence layer. The <a href="https://spring.io/projects/spring-data">Spring Data</a> has many projects within it where the best known is the Spring Data JPA.</p>

<blockquote> It makes it easy to use data access technologies, relational and non-relational databases, map-reduce frameworks, and cloud-based data services. This is an umbrella project which contains many subprojects that are specific to a given database. <a href="https://spring.io/projects/spring-data">[1]</a></blockquote>

<p>	<center>
		<img src="/img/spring/springdataprojects.png" width="30%" />
</center></p>


<p style="text-align: justify;">The Spring Data provides a common set of interfaces, a common naming convention, aspected behavior and repository and data mapping convention. The <a href="https://docs.spring.io/spring-data/jdbc/docs/2.2.3/reference/html/#repositories">Repository</a> interface (inspired by DDD) gives to developer the CRUD actions ready to use, avoid all the DAO implementations. Besides that, it also give support to sort results or to pagination. Then, the key components are Repository Interface and Entity Objects.</p>

<p>The example below show a repository with the method to consult student by name and you don't need to implement it. If you need a specific query you also can custom a query to it, eliminating the use of @NamedQuery on the entity classes.<p>

<p><center>
	<img src="/img/spring/repositoryimpl.png" />
</center></p>

<p style="text-align: justify;">In summary, as the benefits, Spring Data remove boilerplate code and provide a clean mechanism to make swapping data sources easier.</p>

<br />
<h3>Spring Data Commons</h3>

<blockquote>Core Spring concepts... provides shared infrastructure across the Spring Data projects. It contains technology neutral repository interfaces as well as a metadata model for persisting Java classes</blockquote>

<p><a href="https://github.com/spring-projects/spring-data-commons">Goals:</a></p>

<em>
	<ul>
		<li>Powerful Repository and custom object-mapping abstractions</li>
		<li>Support for cross-store persistence</li>
		<li>Dynamic query generation from query method names</li>
		<li>Implementation domain base classes providing basic properties</li>
		<li>Support for transparent auditing (created, last changed)</li>
		<li>Possibility to integrate custom repository code</li>
		<li>Easy Spring integration with custom namespace</li>
	</ul>
</em>

<p><b>Maven</b></p>
{% highlight ruby %}
<dependency>
  <groupId>org.springframework.data</groupId>
  <artifactId>spring-data-commons</artifactId>
  <version>${version}</version>
</dependency>
{% endhighlight %}

<br />
<h3>Spring Data JDBC</h3>

<blockquote>Spring Data repository support for JDBC. In order to achieve this it does NOT offer caching, lazy loading, write behind or many other features of JPA. This makes Spring Data JDBC a simple, limited, opinionated ORM</blockquote>

<p>If you need something simpler than JPA you can use JDBC. More detail about it you can see the <a href="https://docs.spring.io/spring-data/jdbc/docs/2.2.3/reference/html/#jdbc.repositories">documentation</a>.</p>

<p><b>Maven</b></p>
{% highlight ruby %}
  <dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-jdbc</artifactId>
    <version>2.2.3</version>
  </dependency>
{% endhighlight %}

<p><b>Plus</b></p>

<center>
	<iframe width="360" height="215" src="https://www.youtube.com/embed/EaHlancPA14" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

<br />
<h3>Spring Data JPA</h3>

<blockquote>Spring Data repository support for JPA. Spring Data JPA aims to significantly improve the implementation of data access layers by reducing the effort to the amount that’s actually needed. As a developer you write your repository interfaces, including custom finder methods, and Spring will provide the implementation automatically</blockquote>

<p style="text-align: justify;">The way to code with JPA using Spring is similar how you code using <a href="https://fabiana2611.github.io/javaee/jpa">JPA with Java EE</a>. However, in  Java EE , some code is too verbose. More detail about it you can see the <a href="https://docs.spring.io/spring-data/jpa/docs/2.5.3/reference/html/#jpa.repositories">documentation</a>.</p>

<p><b>Maven</b></p>

{% highlight ruby %}
<dependency>
   <groupId>org.springframework.data</groupId>
   <artifactId>spring-data-jpa</artifactId>
   <version>2.4.0</version>
</dependency>
{% endhighlight %}

<p><b>Plus</b></p>

<table>
  <tr>
    <th>JPA</th>
    <th>JPA e Hibernate</th>
  </tr>
  <tr>
    <td>
      <iframe width="360" height="215" src="https://www.youtube.com/embed/yvXCxWkLpfA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </td>
    <td>
  		<iframe width="360" height="215" src="https://www.youtube.com/embed/TQQki9yQaLg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </td>
  </tr>
</table>

<br />
<h3>Spring Data LDAP</h3>

<blockquote>It provides repository abstractions for Spring LDAP on top of Spring LDAP’s LdapTemplate and Object-Directory Mapping</blockquote>

<p>More detail about how to use LDAP Repositories you can see the <a href="https://docs.spring.io/spring-data/ldap/docs/2.5.3/reference/html/#ldap.repositories">documentation</a>.</p>

<p><b>Maven</b></p>

{% highlight ruby %}
<dependency>
	<groupId>org.springframework.data</groupId>
	<artifactId>spring-data-bom</artifactId>
	<version>2021.0.3</version>
	<scope>import</scope>
	<type>pom</type>
</dependency>
{% endhighlight %}

<p><b>Plus</b></p>

<center>
	<iframe width="360" height="215" src="https://www.youtube.com/embed/hdUQaGePWRo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

<br />
<h3>Spring Data KeyValue</h3>

<blockquote>Map based repositories and APIs to easily build a Spring Data module for key-value stores.</blockquote>

<p>More detail about it you can see the <a href="https://github.com/spring-projects/spring-data-keyvalue">documentation</a>.</p>

<p><b>Maven</b></p>

{% highlight ruby %}
<dependency>
  <groupId>org.springframework.data</groupId>
  <artifactId>spring-data-keyvalue</artifactId>
  <version>${version}.RELEASE</version>
</dependency>
{% endhighlight %}

<br />
<h3>Spring Data REST</h3>

<blockquote>Exports Spring Data repositories as hypermedia-driven RESTful resources in a simplest way then Spring MVC or Spring WebFlux.</blockquote>

<p>More detail about how to use LDAP Repositories you can see the <a href="https://docs.spring.io/spring-data/rest/docs/3.5.3/reference/html/#intro-chapter">documentation</a>.</p>

<p><b>Maven</b></p>

{% highlight ruby %}
<dependency>
  <groupId>org.springframework.data</groupId>
  <artifactId>spring-data-rest-webmvc</artifactId>
  <version>3.5.3</version>
</dependency>
{% endhighlight %}

<p><b>Plus</b></p>

<center>
	<iframe width="360" height="215" src="https://www.youtube.com/embed/prtat_cKUVA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

<br />
<h3>Conclusion</h3>

<p style="text-align: justify;">This post had no intention to go deep into the Spring Data but to show Spring Data is more than JPA. If you need one of the Spring Data projects, go to the <a href="https://spring.io/projects/spring-data">documentation</a> and improve your knowledge.</p>

<br />
<h3>References</h3>

<ul>
	<li><a href="https://www.linkedin.com/learning/spring-spring-data-2">Linkedin - Spring: Spring Data 2</a></li>
  <li><a href="https://docs.spring.io/spring-framework/docs/5.3.x/reference/html/data-access.html#spring-data-tier">Spring Doc - Spring Access </a></li>
  <li><a href="https://spring.io/projects/spring-data">Spring Doc - Spring Data</a></li>
	<li><a href="https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#preface">Spring Doc - Spring Data JPA</a></li>
	<li><a href="https://www.baeldung.com/the-persistence-layer-with-spring-data-jpa">Introduction to Spring Data JPA</a></li>
	<li><a href="https://blog.algaworks.com/spring-data-jpa/">O que é Spring Data JPA?</a></li>
	<li><a href="https://www.infoq.com/br/articles/spring-data-intro/">Spring Data: A solução mais geral para persistência?</a></li>
</ul>
