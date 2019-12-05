---
layout: post
title:  "Angular - Observable"
date:   "2019-10-24"
category: "frontend"
permalink: /:categories/angular-observable
---

<p style="text-align: justify;"><a href="https://angular.io/guide/observables-in-angular#observables-in-angular">Observable</a> is an alternative to handle asynchronous tasks. It is the resource to manage the reaction of the system. It will listen <a href="https://angular.io/guide/observables-in-angular#router">router</a>/<a href="https://angular.io/guide/observables-in-angular#reactive-forms">forms</a> or handle <a href="https://angular.io/guide/observables-in-angular#http">http request/response</a> of the system and do some operation when a scenario happen. For example, if an event happen (click), you can watch this and react whit that.</p>
<p style="text-align: justify;">Examples of data sources candidates do be observable: (User Input) Event, Http requests, Triggered in code.</p>
<p style="text-align: justify;">In Angular, the <a href="https://angular.io/guide/rx-library#the-rxjs-library">RxJS</a> is the library that implement the Observable type.</p>

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
And an example using the methid "interval":
<pre>setInterval(() => {
    observer.next(count);
    if (count === 5) {
        observer.complete();
    }
    count++;
}, 1000);</pre>

<br/>
<h2>Next/Previsous Angular Post</h2>
<br/>
Services<a href="https://fabiana2611.github.io/angular/angular-service" class="btn btn-primary">
<img src="/img/angular/previous.png" width="50" height="50" ></a>

<h2>References</h2>
<ul>
	<li><a href="https://angular.io/guide/comparing-observables">Angular IO</a></li>
	<li><a href="https://www.udemy.com/course/the-complete-guide-to-angular-2/learn/lecture/6656450?start=0#overview">Udemy - Angular Complete</a></li>
</ul>
<code></code>
