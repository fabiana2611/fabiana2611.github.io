---
layout: post
title:  "Angular - Observable"
date:   "2019-10-24"
categories: node frontend 
permalink: /:categories/angular-observable
---

<p style="text-align: justify;">There are two different protocols to define the relationship between Producer and Consumer. These protocols are <a href="http://reactivex.io/rxjs/manual/overview.html#pull-versus-push">PULL and PUSH</a>. </p>

<ul>
  <li><b>What is Pull?</b> <em>In Pull systems, the Consumer determines when it receives data from the data Producer. The Producer itself is unaware of when the data will be delivered to the Consumer.</em></li>
  <li><b>What is Push?</b><em> In Push systems, the Producer determines when to send data to the Consumer. The Consumer is unaware of when it will receive that data.</em></li>
</ul>

<p>Some ways to manipulate the stream of data using those protocols are:</p>

<ul>
  <li><b>Ajax:</b> works as a pull and not applicable to push data.</li>
  <li><b>Promise:</b> is as a Push and can retrieve results once. <em>A Promise (the Producer) delivers a resolved value to registered callbacks (the Consumers). It was very used for AngularJS to asynchronous events.</em></li>
  <li><b>Observable:</b> <em>is a Producer of multiple values, pushing them to Observers (Consumers). </em>  </li>
</ul>

<h1>Observables vs Promises</h1>

<p style="text-align: justify;">The use of these resources makes attend the use of reactive programming pattern. However, the Observable over-place the use of Promise. Here is some <a href="https://angular.io/guide/comparing-observables#observables-compared-to-promises">differences</a> between both solutions.</p>

<table>
  <tr>
    <th>Observable</th>
    <th>Promise</th>
  </tr>
  <tr>
    <td>start with subscription call</td>
    <td>execute with the creation</td>
  </tr>
  <tr>
    <td>many values</td>
    <td>one value</td>
  </tr>
  <tr>
    <td>more then one clauses</td>
    <td>only one (then)</td>
  </tr>
  <tr>
    <td>the subscribe method handling errors</td>
    <td>the child is responsible for the errors</td>
  </tr>
</table>

<h1>The different types of observables</h1>

<p style="text-align: justify;"><em>An Observable is a stream of asynchronous events that can be processed with array-like operators.<a href="https://medium.com/ngx-rocket/the-missing-introduction-to-angular-and-modern-design-patterns-43e8815c2801">[1]</a></em>. Therefore, <a href="https://angular.io/guide/observables-in-angular#observables-in-angular">Observable</a> is an way to handle asynchronous tasks. It is the resource to manage the reaction of the system. The new version of Angular use the observable and his specialization. </p>

<ul>
  <li><b><a href="http://reactivex.io/rxjs/manual/overview.html#observable">Observable</a></b>
    <ul>
      <li>Cold: the code is executed even only one observer.</li>  
      <li>Uni-directional: Observer can not assign value to observable.</li>
      <li>The code will run for each observer.</li>      
      <li>Unicast: emit values from the observable not from any other component.</li>
      <li>It creates copy of data for each observer.</li>    
      <li>Passive: Observables are passive subscribers to the events</li>
      <li>Each subscribers get different instance of the event, then the result on each Observer can be different.</li>
      <li>Lifecycle: creation, subscription, execution and destruction</li>
    </ul>
  </li>
  <li><b><a href="http://reactivex.io/rxjs/manual/overview.html#subject">Subject</a></b>
    <ul>
      <li>Subject extends Observable</li>
      <li>Hot: the code is executed and value gets broadcast even if there is no observer.</li>
      <li>bi-directional: Observer can assign value to observable.</li>
      <li>Same data is shared between all observers.</li>
      <li>Active: Subjects can trigger new events using next or complete methods</li>      
      <li>All subscribers get the same event</li>
      <li>It allows values to be multicasted to many Observers. </li>
      <li> It can act as both subscribers and emmitter</li>
    </ul>
  </li>
  <li><b><a href="http://reactivex.io/rxjs/manual/overview.html#behaviorsubject">BehaviorSubject</a></b>
    <ul>
      <li>BehaviorSubject extends Subject</li>
      <li><em>It stores the latest value emitted to its consumers, and whenever a new Observer subscribes, it will immediately receive the "current value"</em></li>
    </ul>
  </li>
  <li><b><a href="http://reactivex.io/rxjs/manual/overview.html#replaysubject">ReplaySubject</a></b>
    <ul>
      <li>ReplaySubject extends Subject</li>
      <li>The subject will miss all the values that are broadcast before creation of observer. <em>A ReplaySubject records multiple values from the Observable execution and replays them to new subscribers.</em></li>
    </ul>
  </li>
</ul>

<h1>Using it</h1>

<p style="text-align: justify;">The observables are used, for instance, to listen <a href="https://angular.io/guide/observables-in-angular#router">router</a>/<a href="https://angular.io/guide/observables-in-angular#reactive-forms">forms</a> or handle <a href="https://angular.io/guide/observables-in-angular#http">http request/response</a> of the system and do some operation when a scenario happen. When the observable is part of the framework, the angular handle the observable. However, if the observable is created by the developer then it should be handled and destroyed.</p>

<p style="text-align: justify;">Examples of data sources candidates do be observable: (User Input) Event, Http requests, Triggered in code.</p>

<p style="text-align: justify;">In Angular, the <a href="https://angular.io/guide/rx-library#the-rxjs-library">RxJS</a> is the library used to work with asynchronous data streams. It implement the Observable type.</p>

<blockquote>
<p style="text-align: justify;">RxJS (Reactive Extensions for JavaScript) is a library for reactive programming using observables that makes it easier to compose asynchronous or callback-based code.</p>
</blockquote>

<p style="text-align: justify;">This library offer <a href="https://angular.io/guide/rx-library#observable-creation-functions">functions</a> to create new Observables. Also, some operators are prepared to react and return a observation like map, filter. <a href="https://rxmarbles.com/">Here</a> a dynamic way to compare the operators.</p>

<p>The <a href="https://angular.io/guide/rx-library#naming-conventions-for-observables">naming conventions</a> for observables is use the "$".</p>

Below is shown an example of the imports:

{% highlight ruby %}
import { interval, Subscription, Observable } from 'rxjs';
import { map, filter } from 'rxjs/operators';
{% endhighlight %}

Now an example the the observable on router using <em>params</em>:

{% highlight ruby %}
this.route.params.subscribe((params: Params) => {
    this.id = +params.id;
});
{% endhighlight %}

And an example using the method "interval":

{% highlight ruby %}
setInterval(() => {
    observer.next(count);
    if (count === 5) {
        observer.complete();
    }
    count++;
}, 1000);
{% endhighlight %}

Here is an example using Subject.

{% highlight ruby %}
private mySubject$: Subject<MyObjectRest> = new BehaviorSubject(null);

ngInit() {
  this.load().pipe(
      switchMap(myObject=> {
        return myObject;
      })
    );
}

load(): Observable<MyObjectRest> {
   return this.getMyObject().pipe(
      tap(
        (value: MyObjectRest) => this.mySubject$.next(value))
      );
}

getMyObject(): Observable<MyObjectRest> {
    return this.http.get<MyObjectRest>("https://myapp/endpoint");
}
{% endhighlight %}



<h2>References</h2>
<ul>
  <li><a href="https://angular.io/guide/observables">Angular IO - Observables</a></li>
	<li><a href="https://www.udemy.com/course/the-complete-guide-to-angular-2/learn/lecture/6656450?start=0#overview">Udemy - Angular Complete</a></li>
  <li><a href="https://blog.angular-university.io/rxjs-error-handling/">RxJs Error Handling: Complete Practical Guide</a></li>
  <li><a href="https://xgrommx.github.io/rx-book/content/getting_started_with_rxjs/creating_and_querying_observable_sequences/error_handling.html">RxJs: Error Handling in the Reactive Extensions</a></li>
  <li><a href="https://alligator.io/rxjs/simple-error-handling/l">Simple Error Handling in RxJS</a></li>
  <li><a href="https://www.intertech.com/Blog/angular-best-practice-rxjs-error-handling/">Angular Best Practice: RxJS Error Handling</a></li>
  <li><a href="https://www.learnrxjs.io/">Learn RxJS</a></li>
  <li><a href="https://coryrylan.com/blog/rxjs-observables-versus-subjects">RxJS Observables versus Subjects</a></li>
  <li><a href="https://stackoverflow.com/questions/47537934/what-is-the-difference-between-observable-and-a-subject-in-rxjs">Stackoverflow: What is the difference between Observable and a Subject in rxjs?</a></li>
  <li><a href="https://medium.com/duomly-blockchain-online-courses/understand-how-rxjs-observables-and-subjects-work-and-whats-the-difference-between-them-13d9b047dd94">Understand how RxJS Observables and Subjects work and what’s the difference between them</a></li>
  <li><a href="https://medium.com/ngx-rocket/the-missing-introduction-to-angular-and-modern-design-patterns-43e8815c2801">The Missing Introduction to Angular and Modern Design Patterns</a></li>
  <li><a href="https://dev-academy.com/angular-architecture-best-practices/">Angular Architecture Patterns and Best Practices</a></li>
</ul>
