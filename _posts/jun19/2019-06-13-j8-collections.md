---
layout: post
title:  "Java 8 - Part VII [Collections]"
date:   2019-06-13
categories: java
permalink: /:categories/collections
---

<p style="text-align: justify;">Let's start the seventh post of the Java 8 series about the changes that you can find from version 6 to 8, the Collections.</p>
<p style="text-align: justify;">You will see some subject already mentioned in the <a href="https://fabiana2611.github.io/java/stream" >stream post</a>, but I consider important to have a separate post to this subject.</p>

<h2>Summary</h2>
<center>
  <iframe width="560" height="315" src="https://www.youtube.com/embed/g5IK0XqwYXo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>
<br/>

<h2>Introduction</h2>
<blockquote>A collection is a group of objects contained in a single object.</blockquote>
The main interfaces in the Collections Framework are:
<ul>
	<li><a href="http://www.java2s.com/Tutorials/Java/Java_Collection/0130__Java_List.htm" >List</a>: an ordered collection of elements; it allows duplicate entries. It does not limit the null elements
<ul>
	<li style="text-align: justify;"><a href="https://www.geeksforgeeks.org/arraylist-in-java/" >ArrayList</a>: dynamic arrays. It's not synchronized, allow null values and maintenance the insertion order. It can not be used by primitives.</li>
	<li style="text-align: justify;"><a href="https://www.geeksforgeeks.org/applications-of-linked-list-data-structure/" >LinkedList</a>: the elements are not stored side-by-side. They are linked by pointers. Each element specifies previews and next elements.</li>
</ul>
</li>
	<li><a href="https://www.geeksforgeeks.org/internal-working-of-sethashset-in-java/" >Set</a>: it's not ordered collection and it does not allow duplicate entries. It allows only one null element.
<ul>
	<li>The <a href="https://howtodoinjava.com/java/collections/java-hashset/" >HashSet</a> works like HashMap but not allow duplicate elements.</li>
</ul>
</li>
	<li><a href="https://www.geeksforgeeks.org/queue-data-structure/" >Queue</a>: ordered for a process (FIFO - first-in, first-out)</li>
	<li><a href="http://www.java2s.com/Tutorials/Java/Java_Collection/0180__Java_Map.htm" >Map</a>: it maps keys to values; it does not allow duplicate key.
<ul>
	<li style="text-align: justify;"><a href="https://howtodoinjava.com/java-hashmap/" >HashMap</a> implements Map interface. You can see the internal working in this <a href="https://www.geeksforgeeks.org/internal-working-of-hashmap-java/" >post </a>on <a href="https://www.geeksforgeeks.org/" >GeeksforGeeks</a>. You will see that Java 8 change the implementation to solve collision. Now Java 8 began using <strong>linked-list</strong> and as soon as the threshold is reached the hash will change to use a <strong>balanced tree</strong>.
<ul>
	<li><a href="https://www.geeksforgeeks.org/linkedhashmap-class-java-examples/" >LinkedHashMap</a>: similar to the HashMap but now you can access the elements by their insertion order.</li>
</ul>
</li>
	<li style="text-align: justify;"><a href="https://www.geeksforgeeks.org/hashtable-in-java/" >HashTable</a> also implements Map interface. The main differences between the HashTable and the HashMap are that the first one does not allow to use null value to the key or to the value and it is synchronized, which is an important reason to make the performance worst comparing with HashMap. The <span style="color: #993366;"><em>ConcurrentHashMap</em></span> (from Executor framework) is similar to HashTable, but the ConcurrentHashMap has a better performance.  ConcurrentHashMap read data using get() without locks (the locking is applied only for updates), by another hand, the HashTable is synchronized for all operation (single lock for whole data). More detail about the differences you can see on this other <a href="https://www.geeksforgeeks.org/differences-between-hashmap-and-hashtable-in-java/" >GeeksforGeeks post</a>. And an implementation you can see <a href="https://www.geeksforgeeks.org/implementing-our-own-hash-table-with-separate-chaining-in-java/" >here</a>.</li>
	<li style="text-align: justify;"><a href="https://www.geeksforgeeks.org/hashmap-treemap-java/" >TreeMap</a> implements a child of Map interface, the SortedMap. It's useful to use with unique elements and where is necessary to have sorted elements (natural order or using Comparable interface).</li>
</ul>
</li>
</ul>

<center>
  <img src="/img/j8/collection-hierarchy.png" width="719" height="320" />
  <br/>
  <em><a href="https://howtodoinjava.com/interview-questions/useful-java-collection-interview-questions/" >HowToDoInJava - Java Collection</a></em>
</center>
<br/>
 
<p style="text-align: justify;">Another post also addresses the topic Java collection. If you want a little more about this go to the Marcus Biel <a href="https://dzone.com/articles/an-introduction-to-the-java-collections-framework" >Java Collection post</a> in <a href="https://dzone.com/" >DZone</a>.</p>

<h2><b style="font-size: x-large; font-family: Times-Roman, serif;">Using the Diamond Operator</b></h2>
<p style="text-align: justify;">From Java 7, you can omit the type of the generic class from the right side, but the diamond operator ('<>') is required yet.</p>

{% highlight ruby %}
# Before
Map<Map<String,Integer>, List> map1  =
       new HashMap<Map<String,Integer>, List>();

# New Version
Map<Map<String,Integer>, List> map2 = new HashMap<>();

# DOES NOT COMPILE
Map<> map2 = new HashMap<Map<String,Integer>, List>();
{% endhighlight %}

<p style="text-align: justify;">The compiler will fill the type with the type declared on the right side. The diamond is limited to be used only on right side.</p>

<h2 style="text-align: justify;">Iterates, filters and sorts (using lambda)</h2>
<p style="text-align: justify;">To <strong>iterate</strong> through the collection you can do this using <em><span style="color: #993366;">forEach</span></em> loop, the index, while loop (see this HowToDoInJava <a href="https://howtodoinjava.com/java/collections/different-ways-to-iterate-over-collections-in-java/" >post</a> to examples). But you don't need to navigate each element in every case. If you want to search some elements it's possible to use the <em><span style="color: #993366;">binarySearch</span></em> method to do this. But the list needs to be sorted.</p>

{% highlight ruby %}
# Array
int[] n = {6,9,1,8}
Arrays.sort(n); // [1,6,8,9]
Arrays.binarySearch(n,6)); // the result is the index '1'

# List
List l = Arrays.asList(9,7,5,3);
Collections.sort(l);
Collections.binarySearch(l,3); // the result is the index '0'

# Stream
Stream.iterate(1L, n->n*2).limit(10).forEach(System.out::print);
{% endhighlight %}

<p style="text-align: justify;">To <strong>sort</strong> a collection you need to know how to compare the elements. So, you can use the <em><span style="color: #993366;">Comparator</span></em> interface with <em>inner class</em> or using <em>lambda expression</em>. It's possible to say that <span style="color: #993366;"><em>Comparator</em></span> is a functional interface because it has a single abstract method. If it's necessary you can use a not natural order with <em><span style="color: #993366;">reverseOrderMethod</span></em>.</p>

{% highlight ruby %}
# inner class
Comparator byWeight = new Comparator() {
    public int compare(A a1, A a2) {
         return a1.getWeight() - a2.getWeight();
    }
};

# Lambda
Comparator byWeight =
    (A a1, A a2) -> {return a1.getWeight() - a2.getWeight(); };

# Reverse Order
List l = Arrays.asList(1,2,3);
Comparator c = Comparator.reverseOrder();
Collections.binarySearch(l,3,c);
{% endhighlight %}

Also you can use <strong>filters</strong> in the collections. The Streams accept the <span style="color: #993366;"><em>Predicate</em></span> interface to apply in the collection.  Example you can see <a href="https://www.mkyong.com/java8/java-8-streams-filter-examples/" >here</a>, compare before and after Java 8.

{% highlight ruby %}
Predicate pred = e -> e % 2=0;
collection.stream.filter(pred).collect(Collectors.toList());
{% endhighlight %}

<h2>Java SE 8 collection improvements</h2>
<p style="text-align: justify;">Java 8 introduced new methods to help us to manipulate the collections. One of them was the <em><span style="color: #993366;">removeIf</span></em> method to remove an element using a condition. Another one was the <em><span style="color: #993366;">replaceAll</span></em>, where you pass a lambda expression and to apply to each element. You can use the <em><span style="color: #993366;">forEach</span></em> loop to navigate by the list and do something.</p>

{% highlight ruby %}
List list = Arrays.asList(1,2,3,4,5);
list.removeIf( i -> s > 3);
list.replaceAll( i -> i*2);
list.forEach( i -> System.out.println(i));
{% endhighlight %}

<p style="text-align: justify;">The <span style="color: #993366;">Map</span> also added new methods such <em><span style="color: #993366;">merge </span></em>that add a new element with a logic.</p>

{% highlight ruby %}
# merge
Map<String, String> map = new HashMap<>();
map.put("key1", "value1");
map.put("key2", null);

BiFunction<String, String, String> logic =
    (v1,v2) -> v1.length() > v2.length() ? v1:v2;

String result1 = map.merge("key1", "new", logic);
// Result1 = value1;
String result2 = map.merge("key1", "newValue1", logic);
// Result2 = newValue1;
System.out.println(map.get("key1")); // {key1=newValue1}

# putIfAbsent - add new value if not exist or value is null
map.putIfAbsent("key2", "value2");
map.putIfAbsent("key1", "value3");
System.out.println(map); // {key1=newValue1, key2=value2}
{% endhighlight %}

<p style="text-align: justify;">The <span style="color: #993366;"><em>computeIfPresent</em></span> is another method to map and runs only when the key isn’t present or is null. And <span style="color: #993366;"><em>computeIfAbsent</em></span> do the opposite.</p>

{% highlight ruby %}
# computeIfPresent
Map<String, Integer> total = new HashMap<>();
map.put("key1", 1);
map.put("key2", null);

BiFunction<String, String, String> logic =
  (v1,v2) -> v1 + 1;

Integer k1 = total.computeIfPresent("key1", logic); // k1 = 2
Integer k3 = total.computeIfPresent("key3", logic); // k2 = null

# computeIfAbsent
Function<String, Integer> func = k -> 99;
total.computeIfAbsent("key1", func); // 1
total.computeIfAbsent("key2", func); // 99
total.computeIfAbsent("key3", func); // 99
{% endhighlight %}

<h2>Streams</h2>
<p style="text-align: justify;">The <a href="https://fabiana2611.github.io/java/stream" >stream</a> in java is a sequence of data which you can execute operation and get a result. It's not a collection. The Stream API was introduced to process elements in sequence.  The stream wraps an existing collection to support operations expressed with lambdas, so you specify what you want to do, not how to do it.</p>
Some <a href="https://www.java2novice.com/java_interview_questions/java-8-streams-vs-collection-framework/" >differences of the stream from the collection</a> are:
<ul>
	<li style="text-align: justify;"><b><i>No storage.</i></b> A stream gets each element from a source (data structure, an array, a generator function) and processes through a pipeline of computational operations.</li>
	<li style="text-align: justify;"><b><i>Functional in nature.</i></b> An operation on a stream produces a result but does not modify its source.</li>
	<li style="text-align: justify;"><b><i>Laziness-seeking.</i></b> Many stream operations can be implemented lazily.</li>
	<li style="text-align: justify;"><b><i>Possibly unbounded.</i></b> It's possible to work with infinite size using streams throughout short-circuiting operations such as limit(n) or findFirst().</li>
	<li style="text-align: justify;"><b><i>Consumable.</i></b> The elements of a stream are only visited once during the life of a stream.</li>
</ul>

<p style="text-align: justify;"> The Stream pipeline is the set of operations chained, which can be the intermediate operations and terminal operations.</p>

<ul>
	<li style="text-align: justify;">Intermediate Stream: execute operation where is possible to manipulate the stream and the result is another stream.</li>
	<li style="text-align: justify;">Terminal operator: execute the operator to get a result different of the stream.</li>
</ul>

<h4>Intermediate Stream Operation</h4>

<ul>
	<li style="text-align: justify;"><span style="color: #993366;">flatMap</span>: "<em>It takes each element in the stream and makes any elements it con</em><em>tains top-level elements in a single stream</em>". It is usual to remove empty elements of when you are using a list with a list.</li>
</ul>  
{% highlight ruby %}
Stream.of(Arrays.asList(), Arrays.asList("a"), Arrays.asList("b"))
        .flatMap (l->l.stream()).forEach(System.out::print); //ab
{% endhighlight %}

<ul>  
	<li style="text-align: justify;"><span style="color: #993366;">map</span>: "<em>It creates a one-to-one mapping from the elements in the stream to the ele</em><em>ments of the next step in the stream</em>"</li>
</ul>
{% highlight ruby %}
Stream.of("a","b","c").map(String::length).forEach(System.out::print); //111
{% endhighlight %}

<h4>Terminal Stream Operation</h4>

<em>Search for data:</em>
<ul>
  <li style="text-align: justify;"><span style="color: #993366;">findAny/findFirst</span>: It return a Optional< T > object. To an empty stream, the return will be an empty Optional return. It works with an infinite stream. These methods do not need to process all the elements. The findAny method is useful to work with a parallel stream.</li>
</ul>  
{% highlight ruby %}
Stream.of("a","b","c")
      .findAny().ifPresent(System.out::println); //a
{% endhighlight %}

<ul>
  <li style="text-align: justify;"><span style="color: #993366;">allMatch/anyMatch/noneMatch</span> : the return is a boolean type related to the predicate passed. The <span style="color: #993366;">allMatch</span> and the <span style="color: #993366;">noneMatch</span> methods cannot be working in an infinite stream.</li>
</ul>
{% highlight ruby %}
Predicate<String> pred = x->Character.isLetter((x.charAt(0));
Stream.of("a","bb","cc", "1").anyMatch(pred); //
{% endhighlight %}

<em>Reduction operator</em>

<ul>
  <li style="text-align: justify;"><span style="color: #993366;">collect</span>: it does not terminate an infinite execution. It is a reduction operator.</li>
  <li style="text-align: justify;"><span style="color: #993366;">min/max</span>: It allows find smallest or largest value. It returns an Optional< T > object to be able to represent no value. In an infinite stream, it cannot terminate the process.</li>
</ul>
{% highlight ruby %}
Stream.of("a","bb","cc")
    .min((s1,s2)->s1.length()- s2.length()); //a
{% endhighlight %}

<ul>
  <li style="text-align: justify;"><span style="color: #993366;">count</span>: it returns a long number the represents the number of elements in a stream.  It does not terminate execution in case of the infinite stream.</li>
</ul>
{% highlight ruby %}
Stream.of ("a","b","c").count(); // 3
{% endhighlight %}

<br/>
<h4>Group the results</h4>
<ul>
	<li><span style="color: #993366;">averagingDouble/averagingInt/averagingLong: </span>return the average to the collect
<ul>
	<li>
  {% highlight ruby %}
  System.out.print(Stream.of ("a","b","c")
     .collect(Collectors.averagingInt(String::length))); // (1+1+1)/3
  {% endhighlight %}
</li>
</ul>
</li>
	<li><span style="color: #993366;">joining: </span>it creates a single string.
<ul>
	<li>
  {% highlight ruby %}
  System.out.print(Stream.of ("a","b","c")
          .collect(Collectors.joining(","))); // a,b,c
  {% endhighlight %}
</li>
</ul>
</li>
	<li><span style="color: #993366;">groupingBy: </span>it will create a map using a Function.
<ul>
	<li>
  {% highlight ruby %}
  Map<Integer, List<String>> map = Stream.of ("a","b","cc","dd")
    .collect(Collectors.groupingBy(String::length));
  System.out.print(map); // {1=[a,b], 2=[cc,dd]}
  {% endhighlight %}
</li>
</ul>
</li>
	<li><span style="color: #993366;">partitioningBy: </span>it will create a map using a Predicate.
<ul>
	<li>
  {% highlight ruby %}
  Map<Boolean, List<String>> map = Stream.of ("a","b","cc","dd")
    .collect(Collectors.partitioningBy(s->s.length() <2 ));
  System.out.print(map); // {false=[cc,dd], true= [a,b]}
  {% endhighlight %}
</li>
</ul>
</li>
</ul>
<h4>Optional With Primitive Streams</h4>
<ul>
	<li><span style="color: #993366;">average</span>: it returns a optional type to primitive (ex. OptionalDouble)
<ul>
	<li>
<pre>IntStream.rangeClosed(1,10).average();</pre>
</li>
</ul>
</li>
</ul>
<ul>
	<li><span style="color: #993366;">sum</span>: It does not return optional type
<ul>
	<li>
  {% highlight ruby %}
  IntStream.rangeClosed(1,10).sum();
  {% endhighlight %}
</li>
</ul>
</li>
	<li><span style="color: #993366;">min:/max</span>:
<ul>
	<li>
<pre>IntStream.rangeClosed(1,10).min();</pre>
</li>
</ul>
</li>
</ul>
<h2>Related Posts</h2>
<ul>
	<li><a href="https://fabiana2611.github.io/java/nio" >Java 8 – Part VI [File IO NIO.2]</a></li>
  <li><a href="https://fabiana2611.github.io/java/concurrency" >Java 8 – Part V [Concurreny]</a></li>
  <li><a href="https://fabiana2611.github.io/java/stream" >Java 8 – Part IV [Streams]</a></li>
  <li><a href="https://fabiana2611.github.io/java/lambda">Java 8 – Parte III [Lambda]</a></li>
  <li><a href="https://fabiana2611.github.io/java/datetime" >Java 8 - Part II [Localization, Date, Time]</a></li>
    <li><a href="https://fabiana2611.github.io/java/enhancements" >Java 8 - Language Enhancements</a></li>
</ul>
<h2>Reference</h2>
<ul>
	<li><a href="http://ocpj8.javastudyguide.com/ch07.html" >OCP8 - Collection</a></li>
	<li><a href="http://pdf.th7.cn/down/files/1603/Oracle%20Certified%20Professional%20Java%20SE%208%20Programmer%20Exam%201Z0-809.pdf" >OCP Oracle Cetified Professional Java SE 8  Programmer II – Study Guide</a></li>
	<li><a href="https://github.com/java8/Java8InAction" >Java In Action – Github</a></li>
	<li><a href="https://howtodoinjava.com/java-collections/" >HowToDoInJava</a></li>
	<li><a href="http://www.java2s.com/Tutorials/Java/Java_Collection/index.htm" >java2s.com</a></li>
</ul>
