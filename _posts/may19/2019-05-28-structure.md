---
layout: post
title:  "Data Structure Curiosity"
date:   2019-05-28
categories: algorithm
permalink: /:categories/data-structure
---

Hello!!

<p style="text-align: justify;">Here, I'd like to talk about some info we have pay attention of some <a href="https://en.wikipedia.org/wiki/List_of_data_structures">data structure</a> to decide which is the best choice in your scenario. Some kind of knowledge that many times we don't pay attention in day-by-day.</p>

<h2>HashMap</h2>

HashMap is a data structure that map keys to values. In Java, it is a collection class which implements Map interface.

<ul>
	<li>Key: HashMap (1) can have only unique keys, (2) only one 'null' key.</li>
	<li>Value: It can be mapped to many keys,.</li>
	<li>This structure only store <span style="color: var(--color-neutral-600);">object references, not primitive.</span></li>
</ul>

<p style="text-align: justify;">The HashMap is <span style="color: #993366;"><strong>not thread-safe</strong></span>, so, if you need to synchronize the object, you can use <span style="color: #993366;"><em>Collections.synchronizedMap(hashMap)</em></span>, which will control all the structure (all operations - read and write), or you can use <em><span style="color: #993366;">ConcurrentHashMap</span></em> that will control only write operations. It happens because the last one locks only a portion of the object and the method <span style="color: #993366;"><em>synchronizedMap </em></span>lock the whole map. The <span style="color: #993366;"><em>HashTable</em></span> is the legacy when you needed to have a synchronized object.</p>

<strong><em>How it works</em></strong>

<p style="text-align: justify;">This sort of structure use hash principle to converts an object into an integer form. Each value resulted from the hash function will represent a position in the HashMap array. That position is an element called 'Bucket'. Then, when is given a key the process will calculate the index of the array:</p>

{% highlight ruby %}
  index = hashCode(key) & (n-1) //n is the size of the array
{% endhighlight %}

<p style="text-align: justify;">The pair key-value is stored such a node, which in Java is an instance of the inner class HashMap.Entry. The Bucket can have more than one node related. It happens in case of a collision. In that case, a linked list structure is used. From Java 8, when the number of nodes becomes larger, the structure used is a balanced tree to improve the performance.</p>

<p style="text-align: justify;">In terms of methods, It uses <em><span style="color: #993366;">hashCode</span></em> to find the position and uses <span style="color: #993366;"><em>equal</em></span> to find the key in the <em>linked list</em>. If the key exists and the operation is to add new value, the old value is replaced. If not exist a new node is created. If the operation is to retrieve the value, it will find the key and get the value. The operation to retrieve value is <span style="color: #993366;"><em>O(1)</em></span>. The worst case using a linked list is<span style="color: #993366;"><em> O(n</em>)</span> and using a balanced tree is <span style="color: #993366;"><em>O(logn). </em></span>The <em><span style="color: #993366;">tree</span></em> uses less space since is not necessary to allocate a large array.</p>

<img src="/img/datastructure/HASH.png" width="504" height="189">

You can try this structure using this <a href="https://www.cs.usfca.edu/~galles/visualization/OpenHash.html">animation</a>.

<h2>ArrayList</h2>

<p style="text-align: justify;">In some languages, arrays and list are resizable.  In Java, an array's size is defined when it is created. The ArrayList is the dynamic resizing array. The access is O(1), but when you add a new value it can have some complexity. If the array is full another one is created with the double of the size and all the elements are copied to the new array, then it can be O(n).</p>

<p style="text-align: justify;">Comparing with LinkedList, ArrayList is batter to retrieve values. If you will have many operations to add new values is better to use LinkedList.</p>

<center>
  <img src="/img/datastructure/arraylistvslinkedlist.png" width="433" height="232">
</center>

<p style="text-align: justify;">You can try the LinkedList using this <a href="https://visualgo.net/en/list">animation</a></p>

<h2>String</h2>

<p style="text-align: justify;">Strings are immutable and always create a new object. Each new String object is stored in the <a href="https://www.journaldev.com/797/what-is-java-string-pool" >pool</a> to the application reuse the objects.</p>

{% highlight ruby %}
  String str = "abc"; //the object in the pool is used
  String str2 = new String("abcd"); // create a reference</pre>
{% endhighlight %}


<center>
  <img src="/img/datastructure/string-pool-java.png" width="450" height="249">
  <br/>
  <em>from post: <a href="https://www.journaldev.com/797/what-is-java-string-pool" >What is Java String Pool</a></em>
</center>
<br/>

<p style="text-align: justify;">If you need to update the same object many times you should use String Builder. It updates the existing object value.</p>

<p style="text-align: justify;">String Builder and String Buffer use the same instance to update the object. The difference between them is that the Spring Buffer is synchronized (thread-safe).</p>

<h2>Stacks and Queues</h2>

<p style="text-align: justify;"><a href="https://www.studytonight.com/data-structures/stack-data-structure"><strong>Stack:</strong></a> LIFO (<a href="https://en.wikipedia.org/wiki/FIFO_and_LIFO_accounting#LIFO">last-in, first-out</a>) | pop, push, peek: O(1) | lookup: O(n)</p>

<p style="text-align: justify;"><a href="https://www.studytonight.com/data-structures/queue-data-structure"><strong>Queues:</strong></a> FIFO (<a href="https://en.wikipedia.org/wiki/FIFO_(computing_and_electronics)">first-in, first-out</a>) | enqueue, dequeue, peek: O(1) | lookup: O(n) </p>

<center>
  <img src="/img/datastructure/stackqueue.png" width="350" height="249">
</center>
<br/>

<h2>Big O Common Data Structure</h2>

<br/>
<center>
  <img src="/img/datastructure/bigo.png" width="650" height="449">
</center>
<br/>

<p>You can see more detail about that in <a href="https://www.bigocheatsheet.com/">Big O Cheat Sheet</a></p>

<h2>References</h2>

<ul>
	<li class="entry-title"><a href="https://www.geeksforgeeks.org/internal-working-of-hashmap-java/" >Internal Working of HashMap in Java</a></li>
	<li><a href="https://howtodoinjava.com/java-hashmap/" >Java HashMap</a></li>
</ul>
