---
layout: post
title:  "JPA - Native Query"
date:   2020-01-30
categories: javaee java database
permalink: /:categories/jpa-native-query
---

<p style="text-align: justify;">In most parts of your life such a programmer, you will use JPQL. It's easy to work. However, in some cases, the JPQL cannot be enough.</p>
<p style="text-align: justify;">Sometimes, there are scenarios where is necessary to use a specific query feature of the database that your JPA implementation (such as hibernate) doesn't give support.</p>
<p style="text-align: justify;">The annotation used when you are using JPQL is the <span style="color: #993366;">@NamedQuerie</span> that you add in your entity. Another option is to add this query inside an XML.</p>

<pre>@NamedQueries({ @NamedQuery(name = "nameOfYourQuery",
  query = "SELECT e FROM YourEntity e"),
public class YourEntity {
....
}</pre>
To execute this query frequently you use something like this:
<pre>entityManager.createNamedQuery("nameOfYourQuery", YourEntity.class);</pre>
To use a native query is similar, but the natural return is a list or an array:
<pre>Query q = em.createNativeQuery("SELECT e.name FROM YourEntity e");
List<Object[]> entities = q.getResultList();</pre>
<p style="text-align: justify;">In case you have a class that represents the result you can call your native query by name:</p>

<pre>Query q = em.createNativeQuery("yourNativeQueryName", YourEntity.class);
List yourEntity = q.getResultList();</pre>
<p style="text-align: justify;">The declaration of your query can be using the annotation <span style="color: #993366;">@SqlResultSetMapping</span>. It needs the annotation <span style="color: #993366;">@ColumnResult</span> that will represent all the columns in the result of your query.</p>

<pre>@SqlResultSetMapping(name="nameYourNativeQueryMap",
   columns = { @ColumnResult(name = "id"),
               @ColumnResult(name = "name")})

@NamedNativeQuery( name = "yourNativeQueryName",
    query = "SELECT e.id, e.name FROM YourEntity e ",
    resultSetMapping = "nameYourNativeQueryMap")</pre>
		
<h2>References</h2>
<ul>
	<li><a href="https://thoughts-on-java.org/jpa-native-queries/">Thoughts On Java</a></li>
	<li><a href="https://www.youtube.com/watch?v=bsZQRZx8prQ&list=PLZTjHbp2Y7812axMiHkbXTYt9IDCSYgQz&index=13">Algaworks - video</a></li>
</ul>
 
