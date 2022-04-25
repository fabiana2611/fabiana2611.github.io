---
layout: post
title:  "Angular - Pipes"
date:   "2019-09-04"
category: frontend node
permalink: /:categories/angular-pipes
---

<p style="text-align: justify;">The Pipe is a resource to transform a data to another format. The symbol of the pipe is the character '|', and to use this, you should put that inside the interpolation expression where the left side (integers, strings, arrays, and date) is your input and the right side is the function to transform the data. If necessary, you can use parameters as well.</p>

Some examples are:
<pre>
<b>{ { birthday | date } }</b>
<b>{ {todaydate | date:'d/M/y'} }</b>
<b>{ {todaydate | date:'d/M/y' | uppercase} }</b>  |  
<b>{ {6589.23 | currency:"EUR"} }</b>
<b>{ {months | slice:2:6} }</b>   
</pre>

Some examples of pipe function are:  DatePipe, UpperCasePipe, LowerCasePipe, CurrencyPipe, Decimalpipe, Jsonpipe, Slicepipe and PercentPipe.

<h2>Custom Pipes</h2>

To create a custom pipe you should to create a file the name of your pipe (app.name.ts), to use the '@Pipe' decorator and implement the method 'transform' from PipeTransform interface.

<pre>
import {Pipe, PipeTransform} from '@angular/core';
@Pipe ({
   name : 'name'
})
export class NamePipe implements PipeTransform {
  transform(value: number): number {
   return //TODO your logic;
 }
}
</pre>

And to use you need to add your pipe in the declarations array of the AppModule and use in the template.

<pre><b>{ {yourdata | name} }</b> </pre>

<h2>Pure and Impure Pipes</h2>

By default, every pipes are <a href="https://angular.io/guide/pipes#pure-pipes">pure</a>. It's mean that the function is called just once, even if the data is updated.

The <a href="https://angular.io/guide/pipes#impure-pipes">impure pipes</a> are the pipes that are called every component change detection cycle. To make the pipe impure add the attribute 'pure: false' inside the '@Pipe' metadata.

<h2>References</h2>

<ul>
  <li><a href="https://angular.io/guide/pipes">Angular Guide - Pipes</a></li>
  <li><a href="https://www.tutorialspoint.com/angular7/angular7_pipes.htm">TutorialsPoint - Pipes</a></li>
</ul>
