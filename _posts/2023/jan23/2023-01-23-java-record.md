---
layout: post
title:  "Java - Record"
date:   2023-01-23
categories: java
permalink: /:categories/java-record
---

<p style="text-align: justify;">The Record feature is part of the <a href="https://openjdk.org/projects/amber/">Project Amber</a>, <em>an effort to explore and incubate smaller, productivity-oriented Java features</em>. This feature was introduced in <a href="https://docs.oracle.com/en/java/javase/14/language/records.html">Java 14</a> and is going being improved step by steps. For release 20, e.g, you can see <a href="https://openjdk.org/jeps/432">here</a>.</p>

<p style="text-align: justify;"><em>A record class is a shallowly immutable, transparent carrier for a fixed set of values, called the record components <a href="https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Record.html">[1]</a></em></p>

<p style="text-align: justify;">The <a href="https://openjdk.org/jeps/395">Record</a> is a class type in java to be used to data carrier. It has:</p>
<ul>
  <li>canonical constructor (same accessibility of the record)</li>
  <li>private final fields</li>
  <li>Getters methods for each field</li>
  <li>Equals method</li>
  <li>HashCode method</li>
  <li>ToString method.</li>
</ul>

<p style="text-align: justify;">The responsibility for creating all these methods lies with Java Compiler. All these methods can be override.</p>

<br/>
<h2>How to use the record</h2>

<p style="text-align: justify;">The records are a implementation of the Value Object pattern where the instances are imutable. They don't use the bean conventions using "get" in the methods to access the attributes.</p>

<p style="text-align: justify;">To create a record is necessary to use the keyword <b>record</b> and declare the attributes. The compiler will create the methods to access the attributes (Getters), all-arguments constructor, toString, equals, hashCode. Pay attention that the Setters will not be created. Furthermore, this class cannot have subclass because it is marked as final class.</p>


{% highlight ruby %}
record FirstRecord (int att1, String att2, double att3, Object att4){
}

public class MyFirstRecord {

  public static void main(String[] args) {

    FirstRecord fr = new FirstRecord(1, "abc", 0, null);

    System.out.println(fr.att1());
    System.out.println(fr.att2());
    System.out.println(fr.att3());
    System.out.println(fr.att4());
    System.out.println(fr);
  }
}

# Console
1
abc
0.0
null
FirstRecord[att1=1, att2=abc, att3=0.0, att4=null]
{% endhighlight %}

<p style="text-align: justify;">Even though the record gives the constructor, it can be explicit for some validation purposes. In the same way, it's possible to create a non-arg constructor (not recommended). For non-arg constructor, you have to call explicitly the arg-constructor anyway. In case of add new attribute, it should be static.</p>

{% highlight ruby %}
record FirstRecord (int att1, String att2, double att3, Object att4){

  static String newAtt;

  FirstRecord() {
    this (0, "", 0, null);
  }
}
{% endhighlight %}

<p style="text-align: justify;"> The record support generics and annotations. It also support instance methods and static methods.</p>.

{% highlight ruby %}
record FirstRecord<T> (@Transient Long att1, String att2, T att){
  public String process() {
    return "Att2: " + att2;
  }
  public static void test(FirstRecord myRecord) {
      System.out.println(myRecord.att1);
  }
}

MyRecord<Integer> fr = new MyRecord<>(1L, "test", 2);

System.out.println(fr.process());
FirstRecord.test(fr);
{% endhighlight %}


<p style="text-align: justify;">Another point is that Records can implement interfaces (implements) but cannot extend other records. </p>


<br/>
<h2>When to use the record</h2>

<p style="text-align: justify;">It is indicated to use as domain model class or data transfer objects, e.g, when it's not necessary to change the values.</p>

<p style="text-align: justify;">However, it can be painful in cases where you have many attributes and most of then are null.</p>

<p style="text-align: justify;">The record is flexible to be customized. However, if you need to do this a lot, maybe the record is not the best option for you.</p>

<br/>
<h2>Record vc Lombok</h2>

<p style="text-align: justify;"><a href="https://projectlombok.org/">Lombok</a> is a external library to auto-generate some common patterns avoiding boilerplate. It helps to create immutable objects with @Value annotation. Lombok is more mature and is more flexible. Also, lombok can add some validations to validate fields. Beside,it has @Data annotation if is necessary change data. Another good point is the fact that Lombok can use the @Builder annotation to facilitate the object creation.</p>

<p>Analysis by <a href="https://www.baeldung.com/java-record-vs-lombok">cases</a>:</p>
<ol>
  <li>Classes with many fields
    <ul>
      <li>Record: instantiation can be hard especially if some of the fields aren't mandatory (better for smaller objects)</li>
      <li>Lombok: provides implementation of the Builder  design pattern</li>
    </ul>
  </li>
  <li>Mutable Data
    <ul>
      <li>Record is exclusively for immutable data. Not inficate for frameworks that require Setters methods (as hibernate)</li>
      <li>Lombok can use @Data to be mutable. When creating an @Entity, Lombok can be a better choice.</li>
    </ul>
  </li>
  <li>Inheritance
    <ul>
      <li>Record do not support inheritance.</li>
      <li>Lombok can use @Data objects that can both extend other classes and be extended.</li>
    </ul>
  </li>
</ol>


<br/>
<h2>Conclusion</h2>

<p style="text-align: justify;">Lombok is the best option for many scenarios. However, it's good override it as soon as possible. The plans are to improve the record for each version.</p>

<br />
<h3>References</h3>
<ul>
  <li><a href="https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/lang/Record.html">Java Record - Java Doc</a></li>
  <li><a href="https://howtodoinjava.com/java14/java-14-record-type/">Java record Type with Examples</a></li>
  <li><a href="https://www.baeldung.com/java-record-vs-lombok">Java 14 Record vs. Lombok</a></li>
  <li><a href="https://blogs.oracle.com/javamagazine/post/records-come-to-java">Records Come to Java</a></li>
</ul>  
