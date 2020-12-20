---
layout: post
title:  "Angular - Observable"
date:   "2019-10-24"
category: "frontend"
permalink: /:categories/angular-observable
---

<p style="text-align: justify;"><a href="https://angular.io/guide/observables-in-angular#observables-in-angular">Observable</a> is an alternative to handle asynchronous tasks. It is the resource to manage the reaction of the system. It will listen <a href="https://angular.io/guide/observables-in-angular#router">router</a>/<a href="https://angular.io/guide/observables-in-angular#reactive-forms">forms</a> or handle <a href="https://angular.io/guide/observables-in-angular#http">http request/response</a> of the system and do some operation when a scenario happen. For example, if an event happen (click), you can watch this and react whit that.</p>

<p style="text-align: justify;">The consumer uses the observable result when it is notified by the use of the subscribe method. When the observable is part of the framework, the angular handle the observable. However, if the observable is created by the developer, then that should be handled and destroyed.</p>

<p style="text-align: justify;">Examples of data sources candidates do be observable: (User Input) Event, Http requests, Triggered in code.</p>

<p style="text-align: justify;">In Angular, the <a href="https://angular.io/guide/rx-library#the-rxjs-library">RxJS</a> is the library used to work with asynchronous data streams. It implement the Observable type.</p>

<blockquote>
<p style="text-align: justify;">RxJS (Reactive Extensions for JavaScript) is a library for reactive programming using observables that makes it easier to compose asynchronous or callback-based code.</p>
</blockquote>
<p style="text-align: justify;">This library offer <a href="https://angular.io/guide/rx-library#observable-creation-functions">functions</a> to create new Observables. Also, some operators are prepared to react and return a observation like map, filter.</p>
The <a href="https://angular.io/guide/rx-library#naming-conventions-for-observables">naming conventions</a> for observables is use the "$".

Below is shown an example of the imports:
<pre>import { interval, Subscription, Observable } from 'rxjs';
import { map, filter } from 'rxjs/operators';</pre>
Now an example the the observable on router using <em>params</em>:

<pre>this.route.params.subscribe((params: Params) => {
    this.id = +params.id;
});</pre>

And an example using the method "interval":

<pre>setInterval(() => {
    observer.next(count);
    if (count === 5) {
        observer.complete();
    }
    count++;
}, 1000);</pre>

If it is asynchronous you should to use the error that cames from the observable.

<pre>
observable.subscribe({
  ( ...) ,
  error(x) { console.log(x)}
});
</pre>

To synchronous behaviour you can use the Promise.

<pre>
promise.then(....).catch(...);
</pre>

<h3><em>Observables vs promises <a href="https://angular.io/guide/comparing-observables#observables-compared-to-promises">[Ref]</a></em></h3>
<ul>
  <li>Observables: start with subscription call. Promises: execute with the creation.</li>
  <li>Observables: many values. Promises: one value</li>
  <li>Observables: more then one clauses. Promises: only one (then)</li>
  <li>Observables: the subscribe method handling errors. Promises: the child is responsible for the errors.</li>
</ul>

<br/>
<h2>Next/Previsous Angular Post</h2>
<br/>
Services<a href="https://fabiana2611.github.io/angular/angular-service" class="btn btn-primary">
<img src="/img/angular/previous.png" width="50" height="50" ></a>

<h2>References</h2>
<ul>
  <li><a href="https://angular.io/guide/observables">Angular IO - Observables</a></li>
	<li><a href="https://angular.io/guide/comparing-observables">Angular IO  - Observables vs Primise</a></li>
	<li><a href="https://www.udemy.com/course/the-complete-guide-to-angular-2/learn/lecture/6656450?start=0#overview">Udemy - Angular Complete</a></li>
  <li><a href="https://blog.angular-university.io/rxjs-error-handling/">RxJs Error Handling: Complete Practical Guide</a></li>
<li><a href="https://xgrommx.github.io/rx-book/content/getting_started_with_rxjs/creating_and_querying_observable_sequences/error_handling.html">RxJs: Error Handling in the Reactive Extensions</a></li>
<li><a href="https://alligator.io/rxjs/simple-error-handling/l">Simple Error Handling in RxJS</a></li>
<li><a href="https://www.intertech.com/Blog/angular-best-practice-rxjs-error-handling/">Angular Best Practice: RxJS Error Handling</a></li>
<li><a href="https://www.learnrxjs.io/">Learn RxJS</a></li>

</ul>
