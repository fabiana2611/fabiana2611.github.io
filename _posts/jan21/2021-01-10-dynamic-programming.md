---
layout: post
title:  "Dynamic Programming"
date:   2021-01-09
categories: foundation
permalink: /:categories/dynamic-programming
---

<p style="text-align:justify;">Dynamic programming (<strong>DP)</strong> is a technique to solve polynomial problems through the reuse idea. It's similar to divide-and-conquer where you will break to the smaller problem and reuse the results to find the final solution.</p>

<center>
<a href="https://www.geeksforgeeks.org/dynamic-programming-vs-divide-and-conquer/"><img class="  wp-image-1211 aligncenter" src="/img/dp/diagrama.png" alt="diagrama.png" width="279" height="216"></a>
<br/>
<em>Font: GeeksForGeeks</em>
</center>
<br/>

<p style="text-align:justify;">Usually, problems to maximize or minimize can be solved using DP. However, to a problem to be considered a DP it needs to fit with certain restrictions or prerequisites. Then, to a problem to be considered solved by DP it has to have:</p>

<ul>
 	<li style="text-align:justify;"><a href="https://en.wikipedia.org/wiki/Optimal_substructure">optimal substructure</a>: <em>optimal solution can be constructed from optimal solutions of its subproblems</em></li>
 	<li style="text-align:justify;"><a href="https://en.wikipedia.org/wiki/Overlapping_subproblems">overlapping sub-problem</a>: <em>the problem can be broken down into subproblems which are reused several times or a recursive algorithm for the problem solves the same subproblem over and over rather than always generating new subproblems. </em>The techniques to resolve the problems are<a href="https://www.geeksforgeeks.org/tabulation-vs-memoization/"> <strong>memorization</strong>&nbsp;and <strong>tabulation</strong></a>.</li>
</ul>
<p style="text-align:justify;">If a problem doesn't fit with these two attributes it's just in the divide-and-conquer strategy. That's why the merge sort and quick sort are not classified as dynamic programming problems.</p>
We can summarize how to identify if a problem solved using DP in the <a href="https://dev.to/nikolaotasevic/dynamic-programming--7-steps-to-solve-any-dp-interview-problem-3870">steps</a>:
<ol>
 	<li>Identify problem variables</li>
 	<li>Clearly express the recurrence relation</li>
 	<li>Identify the base cases</li>
 	<li>Decide if you want to implement it iteratively or recursively</li>
</ol>
<p style="text-align:justify;">Steps 1, 2 and 3 are related to the state of the transition. Then, the DP is regarding find a relation between previous states and the current state.</p>

<ul>
 	<li style="text-align:justify;"><a href="https://www.geeksforgeeks.org/solve-dynamic-programming-problem/"><b>State</b></a>: <em>A state can be defined as the set of parameters that can uniquely identify a certain position or standing in the given problem. This set of parameters should be as small as possible to reduce state space.</em></li>
</ul>
<p style="text-align:justify;">One example is the Fibonacci problem [<a href="https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/">1</a>][<a href="https://www.educative.io/courses/grokking-dynamic-programming-patterns-for-coding-interviews/m2G1pAq0OO0">2</a>]. Using recursive solution the time complexity is O(2^n) while the DP solution only O(n).</p>

<br/>
<center>
<img class=" size-full wp-image-1210 aligncenter" src="/img/dp/fibonacci.png?w=678" alt="fibonacci.png" width="449" height="418">
</center>
<br/>

<p style="text-align:justify;">The first method (fibRec) solves the problem using the memorization idea, with recursive calls and star the state in N (TopDown). The second method (fibDP) uses the tabulation idea with the initial state started by '1' (BottomUp). The first strategy is easier to think and implement, however, it uses recursivity, which makes the second one, the iterative way, faster than the first method.</p>

<p style="text-align:justify;">The solution can be improved using cache. The figure bellow is an example given by <a href="https://medium.com/@isachenx/understanding-caching-with-memoize-and-fibonacci-numbers-3a6f174af90a">Isabella Chen</a> in his post.</p>

<br/>
<center>
<img src="/img/dp/fibo_cache.png?w=678" width="349" height="218">
</center>
<br/>

<h2>Recursion: Pay Attention to the stack</h2>

<p style="text-align:justify;">You have to pay attention how you are using the recursion. When the values are bing passed to be calculate on the end of the process you will have a stack with many values. It can throw errors because of a full stack. </p>

<p style="text-align:justify;">The example bellow (fibonacci) show how the stack is going to be used to process all the result in the end, going back each step when have values the be processed.</p>

<br/>
<center>
<img src="/img/dp/stack.png" width="649" height="218">
</center>
<br/>

Here is a good explanation how happen this use of stack by recursion.

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/dxyYP3BSdcQ" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

<p style="text-align:justify;">The second example (factorial) uses a different approach. It solves that by pre-processing values. With the results known, is possible to process them without overuse the stack.</p>

<center>
<img src="/img/dp/optimization_stack.png" width="349" height="218">
</center>
<br/>

<h2>Conclusion</h2>

<p style="text-align:justify;">Dynamic Programming is a great resource to improve performance in complex problems and recursion is good support. However, the recursion can give memory problem is not have a good implementation.</p>

<p style="text-align:justify;">Also, you can see other <a href="https://fabiana2611.github.io/foundation/sortalgorithm">algorithms</a> that use the DP: <a href="https://www.geeksforgeeks.org/quick-sort/">QuickSort</a> and <a href="https://www.geeksforgeeks.org/merge-sort/">MergeSort</a>.</p>

<h2>Reference</h2>

<ul>
 	<li class="entry-title"><a href="https://www.geeksforgeeks.org/solve-dynamic-programming-problem/">How to solve a Dynamic Programming Problem?</a></li>
 	<li><a href="https://www.tutorialspoint.com/data_structures_algorithms/dynamic_programming.htm">Data Structures - Dynamic Programming</a></li>
 	<li><a href="https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/">Program for Fibonacci numbers</a></li>
 	<li><a href="https://www.educative.io/courses/grokking-dynamic-programming-patterns-for-coding-interviews/m2G1pAq0OO0">Educative - What is Dynamic Programming?</a></li>
 	<li><a href="https://www.geeksforgeeks.org/dynamic-programming-vs-divide-and-conquer/">Dynamic Programming vs Divide-and-Conquer</a></li>
 	<li><a href="https://www.geeksforgeeks.org/dynamic-programming/">Dynamic Programming</a></li>
 	<li><a href="https://dev.to/nikolaotasevic/dynamic-programming--7-steps-to-solve-any-dp-interview-problem-3870">Dynamic Programming – 7 Steps to Solve any DP Interview Problem</a></li>
 	<li><a href="https://www.tutorialspoint.com/data_structures_algorithms/dynamic_programming.htm">Tutorials Point - DP</a></li>
 	<li><a href="https://www.cs.cmu.edu/~avrim/451f09/lectures/lect1001.pdf">Lecture 11 - DP</a></li>
 	<li>Typical Problems to solve with DP
    <ul>
     	<li>https://www.guj.com.br/t/algoritmo-da-mochila-programacao-dinamica/91069</li>
     	<li>https://blog.usejournal.com/top-50-dynamic-programming-practice-problems-4208fed71aa3</li>
    </ul>
</li>
</ul>
