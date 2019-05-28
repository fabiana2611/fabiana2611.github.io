---
layout: post
title:  "Sort Algorithm"
date:   2019-05-19
categories: algorithm
permalink: /:categories/sortalgorithm
---

<p style="text-align: justify;">There are many sort algorithm you can use. Which of them should you choose? The complexity show to you about the performance.</p>
<p style="text-align: justify;">I put the main algorithm together to help to see the differences. More detail about all of them you can see in <a href="https://www.geeksforgeeks.org/fundamentals-of-algorithms/#DynamicProgramming" >GeeksforGeeks</a>.</p>

<br/>
<h3>Complexity</h3>

Based on this <a href="http://blog.benoitvallon.com/sorting-algorithms-in-javascript/sorting-algorithms-in-javascript/" >other post</a> I separate some algorithms that we can see more frequently.

<center>
  <img src="/img/sortalgorithm/tableComplexity.png" width="507" height="300">
</center>
 
<p style="text-align: justify;">There is a <a href="http://warp.povusers.org/SortComparison/integers.html" >work</a> that compare all of these algorithm. On that post, you will see that algorithms like Insertion can have better results then <span style="color: #993366;"><em>Merge</em></span> or <span style="color: #993366;"><em>Quick</em></span> sort when you have not much data. However, if you have a several numbers of data the algorithms with better results will be <em><span style="color: #993366;">Merge</span></em> and <span style="color: #993366;"><em>Quick sort</em></span>.</p>
<p style="text-align: justify;">It's possible to see that <span style="color: #993366;"><em>QuickSort</em></span> and <em><span style="color: #993366;">MergeSort</span></em> are very similar.  However, the <span style="color: #993366;"><em>QuickSort</em></span> is better if you pay attention to the space complexity <a href="https://hackernoon.com/what-does-the-time-complexity-o-log-n-actually-mean-45f94bb5bfbf" >O(log(n))</a>. But the worst case the MergeSort have a better performance.</p>
<p style="text-align: justify;">The Java's Arrays.sort() uses the <span style="color: #993366;"><em>QuickSort</em></span> algorithm. It's used to sort primitive data. The <span style="color: #993366;"><em>QuickSort</em></span> is not a <a href="https://en.wikipedia.org/wiki/Sorting_algorithm#Stability" >stable algorithm</a> and since you are working with primitive the stability is not an issue and the change of position does not make difference.</p>
<p style="text-align: justify;">On other hands, Java's Collections.sort() uses <span style="color: #993366;"><em>MergeSort</em></span>, a stable sort. This algorithm does not reorder equal elements. Since it's working with an object the stability is important.</p>
<p style="text-align: justify;">Thinking about <em><span style="color: #993366;">Heap</span></em> vs <span style="color: #993366;"><em>Quick</em></span>, both are not stable, but usually, <em><span style="color: #993366;">QuickSort</span></em> is faster than <em><span style="color: #993366;">HeapSort</span></em>. In the worst case, <span style="color: #993366;"><em>HeapSort</em></span> is better than <span style="color: #993366;"><em>QuickSort</em></span>. You will see in the <a href="http://warp.povusers.org/SortComparison/integers.html" >test</a> that the <em><span style="color: #993366;">QuickSort</span></em> result had been better when the quantity of the data was growing. More detail about this you can see <a href="http://www.meacse.org/IJCAR/archives/41.pdf" >here</a>.</p>
You also can see <a href="https://www.geeksforgeeks.org/why-quick-sort-preferred-for-arrays-and-merge-sort-for-linked-lists/" >Why Quick Sort preferred for Arrays and Merge Sort for Linked Lists?.</a>

<br/>
<h3>Illustration</h3>

<iframe width="360" height="215" src="https://www.youtube.com/embed/xWBP4lzkoyM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="360" height="215" src="https://www.youtube.com/embed/nmhjrI-aW5o" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="360" height="215" src="https://www.youtube.com/embed/OGzPmgsI-pQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="360" height="215" src="https://www.youtube.com/embed/MtQL_ll5KhQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="360" height="215" src="https://www.youtube.com/embed/JSceec-wEyw" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe width="360" height="215" src="https://www.youtube.com/embed/PgBzjlCcFvc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br/>
<h3>Conclusion</h3>

<p style="text-align: justify;">In practice we will not need to implement these algorithm. There are libraries that do this for us. But we need understand how this works to decide what to use.</p>
<p style="text-align: justify;">Also, there are many posts explain each algorithm in detail. What I want with this post is put some of them together to have a general view. It makes my choice easier.</p>

<h3>References</h3>
<ul>
	<li><a href="https://www.geeksforgeeks.org/fundamentals-of-algorithms/" >GeekforGeeks - Algorithm</a></li>
	<li><a href="http://warp.povusers.org/SortComparison/integers.html" >Comparison of several sorting algorithms: Integers</a></li>
	<li id="about-the-sorting-algorithms-series"><a href="http://blog.benoitvallon.com/sorting-algorithms-in-javascript/sorting-algorithms-in-javascript/" >About the #sorting-algorithms series</a></li>
	<li><a href="https://en.wikipedia.org/wiki/Sorting_algorithm#Stability" >Stable Algorithm - wikipedia</a></li>
	<li><p id="1f49" class="graf graf--h3 graf--leading graf--title"><a href="https://hackernoon.com/what-does-the-time-complexity-o-log-n-actually-mean-45f94bb5bfbf" >What does the time complexity O(log n) actually mean?</a></p>
</li>
</ul>
