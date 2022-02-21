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

{% highlight ruby %}
//  1 1 2 3 5 8 13 21 34 56 90
public class Fibonacci {

  private static int number;
  private Integer cache[];

  public static void main(String[] args) {

    number = 9;

    Fibonacci fact = new Fibonacci();
    System.out.println(fact.fibonacciRecursive(number));
    System.out.println(fact.fibonacciIterative(number));
  }

  public int fibonacciRecursive(int number) {
    if (number <= 1) {
	    return number;
    }
    return fibonacciRecursive(number - 1) + fibonacciRecursive(number - 2);
  }

  public long fibonacciIterative(int number) {

    int f[] = new int [number + 2];
    f[0] = 0;
    f[1] = 1;

    for (int i = 2; i <= number; i++) {
      f[i] = f[i -1] + f[i-2];
    }

    return f[number];
  }

  public int cacheFibo(int number) {

    Integer cache[] = getCache();

    if (cache[number] == null) {
      cache [number] = cacheFibo(number-1) + cacheFibo(number-2);
    }

    return cache[number];
  }

  private Integer[] getCache() {
    if(cache == null) {
      cache = new Integer [number];
    }
    return cache;
  }

}
{% endhighlight %}

<p style="text-align:justify;">The first method (fibonacciRecursive) solves the problem using the memorization idea, with recursive calls and star the state in N (TopDown). The second method (fibonacciIterative) uses the tabulation idea with the initial state started by '1' (BottomUp). The first strategy is easier to think and implement, however, it uses recursivity, which makes the second one, the iterative way, faster than the first method.</p>

<p style="text-align:justify;">The solution can be improved using cache. The last method (cacheFibo) show that.

<h2>Recursion: Pay Attention to the stack</h2>

<p style="text-align:justify;">You have to pay attention how you are using the recursion. When the values are bing passed to be calculate on the end of the process you will have a stack with many values. It can throw errors because of a full stack. </p>

<p style="text-align:justify;">The example bellow (fibonacci) show how the stack is going to be used to process all the result in the end, going back each step when have values the be processed.</p>

{% highlight ruby %}
//5! = 5*4*3*2*1
public class Factorial {

  public static void main(String[] args) {
    Factorial fact = new Factorial();
    System.out.println(fact.factorialRecursive(5));
    System.out.println(fact.factorialRecursive(5,1));
    System.out.println(fact.factorialIterative(5));
  }

  public long factorialRecursive(int number) {
    if (number == 2) {
      return 2;
    }
    System.out.println(number + " * factorialRecursive(" + (number - 1) + ")" );
    long result  =  number * factorialRecursive(number - 1);
    System.out.println("Partial Result: " +  number + " * factorialRecursive(" + (number - 1) + ")" );
    return result;
  }

  public long factorialRecursive(int number, int a) {
    if (number <= 1) {
      return a;
    }
    return factorialRecursive( number - 1, number * a);
	}

  public long factorialIterative(int number) {

    if (number == 0 || number == 1) {
      return 1;
    }

    int result = 1;

    for (int i = 2; i <= number; i++) {
      result *= i;
    }

    return result;
  }
}
{% endhighlight %}

<p style="text-align:justify;">The outcome from the first recursive code is printed bellow where you will see the stack being completed with data to calculate everything in the end, removing data from the stack.</p>

<pre>
// Storage data on stack
5 * factorialRecursive(4)
4 * factorialRecursive(3)
3 * factorialRecursive(2)

// Go down in the stack calculating values
3 * factorialRecursive(2)
4 * factorialRecursive(3)
5 * factorialRecursive(4)

// Result
120
</pre>

<p style="text-align:justify;">The second recursive code is a memory improvement where the values is already calculate. It makes not necessary storage the data.</p>

<p style="text-align:justify;">Here is a good explanation how happen this use of stack by recursion.</p>

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/dxyYP3BSdcQ" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

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
