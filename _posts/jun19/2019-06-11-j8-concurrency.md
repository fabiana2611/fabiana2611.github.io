---
layout: post
title:  "Java 8 - Part V [Concurrency]"
date:   2019-06-11
categories: java
permalink: /:categories/concurrency
---

<p style="text-align: justify;">One important update that Java 8 brings to us is the introduction of parallel streams. Other important to mention is the Arrays class that now supports parallel operations. But Is it the same thing as concurrency?</p>


<center>
  <img src="/img/j8/councurrencyParallelism2.png" alt="councurrencyParallelism2.png" width="456" height="302" />
  <br/>
  <em>Concurrency vs Parallelism</em>
</center>  

<p style="text-align: justify;">So, it's time to start the fifth post of the Java 8 series about the changes that you can find from version 6 to 8.</p>

<h2>Summary</h2>
<center>
  <iframe width="560" height="315" src="https://www.youtube.com/embed/p3pchT5ETV4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>
<br/>

<h2>What is it?</h2>
<p style="text-align: justify;">The concurrency is when more than one processes run simultaneously and use the same resource. That race condition needs to be monitored and controlled to avoid two or more threads have access to the same state information. It assures that one thread does not modify the state while the other is performing an atomic state-dependent operation.</p>

<h2>Thread problems</h2>

<blockquote>
<p style="text-align: justify;">Liveness is the ability of an application to be able to execute in a timely manner. Liveness problems, then, are those in which the application becomes unresponsive.</p>
</blockquote>

<ul>
	<li style="text-align: justify;">Deadlock: <em>two or more threads are blocked forever, each waiting on the other.</em></li>
	<li style="text-align: justify;">Starvation: <em>a single thread is perpetually denied access to a shared resource or lock.</em></li>
	<li style="text-align: justify;">Livelock: <em>two or more threads are conceptually blocked forever, although they are each still active and trying to complete their task. It's a special case of resource starvation.</em></li>
	<li>Race Condition: <em>two or more threads try to complete a related task at the same time.</em></li>
</ul>

<center>
  <a href="https://www.slideshare.net/mariofusco/if-you-think-you-can-stay-away-from-functional-programming-you-are-wrong" ><img src="/img/j8/problemasConcorrencia.png" width="430" height="249" /></a>
  <br/>
  <em>Effects of Concurrency</em>
</center>
<br/>

<h2>How to coordinate the access?</h2>
<p style="text-align: justify;">When concurrent activities interact, some sort of coordination is required. The <em><span style="color: #993366;">Synchronization</span></em> (<em>synchronized</em> keyword) is a solution to ensure that only one thread at a time can access the code and guarantee the consistency. When a thread uses a code this thread locks the code and any other thread can use that one. Every other thread is blocked. The first thread need release the code to that be available to be accessed by other threads.</p>

{% highlight ruby %}
# Lock an object
synchronized(object) { /*....*/ }

# Lock a method
private synchronized void methodA() {
    System.out.print((++count)+" ");
}

# static code
public static synchronized void methodB() {
    System.out.print("Finished work");
}
{% endhighlight %}

<h2><strong>Lock, ReadWriteLock and ReentrantLock</strong></h2>
<p style="text-align: justify;">To use <em><span style="color: #993366;">synchronized</span></em> keyword is a limited solution. It's not possible, for example, to check if a locked object is available. Concurrent API added the <span style="color: #993366;">Lock</span> framework to help on that. This framework offer method to acquire and release the lock explicitly. It is used to avoid deadlock.</p>

{% highlight ruby %}
Lock lock = new ReentrantLock();
try {
    lock.lock();
    System.out.print((++count)+" ");
} finally {
    lock.unlock();
}

PS: All other threads will wait until this thread call the unlock.
PS: You should unlock the thread that have the lock.
If you don't do that you will get a runtime exception (IllegalMonitorStateException)
{% endhighlight %}

<p style="text-align: justify;">The <em><span style="color: #993366;">tryLock</span></em> method is an alternative to the lock because it returns a boolean result indicating whether was obtained, which avoid thread to wait indefinitely.</p>

{% highlight ruby %}
Lock lock = new ReentrantLock();
if(lock.tryLock()) {
    try {
       System.out.print((++count)+" ");
    } finally { lock.unlock(); }
} else {
    System.out.println("Unable to acquire lock!");
}

# Alternativaly
lock.tryLock(10, TimeUnit.SECONDS)
// Return TRUE if the lock is acquired within this 10 seconds.
{% endhighlight %}

<p style="text-align: justify;">The <em><span style="color: #993366;">lock</span></em> guarantees mutually exclusivity of an object. But sometimes only the write processes need to lock the object, making the read available to other threads. To make this possible you can use the <em><span style="color: #993366;">ReadWriteLock</span></em> interface with the <span style="color: #993366;"><em>realLock</em></span> and <span style="color: #993366;"><em>writeLock</em></span> methods. This class doesn't implement the <em><span style="color: #993366;">Lock</span></em> interface, but these two methods return Lock objects. In fact, <em><span style="color: #993366;">ReentrantReadWriteLock</span></em> class implements the <span style="color: #993366;"><em>ReadWriteLock</em></span> interface.</p>

{% highlight ruby %}
private ReadWriteLock readWriteLock = new ReentrantReadWriteLock();
Lock lockRead = readWriteLock.readLock();
Lock writeLock = readWriteLock.writeLock();
{% endhighlight %}

<h2>Atomic Package</h2>
<p style="text-align: justify;">Atomic operations are performed in a single step (package java.concurrent.atomic). This package helps to coordinate access to primitive value and the reference object. Furthermore, it offers classes such as <span style="color: #993366;"><a href="https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/atomic/AtomicInteger.html" >AtomicInteger</a></span> and <span style="color: #993366;"><a href="https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/atomic/AtomicLong.html" >AtomicLong</a></span> that support atomic operation on single variables. Some common atomic methods are <span style="color: #993366;"><em>get, set, getAndSet, incrementAndGet, getAndIncrement, decrementAndGet, getAndDecrement</em></span>.</p>

{% highlight ruby %}
# Example
private AtomicInteger count = new AtomicInteger(0);
private void incrementAndReport() {
    System.out.print(count.incrementAndGet()+" ");
}
{% endhighlight %}

<p style="text-align: justify;">The new methods are [<a href="https://www.amazon.com.br/Java-Action-Lambdas-Functional-Style-Programming/dp/1617291994?tag=kns00-20&ascsubtag=go_952006559_46722489029_301325114634_aud-519888259198:dsa-413046190713_c_29040837259">JavaInAction</a>]:</p>

<ul>
	<li style="text-align: justify;"><strong><em>getAndUpdate - </em></strong>Atomically updates the current value with the results of applying the given function, returning the previous value.</li>
	<li style="text-align: justify;"><em><strong> updateAndGet - </strong></em>Atomically updates the current value with the results of applying the given function, returning the updated value.</li>
	<li style="text-align: justify;"><strong><em>getAndAccumulate</em></strong> - Atomically updates the current value with the results of applying the given function to the current and given values, returning the previous value.</li>
	<li style="text-align: justify;"><em><strong>accumulateAndGet - </strong></em>Atomically updates the current value with the results of applying the given function to the current and given values, returning the updated value.</li>
</ul>

{% highlight ruby %}
// atomically set the minimum between an observed value of 10 and an
// existing atomic integer
int min = atomicInteger.accumulateAndGet(10, Integer::min);
{% endhighlight %}

<p style="text-align: justify;">[<a href="https://www.amazon.com.br/Java-Action-Lambdas-Functional-Style-Programming/dp/1617291994?tag=kns00-20&ascsubtag=go_952006559_46722489029_301325114634_aud-519888259198:dsa-413046190713_c_29040837259">JavaInAction</a>]: "<em>The Java API recommends using the new classes LongAdder, LongAccumulator, Double-Adder, and DoubleAccumulator instead of the Atomic classes equivalent when multiple threads update frequently but read less frequently. These classes are designed to grow dynamically to reduce thread contention".</em></p>

<h2>Concurrent Collections</h2>
<p style="text-align: justify;">If you are working in concurrent environments you can use directly the collections from the package java.util.concurrent that are already prepared for this. Beside the concurrent collections often include performance enhancements that avoid unnecessary synchronization.</p>
<p style="text-align: justify;">Examples of concurrent interfaces available when you use Concurrency API are <span style="color: #993366;">BlockingQueue, BlockingDeque, ConcurrentMap </span>and<span style="color: #993366;"> NavigableMap</span>.</p>

{% highlight ruby %}
# Using synchronized keyword
Map<String,Object> map = new HashMap<String,Object>();
public synchronized void put(String key, String value) {
    map.put(key, value);
}

// Alternative solution
Map<String,Object> map=new ConcurrentHashMap<String,Object>();
public void put(String key, String value) {
    map.put(key, value);
}

# More examples
Queue queue = new ConcurrentLinkedQueue<>();
queue.offer(31);
Deque deque = new ConcurrentLinkedDeque<>();
deque.offer(10);
deque.push(4);
BlockingQueue q = new LinkedBlockingQueue<>();
q.offer(3, 4, TimeUnit.SECONDS);
q.poll(10, TimeUnit.MILLISECONDS);

BlockingDeque d = new LinkedBlockingDeque<>();
d.offerFirst(5, 2, TimeUnit.MINUTES);
d.offerLast(47, 100, TimeUnit.MICROSECONDS);
d.pollFirst(200, TimeUnit.NANOSECONDS);
d.pollLast(1, TimeUnit.SECONDS);
{% endhighlight %}

<strong>CopyOnWrite Collections</strong>
<p style="text-align: justify;"><span style="color: #993366;">CopyOnWriteArrayList </span>and <span style="color: #993366;">CopyOnWriteArraySet</span> copy all of their elements to a new structure when an element is added, modified (change reference), or removed from the collection. <span style="color: #993366;">CopyOnWriteArrayList</span> is most useful when you have few updates and inserts and many concurrent reads because the <span style="color: #993366;">CopyOnWrite</span> classes can use a lot of memory.</p>
<strong>Concurrent Collections by methods</strong>
<p style="text-align: justify;">It's possible to obtain synchronized versions of existing non-concurrent collection objects by methods from Collections class. Examples: <span style="color: #993366;">synchronizedCollection, synchronizedList, synchronizedMap</span>.</p>

{% highlight ruby %}
List list = Collections.synchronizedList(
        new ArrayList<>(Arrays.asList(1,6,16)));

synchronized(list) {
    for(int data: list){
        System.out.print(data+" ");
    }
}
{% endhighlight %}

<strong>CyclicBarrier and ForkPool</strong>
<p style="text-align: justify;">The <span style="color: #993366;">CyclicBarrier</span> and <span style="color: #993366;">ForkPool</span> are classes included in Concurrency API to help to coordinate concurrent tasks.</p>
<p style="text-align: justify;">The <span style="color: #993366;">CyclicBarrier's</span> constructor you say a number of threads to wait for. When each thread finish the <span style="color: #993366;">await</span> method is called. When the number of calls is equal to the number informed in the constructor the threads can continue.</p>

{% highlight ruby %}
public void methodA(CyclicBarrier c1, CyclicBarrier c2) {
    // ...
    action1();
    c1.await();
    action2();
    c2.await();
    action3();
    // ...
}
// ...
ExecutorService service = Executors.newFixedThreadPool(4);
ClassA manager = new ClassA();
CyclicBarrier c1 = new CyclicBarrier(4);
CyclicBarrier c2 = new CyclicBarrier(4,
     () -> System.out.println("Continue!"));

for(int i=0; i<4; i++)     service.submit(() -> manager.methodA(c1,c2));
// ...

# Organized Result
1. Action 1 of all threads will be executed.
2. After that, action 2 of all threads,
3. after that will be printed "Continue"
4. and then action 3 of all threads.
{% endhighlight %}

<p style="text-align: justify;">If the current thread is interrupted, the <span style="color: #993366;">await</span> method throws an <span style="color: #993366;">InterruptedException</span>. If another thread is interrupted or time out a <span style="color: #993366;">BrokenBarrierException</span> is thrown.</p>
<strong>The Fork/Join Framework</strong>
<p style="text-align: justify;">The <span style="color: #993366;">ExecutorService</span> was the solution to run asynchronous tasks, but it works best when the tasks are homogeneous and independent. The Fork/Join Framework is a new alternative that complements the concurrency API using the <em>divide and conquer</em> approach. It uses the <em>work-stealing algorithm</em>.</p>
<p style="text-align: justify;">This framework is used to run large tasks split into small tasks and execute, using recursion,  in <strong>parallel</strong> to get results faster. The recursive process has to arrive at a base case. The small results are combined to get the final result. The split phase is the FORK and the combining phase is the JOIN.</p>

<ol>
	<li style="text-align: justify;">Create a ForkJoinTask: define the recursive process. The fork/join solution extending <span style="color: #993366;">RecursiveAction</span> class (implement the void <span style="color: #993366;"><em>compute</em></span> method) or <span style="color: #993366;">RecursiveTask</span> class (implement <em><span style="color: #993366;">compute</span></em> method with a generic return type) which implement <span style="color: #993366;">ForkJoinTask</span> interface</li>
	<li style="text-align: justify;">Create the ForkJoinPool: <em><span style="color: #993366;">new ForkJoinPool(). </span></em>It creates an instance with a number of threads equal to the number of processors of your machine. You can define the number of threads using ForkJoinPool(<span class="hljs-keyword">int</span> parallelism) constructor. It uses the <em>work-stealing</em> algorithm (when a thread is free, it steals the pending work of other threads that are still busy)</li>
	<li style="text-align: justify;">Start the ForkJoinTask:<em><span style="color: #993366;"> pool.invoke(task)</span></em></li>
</ol>

{% highlight ruby %}
# RecursiveAction
protected class A extends RecursiveAction{
    //...
    @Override
    protected void compute(){
        if(....) { .... }
        else {
            // ...
            invokeAll(new A(...), new A(...));
        }
    }
}
// ...
ForkJoinTask<?> task = new A(...);
ForkJoinPool pool = new ForkJoinPool();
pool.invoke(task);

# RecursiveTask
protected class B extends RecursiveTask {
    //...
    @Override
    protected Double compute(){
        if(....) {return X;}
        else {
             // ...
             RecursiveTask o = new B(...);
             o.fork();
             return new B(...).compute() + o.join();
        }
   }
}
// ...
ForkJoinTask task = new B(...);
ForkJoinPool pool = new ForkJoinPool();
Double sum = pool.invoke(task);
{% endhighlight %}

<ul>
	<li style="text-align: justify;">This framework is useful for any task that can be solved recursively and can be computed independently (so the order doesn't matter)</li>
	<li>The <em><span style="color: #993366;">fork</span></em> method  just add a task to the thread's queue</li>
	<li style="text-align: justify;">The <em><span style="color: #993366;">fork</span></em> method should be called before the <span style="color: #993366;">join</span> method.</li>
	<li style="text-align: justify;">The <span style="color: #993366;"><em>join</em> </span>method should be the last step. It'll block the program until the result is returned.</li>
	<li style="text-align: justify;">The <em><span style="color: #993366;">compute</span></em> method should be called before <span style="color: #993366;">join</span> method.</li>
</ul>
A complete code example you can see <a href="https://github.com/java8/Java8InAction/blob/master/src/main/java/lambdasinaction/chap7/ForkJoinSumCalculator.java" >here</a>.

<h2>Thread Basics</h2>
Threads are what make concurrency possible in java. In Java, it happens when multiple threads execute and process at the same time

<blockquote>
<h5 style="text-align: justify;"><em>Threads are units of code that can be executed at the same time. They are sometimes called lightweight processes, although, in fact, a thread is executed within a process (and every process has, at least, one thread, the main thread).</em></h5>
</blockquote>

<p style="text-align: justify;">Generically, it's possible to say that thread uses directly a stack and, since objects are in heap, indirectly the threads use heap because a thread can have a reference of an object in the heap.</p>

<ol>
	<li>
<p style="text-align: justify;"><em><strong>Heap -</strong> Since the global variable is stored in the heap, the heap is shared among threads. All threads share a common heap. [<a href="https://stackoverflow.com/questions/1665419/do-threads-have-a-distinct-heap">1</a>] [<a href="https://cs.stackexchange.com/questions/48345/what-threads-share-in-general">2</a>]</em></p>
</li>
	<li>
<p style="text-align: justify;"><em><strong>Stack -</strong> Since each thread can have its own execution sequence/code, it must have its own stack on which it might push/pop its program counter contents. So threads of the same process do not share a stack. Each <a href="http://en.wikipedia.org/wiki/Stack-based_memory_allocation" rel="noreferrer">thread has a private stack</a>, which it can quickly add and remove items from. [<a href="https://stackoverflow.com/questions/1665419/do-threads-have-a-distinct-heap">1</a>] [<a href="https://cs.stackexchange.com/questions/48345/what-threads-share-in-general">2</a>]</em></p>
</li>
</ol>
<strong>Create Thread</strong>
<p style="text-align: justify;">The two-step process to execute a task using a thread is (1) defining the thread with the task and (2) start the execution. The first step can be done using the <em><span style="color: #993366;">Runnable</span> </em>interface or subclass<span style="color: #993366;"><em> Thread</em></span>. The second one is discouraged, so I will just show the first one example. And the second step is executed using the <span style="color: #993366;"><em>start</em></span> method.</p>

{% highlight ruby %}
# Definition of Runnable Interface
@FunctionalInterface
public interface Runnable {
    void run();
}

# Traditional way
public class A implements Runnable {
    public void run() {        
       System.out.println("Running");    
    }
}
Thread thread = new Thread(new A());
thread.start();

# Using lambda
Thread thread = new Thread(() -> {
    System.out.println("Running");
});
thread.start();

PS: it might not start immediately
PS: Example from OCP8 - Threads
{% endhighlight %}

<b>Executor</b>

This interface introduces the replaces of the use of the Thread by Executor.

{% highlight ruby %}
Runnable r = ...
//Thread t = new Thread(r);
//t.start();
Executor e = ...
e.execute(r);
{% endhighlight %}

<b>ExecutorService</b>

<p style="text-align: justify;">This interface comes in Concurrency API to help to create and manage the threads: get an instance and send to be processed. That instance you can get using the <span style="color: #993366;">Executors</span> factory introduced by Concurrency API.</p>

{% highlight ruby %}
ExecutorService service = null;
try {
   service = Executors.newSingleThreadExecutor();
   System.out.println("begining");
   service.execute(() -> System.out.println("A")); // Task 1
   service.execute(() -> System.out.println("B")); // Task 2
   System.out.println("end");
} finally {
   if(service != null) service.shutdown();
}

# Possible output
begining
A
end
B

PS: The threads will order their result
PS: The single thread executor will queue the tasks
PS: Each task execute after the previous task completes
PS: Task 2 always will execute after Task 1
PS: The shutdown() will not stop tasks that are running
PS: To really stop all threads you have to use shutdownNow()

# void execute(Runnable command)
{% endhighlight %}

<p style="text-align: justify;">The <span style="color: #993366;">ExecutorService</span> interface extends <span style="color: #993366;">Executor</span> interface. The <span style="color: #993366;"><em>execute</em></span> method comes from that interface. A similar method is the <span style="color: #993366;"><em>submit</em></span>() that also complete tasks asynchronously, but unlike execute, return a <span style="color: #993366;">Future</span> object. The Future can show the state of the task with the <em><span style="color: #993366;">isDone</span></em>, <em><span style="color: #993366;">isCancelled</span></em>, <em><span style="color: #993366;">cancel</span></em> and <em><span style="color: #993366;">get</span></em> methods.</p>
<p style="text-align: justify;">The <span style="color: #993366;">ExecutorService</span> also have more two methods. The <span style="color: #993366;">invokeAll</span> and <span style="color: #993366;">invokeAny</span> methods take a collection object containing a list of tasks and execute the tasks synchronously. The first one doesn't stop until all tasks are completed. The second one will wait until at least one task complete. It's possible to inform a timeout to the execution.</p>

{% highlight ruby %}
//...
service = Executors.newSingleThreadExecutor();
Future<?> result = service.submit(() -> {
         for(int i=0; i<500; i++) CheckResults.counter++; });
result.get(10, TimeUnit.SECONDS);
//...

PS: After 10 seconds, throwing a TimeoutException if the task is not done.
{% endhighlight %}

<p style="text-align: justify;">This interface extends <span style="color: #993366;">Executor</span> to provide more features, like the <span style="color: #993366;"><em>submit</em></span> method that accepts <span style="color: #993366;">Runnable</span> and <span style="color: #993366;">Callable</span> objects and allows them to return a value.</p>

<strong>Callable</strong>
<p style="text-align: justify;">It is another important interface (a functional interface) that can be an alternative to the <span style="color: #993366;">Runnable</span> interface retrieving more detail after the task is complete. It returns a value and throws a checked exception.</p>

{% highlight ruby %}
// ...
service = Executors.newSingleThreadExecutor();
Future result = service.submit(() -> 30+11);
System.out.println(result.get());
// ...

PS: The submit is a overload method from ExecutorService to take Callable Object
{% endhighlight %}

If it is necessary, it is possible to schedule the execution.

{% highlight ruby %}
ScheduledExecutorService service = Executors
       .newSingleThreadScheduledExecutor();
Runnable task1 = () -> System.out.println("A");
Callable task2 = () -> "B";
Future<?> result1 = service.schedule(task1, 3, TimeUnit.SECONDS);
Future<?> result2 = service.schedule(task2, 5, TimeUnit.MINUTES);
{% endhighlight %}

<strong><span class="s3">Thread pools</span></strong>
<p style="text-align: justify;"><span style="color: #993366;"><a href="https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Executors.html" >Executors</a></span> provide factory and utility methods for Executor, ExecutorService, ScheduledExecutorService, ThreadFactory and Callable classes to act on a pool of threads. The thread pool cannot be created directly by the interfaces. The tasks in the pool can be executed concurrently.</p>

<blockquote>
<p style="text-align: justify;">A thread pool is a group of pre-instantiated reusable threads that are available to perform a set of arbitrary tasks.</p>
</blockquote>

{% highlight ruby %}
ScheduledExecutorService service = Executors
       .newScheduledThreadPool(10);
service.scheduleAtFixedRate(command,3,1,TimeUnit.MINUTE);
{% endhighlight %}

<ul>
	<li>newCachedThreadPool</li>
	<li>newFixedThreadPool</li>
	<li>newScheduledThreadPool</li>
</ul>

<h4>Tip</h4>
<p style="text-align: justify;">If you need to generate a random number in a thread-safe manner without performance degradation you should use ThreadLocalRandom class. Using <em>java.util.Random</em> and <em>java.lang.Math.danrom</em> is also thread-safe, but they can have poor performance.</p>

<h2>Conclusion</h2>
<p style="text-align: justify;">Concurrency API helps a lot the work to control the shared resource. That API brings good things to help us in sequential and parallel execution. You need to pay attention to the right scenarios to use this resource and use the best of the benefits.</p>

<p style="text-align: justify;">More examples of concurrency you can see in my <a href="https://github.com/fabiana2611/JavaVersionUpdate/tree/master/JavaVersionUpdate/src/br/bia/upgrade/objective/concurrency">GittHub</a>.</p>

<h2>Related Posts</h2>
<ul>
	<li><a href="https://fabiana2611.github.io/java/stream" >Java 8 – Part IV [Streams]</a></li>
  <li><a href="https://fabiana2611.github.io/java/lambda">Java 8 – Parte III [Lambda]</a></li>
  <li><a href="https://fabiana2611.github.io/java/datetime" >Java 8 - Part II [Localization, Date, Time]</a></li>
    <li><a href="https://fabiana2611.github.io/java/enhancements" >Java 8 - Language Enhancements</a></li>
</ul>
<h2>Reference</h2>
<ul>
	<li><a href="http://ocpj8.javastudyguide.com/ch27.html">OCP8 - Concurrency</a></li>
	<li><a href="http://ocpj8.javastudyguide.com/ch26.html">OCP8 - Threads</a></li>
	<li><a href="http://pdf.th7.cn/down/files/1603/Oracle%20Certified%20Professional%20Java%20SE%208%20Programmer%20Exam%201Z0-809.pdf" >OCP Oracle Cetified Professional Java SE 8  Programmer II – Study Guide</a></li>
	<li><a href="https://github.com/java8/Java8InAction" >Java In Action – Github</a></li>
	<li><a href="https://stackoverflow.com/questions/1665419/do-threads-have-a-distinct-heap">[1] Stackoverflow</a></li>
	<li><a href="https://cs.stackexchange.com/questions/48345/what-threads-share-in-general">[2] Stackoverflow</a></li>
</ul>
 
