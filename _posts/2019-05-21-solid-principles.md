---
layout: post
title:  "S.O.L.I.D. Principles"
date:   2019-05-21
categories: bestpractice
permalink: /:categories/silid-principles
---

Hello World!!!

Many times, when we are programming, we feel that we can make it better, but we don't know exactly what to do or if we are in the right way.  In the post about <a href="https://fabiana2611.github.io/bestpractice/cleancode">Clean Code</a> it was said that it is necessary a "code-sense". But how to get this? Where can I start?

Don't worry. Some people have been thinking about it and they will lead us.

Some time ago, [Robert C. Martin](https://en.wikipedia.org/wiki/Robert_Cecil_Martin), wrote an <a href="http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod">article</a> about the principles of object-oriented programming that are very useful for every programmer and it will help us to think more clearly about our codes. He spoke about five principles of classes design and six principles about packages.

This post will focus on the first five ones because if you have this knowledge in your mind, your code will be easy to maintain and to extend and also they make it easy for developers to avoid code smells and easily refactor code.

<ul>
	<li><strong>S - </strong>Single Responsibility Principle (SRP)</li>
	<li><strong>O - </strong>Open-closed principle (OCP)</li>
	<li><b>L - </b>Liskov Substitution principle (LSP)</li>
	<li><b>I - </b>Interface Segregation principle (ISP)</li>
	<li><b>D - </b>Dependency inversion principle (DIP)</li>
</ul>

<br/>
<h3>1. Single Responsibility Principle</h3>

<blockquote><i>A class should have one, and only one, reason to change.</i></blockquote>

It is one of the basic principles most developers apply to build robust and maintainable software. This principle makes your software easier to implement, explain, understand than the ones that provide a solution for everything.

Uncle Bob, in his chapter about <a href="https://drive.google.com/file/d/0ByOwmqah_nuGNHEtcU5OekdDMkk/view">SRP</a>, define responsibility: “a reason for a change”. It's normal if the requirements change and the class has more responsibilities. When this happens you need to change your class. If the class has only one responsibility, the changes are not often and the number of bugs will be reduced.

The picture below shows how Uncle Bob represented in his article a set of classes with more than one responsibility (left) and how he changes the class Rectangle (right).

| :------------- | :------------- |
| <img src="/img/5Principles/SRP1.png" height="300" width="550">       | <img src="/img/5Principles/SRP2.png" height="300" width="550">       |

<br/>
<H3>2. Open-closed Principle</h3>

<blockquote><i>You should be able to extend a classes behavior, without modifying it.</i></blockquote>

You can add new behaviour, but you shouldn't break what works and change what exists. If one of them happens so you need to refactor your code.

Uncle Bob notes that some people had confused this principle. Then, he expresses himself in other <a href="https://8thlight.com/blog/uncle-bob/2013/03/08/AnOpenAndClosedCase.html" >post</a> saying: <em>It should be easy to change the behavior of a module without changing the source code of that module. This doesn't mean you will never change the source code. Ideally, you will be able to add the new behavior by adding new code and changing little or no old code.</em>

The next picture shows the example of the article where the class Circle was added and it was necessary add a new method to AreaCalculator. This implementation makes necessary add new methods to calculate each new shape.


<center>
 <img src="/img/5Principles/OCP1.png" height="300" width="550">  
</center>

The mechanisms behind the OCP are abstraction and polymorphism. Every new shape extends Shape interface and implements a specific behaviour and AreaCalculator doesn't need to know the type of the object.

<center>
 <img src="/img/5Principles/OCP2.png" height="300" width="550">  
</center>

The detail about this principle can be seen in the article about <a href="https://drive.google.com/file/d/0BwhCYaYDn8EgN2M5MTkwM2EtNWFkZC00ZTI3LWFjZTUtNTFhZGZiYmUzODc1/view">OCP</a> with examples. The examples in Java can be seen <a href="https://www.javabrahman.com/programming-principles/open-closed-principle-with-examples-in-java/">here</a>.

<br/>
<h3>3. Liskov Substitution Principle</h3>

<blockquote><i>Derived classes must be substitutable for their base classes.</i></blockquote>

Barbara Liskov introduced this principle in a 1987 and Uncle Bob add this in one of the five class design principles, <a href="https://drive.google.com/file/d/0BwhCYaYDn8EgNzAzZjA5ZmItNjU3NS00MzQ5LTkwYjMtMDJhNDU5ZTM0MTlh/view">LSP</a>.

This principle speaks about inheritance hierarchies. A subclass can override the parent class's method but cannot break the behaviour. This requires all subclasses to behave in the same way as the parent class. So, the behaviour of the class becomes more important than its structure.

The next picture, with detailed explanation in another <a href="https://code.tutsplus.com/tutorials/solid-part-3-liskov-substitution-interface-segregation-principles--net-36710">post</a>, shows an implementation of the classic example used by Uncle Bob in his article about <a href="https://drive.google.com/file/d/0BwhCYaYDn8EgNzAzZjA5ZmItNjU3NS00MzQ5LTkwYjMtMDJhNDU5ZTM0MTlh/view">LSP</a>.

<center>
 <img src="/img/5Principles/LSP2.png" width="500" height="300">  
</center>

You can see the relationship <em>Square</em> <strong>IS_A</strong> <em>Rectangle</em>. But in fact, it is not completely true. A square is a rectangle with equal width and height. If you run a test with <em>Client</em> using a <em>Square</em> object, it will break the test because the properties <em>width</em> and <em>height</em> have the same value.

A solution is to separate the classes and create a new hierarchy where both classes (<em>Square and Rectangle</em>) implement an interface (<em>Geometry</em>) where it is declared a common behaviour.

<br/>
<h3>4. Interface Segregation Principle</h3>

<blockquote><i>Make fine grained interfaces that are client specific.</i></blockquote>
<p style="text-align: justify;"><a href="https://drive.google.com/file/d/0BwhCYaYDn8EgOTViYjJhYzMtMzYxMC00MzFjLWJjMzYtOGJiMDc5N2JkYmJi/view">ISP</a>:<i> “Clients shouldn’t depend on methods they don’t use. Several client-specific interfaces are better than one generalized interface.” </i>It means that it's necessary to take care of the Interface Pollution.

The Interface Pollution happens when an InterfaceA has to add an InterfaceB that InterfaceA doesn't require, for the benefit of one of its subclasses. It makes the class "fat", and "fat" classes are hard to maintain and probably are not cohesive. Certainly, it should be split into different groups.

The picture below shows an example of the problem (left) where one interface is used for many clients and a solution (right) where the interface is split to be used to specific clients. The detail about this example can be seen <a href="https://code.tutsplus.com/tutorials/solid-part-3-liskov-substitution-interface-segregation-principles--net-36710" >here</a>.

<center>
 <img src="/img/5Principles/isp4.png" width="500" height="400">  
</center>

<br/>
<h3>5. Dependency Inversion Principle</h3>
<blockquote><i>Depend on abstractions, not on concretions.</i></blockquote>

<i><a href="https://drive.google.com/file/d/0BwhCYaYDn8EgMjdlMWIzNGUtZTQ0NC00ZjQ5LTkwYzQtZjRhMDRlNTQ3ZGMz/view">DIP</a>: “High-level modules shouldn’t depend on low-level modules. Both modules should depend on abstractions. In addition, abstractions shouldn’t depend on details. Details depend on abstractions.”</i>

The "inversion" term is used because usually software structures are created in which high-level modules depend on low-level modules and abstractions depend on details.

The next picture shows an <a href="https://code.tutsplus.com/tutorials/solid-part-4-the-dependency-inversion-principle--net-36872">example</a> of two dependencies. Two concrete classes, <em>PDFBook</em> and <em>EBookReader</em>, depend on <em>EBook</em> interface.

<center>
 <img src="/img/5Principles/dip.png" width="385">  
</center>

Respecting DIP will help us respect the other principles.

<br/>

<h3>Summary</h3>

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/khosZt-Yep4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

<br/>

<h3>References</h3>
<ul>
	<li><a href="http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod" >Principles Of OOD</a></li>
	<li><a href="https://www.amazon.com/Software-Development-Principles-Patterns-Practices/dp/0135974445/ref=sr_1_1?s=books&ie=UTF8&qid=1378755964&sr=1-1&keywords=robert+c+martin" >Agile Software Development, Principles, Patterns and Practices</a></li>
	<li><a href="https://stackify.com/solid-design-principles/" >SOLID Design Principles Explained - SRP</a></li>
	<li><a href="https://codeblog.jonskeet.uk/2013/03/15/the-open-closed-principle-in-review/" >The Open-Closed Principle, In Review</a></li>
	<li><a href="https://www.javabrahman.com/programming-principles/open-closed-principle-with-examples-in-java/" >Java Brahman - OCP</a></li>
	<li><a href="https://www.javabrahman.com/programming-principles/single-responsibility-principle-with-example-in-java/" >Java Brahman - SRP</a></li>
	<li><a href="https://code.tutsplus.com/tutorials/solid-part-3-liskov-substitution-interface-segregation-principles--net-36710" >LSP and ISP</a></li>
	<li><a href="https://code.tutsplus.com/tutorials/solid-part-3-liskov-substitution-interface-segregation-principles--net-36710" >SOLID: Part 3 - Liskov Substitution & Interface Segregation Principles</a></li>
	<li><a href="https://code.tutsplus.com/tutorials/solid-part-4-the-dependency-inversion-principle--net-36872" >SOLID: Part 4 - The Dependency Inversion Principle</a></li>
</ul>
