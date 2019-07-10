---
layout: post
title:  "Java 8 - Part I [Language Enhancements]"
date:   2019-06-05
category: java
permalink: /:categories/enhancements
---

Hello, everybody!!!

This post starts a series about the changes that you can find between version 6 to 8. For now, let's see some enhancing of the Java Language.

<h3><strong>Summary</strong></h3>

<center>
  <iframe width="560" height="315" src="https://www.youtube.com/embed/Clp6WxVDhHo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

<h3><strong>Switch statement</strong></h3>

<p style="text-align: justify;">Before the Java 7, the switch statement allows you use only primitives expressions (<span style="color: #993366;">int</span>, <span style="color: #993366;">short</span>, <span style="color: #993366;">byte</span>, <span style="color: #993366;">char</span>) and <span style="color: #993366;">enumerated types</span>. A <span style="color: #993366;">float</span> or <span style="color: #993366;">double</span> will generate a compile error. Since Java 7, <span class="classname" style="color: #993366;">Strings</span> are also allowed. Now, you can use the <span class="s1">equivalent primitive numeric wrapper classes</span>: <span style="color: #993366;">Character</span>, <span style="color: #993366;">Byte</span>, <span style="color: #993366;">Short</span> and <span style="color: #993366;">Integer</span>.</p>

<p style="text-align: justify;">You should have in your mind that some scenarios can come up a compile error. For example, each <span style="color: #993366;">case</span> needs either a constant value or a final variable initialized at declaration, and each <span style="color: #993366;">case</span> needs to be unique (different values).</p>

<img src="/img/j8/switchCompilerError.png" width="546" height="159" />

<h3><strong>Literals and Underscore Characters</strong></h3>

Numeric literals can be <span style="color: #993366;">byte</span>, <span style="color: #993366;">short</span>, <span style="color: #993366;">int</span>, <span style="color: #993366;">long</span>, <span style="color: #993366;">float</span> or <span style="color: #993366;">double</span>, generally expressed in <span style="color: #000000;"><strong>decimal</strong></span> base. You can also express that using:

<ul>
	<li><strong>Octal</strong>: it uses number '0'as prefix (Ex. 017)</li>
	<li><strong>Hexadecimal</strong>: it uses number '0' followed by character 'x' as prefix (Ex. 0x2B)</li>
	<li><strong>Binary</strong>: it uses number '0'followed by 'b'or 'B' as prefix (Ex. 0b0010110)</li>
</ul>

<p style="text-align: justify;">Since version 7, you can use underscore to make it better to read. However, you cannot add underscores at the <span style="text-decoration: underline;">beginning</span> of a literal, the <span style="text-decoration: underline;">end</span> of a literal, <span style="text-decoration: underline;">right before a decimal point</span>, or <span style="text-decoration: underline;">right after a decimal point</span>.</p>

<img src="/img/j8/literalCompileError.png" width="578" height="115" />

<h3><strong><span class="s2"> Using try-with-resources statements</span></strong></h3>

<p style="text-align: justify;">The <span style="color: #993366;"><em>try-with-resource</em> </span>block comes out in Java 7. This block permit declares resource that can be closed without doing it explicitly in a <span style="color: #993366;"><em>finally</em></span> block, and that resources exist only in <em>try</em> block scope. In this feature, Java is responsible for close the resource. That structure has a <em>finally</em> block implicitly. However, you can have <em>catch</em> and/ or <span style="color: #993366;"><em>finally</em></span> blocks. The implicit finally block runs before any programmer-coded ones. If more than one resource is declared, Java closes resources in the reverse order from which it created them.</p>

<a href="https://github.com/fabiana2611/JavaVersionUpdate/blob/master/JavaVersionUpdate/src/br/bia/upgrade/objective/language/ExceptionExamples.java" ><img src="/img/j8/tryWithResource.png" width="477" height="98" /></a>

<p style="text-align: justify;">The resource in <em>try</em> block has to implement <em>java.lang.AutoCloseable</em> and his <em>close()</em> method. That interface was introduced in Java 7 and one difference between <em>AutoCloseable</em> and <em>Closable </em>is that the second one restricts the type of exception thrown to IOException.</p>

<p style="text-align: justify;"><a href="https://github.com/fabiana2611/JavaVersionUpdate/blob/master/JavaVersionUpdate/src/br/bia/upgrade/objective/language/ExceptionExamples.java" ><img src="/img/j8/tryWithResourceException.png" width="962" height="306" /></a>If the method in the <span style="color: #993366;"><em>try</em></span> block throws an exception, the java uses the <em>suppressed exception</em> idea, or accumulate the exception. So, all but the first exceptions are suppressed. However, if the exception is thrown in <span style="color: #993366;"><em>finally</em></span> block the previous exception is lost.</p>

<h3><strong><span class="s2">Multiple Exception types </span></strong></h3>

<p style="text-align: justify;">In previous versions, the catch block was used to handle only one exception (checked or unchecked). If exist more than one block,  it's necessary to respect the hierarchy of the classes, or a compile-time error is generated.</p>

<p style="text-align: justify;">Since Java 7, <i>catch block </i>is optional. However, if you don't have a <em>catch</em> block, you have to have a <span style="color: #993366;"><em>finally</em></span> block.</p>
<a href="https://github.com/fabiana2611/JavaVersionUpdate/blob/master/JavaVersionUpdate/src/br/bia/upgrade/objective/language/ExceptionExamples.java" ><img src="/img/j8/catchOptional.png" width="499" height="137" /></a>

<p style="text-align: justify;">It's also available the use of <em>multi-catch</em>. You are able to declare multiple exceptions in the same catch. In this new structure, you have to know that the variable is <em><span style="color: #993366;">final</span>, </em>it must appear only once and at the end, and you cannot combine subclasses and their superclasses in the same catch block.</p>

<a href="https://github.com/fabiana2611/JavaVersionUpdate/blob/master/JavaVersionUpdate/src/br/bia/upgrade/objective/language/ExceptionExamples.java" ><img src="/img/j8/multiCatch.png" width="447" height="178" /></a>

<h3><strong><span class="s2"> Default methods of an interface</span></strong></h3>

<p style="text-align: justify;">An interface is a contract with just methods definitions, that have to be implemented in the concrete class that implement it. If the interface implements some methods it has to be declared as abstract.</p>

<p style="text-align: justify;">An interface cannot be <span style="color: #993366;"><em>final</em></span> and the methods are <span style="color: #993366;"><em>public</em></span> and <span style="color: #993366;"><em>abstract</em></span>. The fields declared in an interface are <span style="color: #993366;"><em>constants</em></span> and by default, they are <span style="color: #993366;"><em>public</em></span>, <span style="color: #993366;"><em>static</em></span> and <span style="color: #993366;"><em>final</em></span>.</p>

<p style="text-align: justify;">Using this structure, if you add a new method definition in the interface, the classes that implement the interface will have a compile error. To fix this, it's necessary to update these classes. It'll be a problem if you have many classes, or these classes are not available or even the new method not make sense for some class.</p>

<p style="text-align: justify;">The Java 8 add the <span style="color: #993366;"><em>default</em></span> method, a method with a body and that is not an abstract method. It can be optionally overridden on the concrete class. In the same way, you can also implement a <span style="color: #993366;"><em>static</em></span> method. Now, the interface can provide behaviour. It's possible implements many <span style="color: #993366;"><em>default</em></span> methods, and each one needs to have a body.</p>

<a href="https://github.com/fabiana2611/JavaVersionUpdate/blob/master/JavaVersionUpdate/src/br/bia/upgrade/objective/language/InterfaceExamples.java" ><img src="/img/j8/interfaceDefaultMethodsStatic.png" width="590" height="282" /></a>

<p style="text-align: justify;">If you implement two interfaces with the same <em>default</em> method, a compile error will happen.</p>

<ul style="text-align: justify;">
	<li><em>Default methods cannot be final.</em></li>
	<li><em>Default methods cannot be synchronized.</em></li>
	<li><em>Default methods are always public.</em></li>
	<li><em>You cannot have default methods for the Object's class methods.</em></li>
</ul>

<h3 style="text-align: justify;"><strong><span class="s2">Use static methods of an interface</span></strong></h3>

<p style="text-align: justify;">Static methods are utility methods created to assist default methods. Static methods on interfaces are not inherited.</p>

<a href="http://ocpj8.javastudyguide.com/ch04.html" ><img src="/img/j8/interfaceStaticMethod.png" width="390" height="240" /></a>

<h3>Related Posts</h3>

<ul>
<li><a href="http://localhost:4000/java/collections.html" >Java 8 - Part VII [Collections]</a></li>
<li><a href="https://fabiana2611.github.io/java/nio" >Java 8 – Part VI [File IO NIO.2]</a></li>
<li><a href="https://fabiana2611.github.io/java/concurrency" >Java 8 – Part V [Concurreny]</a></li>
<li><a href="https://fabiana2611.github.io/java/stream" >Java 8 – Part IV [Streams]</a></li>
<li><a href="https://fabiana2611.github.io/java/lambda">Java 8 – Parte III [Lambda]</a></li>
<li><a href="https://fabiana2611.github.io/java/datetime" >Java 8 - Part II [Localization, Date, Time]</a></li>
  <li><a href="https://fabiana2611.github.io/java/enhancements" >Java 8 - Language Enhancements</a></li>
	<li><a href="https://fabiana2611.github.io/java/jvm">JVM</a></li>
</ul>

<h3><strong>Related</strong></h3>


<h3><strong>Reference</strong></h3>

<ul>
	<li><a href="http://math.hws.edu/eck/cs124/javanotes6/c3/s6.html" >The switch statement</a></li>
	<li><a href="https://docs.oracle.com/javase/tutorial/java/nutsandbolts/switch.html" >Java Tutorial - Switch Statement</a></li>
	<li><a href="http://ocpj8.javastudyguide.com/ch31.html" >OCP8: From Java 6/7 to 8</a></li>
	<li><a href="http://ocpj8.javastudyguide.com/ch19.html" >OCP8: Exceptions</a></li>
	<li><a href="http://ocpj8.javastudyguide.com/ch04.html" >OCP8: Interface</a></li>
	<li><a href="https://github.com/fabiana2611/JavaVersionUpdate" >GitHub/fabiana2611</a></li>
</ul>
