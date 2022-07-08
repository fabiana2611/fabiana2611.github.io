---
layout: post
title:  "Clean Architecture"
date:   2022-07-08
categories: books foundation
permalink: /:categories/clean-architecture
---


<center>
  <p><img src="/img/books/cleanarch.png" width="20%" height="20%"/></p>
</center>

<p style="text-align: justify;">The clean architecture, term used by uncle Bob, wish to achieve the separation of responsibilities  dividing the software into layers. In this direction, each internal layer cannot depends of the over layer an the outer cycle.</p>.

<center>
  <p><img src="/img/books/cleanarchdiagram.png" width="20%" height="20%"/></p>
</center>

<p>Here are the definition around the clean architecture:</p>
<ul>
  <li>Entities encapsulate Enterprise wide business rules </li>
  <li>Use cases orchestrate the flow of data to and from the Entities </li>
  <li>Adapters converts data from the format most convenient for the use cases and entities, to the format most convenient for some external agency such as the Database or the Web</li>
  <li>Frameworks and tools such as the Database, the Web Framework, etc </li>
</ul>

<p><table>
  <tr>
    <td><iframe src="https://www.youtube.com/embed/2dKZ-dWaCiU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
    <td><iframe src="https://www.youtube.com/embed/NyJLw3sc17M" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></td>
  </tr>
</table></p>


<ul>
  <li><a href="https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html">The Clean Code Blog</a></li>
  <li><a href="https://fabiana2611.github.io/arch/hexa-arch-handson">Hexagonal Architecture - Hands On</a></li>
  <li><a href="https://cleancoders.com/">cleancoders.com</a></li>
</ul>
