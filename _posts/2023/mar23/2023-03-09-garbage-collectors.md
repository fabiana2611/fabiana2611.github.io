---
layout: post
title:  "Garbage Collection (GC) Algorithms"
date:   2023-03-09
categories: java
permalink: /:categories/garbage-collectors
---

<p><b>Garbage collector (GC):</b> the component risponsable to manage the application heap, removing the unused objects.</p>
<p><b>Summary:</b> Allocate memory to the application, detect memory not used anymore by the application, provides more memory to the application.</p>
<p><b>Simple steps:</b> (1) Mark: identify pieces of memory are in use and not; (2) Sweep: Remove objects identified in the previous step.</p>

<p style="text-align: justify;">JDK provides different garbage collection algorithms to be used the one that fit better with the application. The metrics to pay attention to the choice are throughput, latency andm emory footprint.</p>

<ul>
  <li>Throughput: collection work per time unit</li>
  <li>Latency: duration of a single operation</li>
  <li>Memory footprint: extra memory necessary to GC operation</li>
</ul>  


<p>
  <center>
    <iframe width="360" height="215" src="https://www.youtube.com/embed/XXOaCV5xm9s" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
  </center>
</p>

<br />
<h2>Serial</h2>

<p><b>Focus:</b>  Footprint and startup time</p>
    
<ul>
  <li>Works with a single thread</li>
  <li>Pause the application threads</li>
  <li>Heap organized in generation</li>
  <li>Not good to use in multi-thread applications. It is suitable for small, short-running applications</li>  
</ul>

{% highlight ruby %}
java -XX:+UseSerialGC -jar Application.java
{% endhighlight %}


<br />
<h2>Parallel</h2>

<p><b>Focus: </b>Throughput</p>

<ul>
  <li>Default for JDK 8 and earlier</li>
  <li>Works with multiple thread</li>
  <li>Copy the in-use memory to other locations in the heap</li>
  <li>Can pause the application</li>
  <li>Generational collector that maximizes garbage collection efficiency</li>
</ul>

{% highlight ruby %}
// Numbers of threads
-XX:ParallelGCThreads=<N>
// Time of pause  
-XX:MaxGCPauseMillis=<N>.  
// Maximum throughput: 
-XX:GCTimeRatio=<N>  
// Maximum heap footprint
-Xmx<N>

// Enable
java -XX:+UseParallelGC -jar Application.java  
{% endhighlight %}

<br />
<h2>Garbage First (G1)</h2>

<p><b>Focus:</b> Balanced Performance between throughput and latency.</p>

<ul>
  <li>Introduced in JDK 6 and fully supported in JDK 7</li>
  <li>Default since JDK 9</li>
  <li>Key technique: generational garbage collection</li>
  <li>Partition heap with the same size</li>
  <li>G1 splits the work in old-generation section into two phases: (1) identify live objects concurrently with the application (remove this kind of operation from FC pauses), reducing the latency; (2) G1 incrementally reclaims memory from the old generation. Reclaiming the old generation incrementally reduce the pause times. it partitions the heap into a set of equal-sized heap regions The default value for the pause time is 200 ms</li>
  <li>Similar to Parallel but avoid lengthy operations in the pauses</li>
  <li>The work is concurrent of the application: decreases the times of the pauses but impact in the throughput.</li>
  <li>Indicated to applications running on multi-processor machines with large memory space.</li>
</ul>

{% highlight ruby %}
java -XX:+UseG1GC -jar Application.java
{% endhighlight %}


<p>
  <center>
    <iframe width="360" height="215" src="https://www.youtube.com/embed/X8w3uqN-X98" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
  </center>
</p>


<br />
<h2>Z Garbage Collector (ZGC)</h2>

<p><b>Focus: </b>Latency</p>

<ul>
  <li>Since JDK 15</li>
  <li>Impact in the throughput</li>
  <li>Extremely small pauses</li>  
  <li>Partition the heap in different sizes</li>  
  <li>Colored pointers: uses some bits (metadata bits) of reference to mark the state of the object</li>  
  <li>Useful to application which require low latency or use a large heap</li>  
</ul>

{% highlight ruby %}
java -XX:+UnlockExperimentalVMOptions -XX:+UseZGC Application.java
// Numbers of threads
-XX:ConcGCThreads=<N>  
{% endhighlight %}


<p>
  <center>
   <iframe width="360" height="215" src="https://www.youtube.com/embed/7k_XfLGu-Ts" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
  </center>
</p>


<h2>Shenandoah</h2>

<p><b>Focus: </b>Latency</p>

<ul>
  <li>Since JDK 12</li>
  <li>Impact in the throughput</li>
  <li>More CPU intensive</li>
  <li>Small pauses</li>
</ul>

{% highlight ruby %}
-XX:+UseShenandoahGC
{% endhighlight %}

<p>
  <center>
    <iframe width="360" height="215" src="https://www.youtube.com/embed/N0JTvyCxiv8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
  </center>
</p>


<h2>ZGC vs Shenandoah</h2>

<p>
  <center>
    <iframe width="360" height="215" src="https://www.youtube.com/embed/WU_mqNBEacw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
  </center>
</p>



<br />
<h2>References</h2>
<ul>
  <li><a href="https://blogs.oracle.com/javamagazine/post/java-garbage-collectors-evolution">Java garbage collection: The 10-release evolution from JDK 8 to JDK 18</a></li>
  <li><a href="https://www.baeldung.com/jvm-garbage-collectors">JVM Garbage Collectors</a></li>
  <li><a href="https://docs.oracle.com/en/java/javase/18/gctuning/available-collectors.html#GUID-45794DA6-AB96-4856-A96D-FDE5F7DEE498">Serial</a></li>
  <li><a href="https://docs.oracle.com/en/java/javase/18/gctuning/parallel-collector1.html">Parallel</a></li>
  <li><a href="https://docs.oracle.com/en/java/javase/18/gctuning/z-garbage-collector.html#GUID-8637B158-4F35-4E2D-8E7B-9DAEF15BB3CD">Z Garbage Collector</a></li>
  <li><a href="https://wiki.openjdk.org/display/shenandoah/Main">Shenandoah</a></li>
  <li><a href="https://developers.redhat.com/articles/2021/11/02/how-choose-best-java-garbage-collector#">How to choose the best Java garbage collector</a></li>
  <li><a href="https://fabiana2611.github.io/java/jvm">JVM</a></li>
</ul>  
