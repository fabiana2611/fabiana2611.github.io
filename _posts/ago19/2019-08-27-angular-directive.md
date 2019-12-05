---
layout: post
title:  "Angular - Directives"
date:   2019-08-27
category: "frontend"
permalink: /:categories/angular-directives
---
<h2>Introduction</h2>

<p style="text-align: justify;"><a href= "https://www.tutorialspoint.com/angular7/angular7_directives.htm">Directives</a> are instructions in the DOM. It gives support to the connection between the component and the template. The types of directives are: component directives, <a href="https://angular.io/guide/structural-directives">structural directives</a> and <a href="https://angular.io/guide/attribute-directives">Attribute Directives</a>.</p>

<h2>Component Directives</h2>
<p style="text-align: justify;">These classes have instruction to handle the component, working with templates. An example is using the <span style="color: #993366;">@Directive</span>.</p>

When you create your own directive you should use the command:

<pre>ng g directive directive_name</pre>

<p style="text-align: justify;">It will create the file <span style="color: #993366;">directive_name.directive.spec.ts</span> and <span style="color: #993366;">directive_name.directive.ts</span>. It also will be declared in the <span style="color: #993366;">add.module.ts</span> file.</p>

{% highlight ruby %}
import { Directive } from '@angular/core';

@Directive({
  selector: '[directive_name]'
})
export class DirectiveNameDirective {
  constructor() { }
}
{% endhighlight %}


<h2>Structural Directives</h2>
<p style="text-align: justify;">Those are used to manipulate the DOM elements (add and remove), changing the structure of the view.</p>

An example is to use * ngIf inside a tag.

<pre>
<p * ngIf = "isOk>Component created</p>
</pre>

<p style="text-align: justify;">In this case, if the result is false, the component will not be rendered in the DOM.</p>

<p style="text-align: justify;">Also is commun the ngFor and ngSwitch.</p>

An explanation about the '\*' you can see <a href="https://angular.io/guide/structural-directives#the-asterisk--prefix">here</a>.

<h2>Attibute Directives</h2>

<p style="text-align: justify;">Those are used to manipulate the appearance and behavior of the DOM elements.</p>

An example id the ngStyle which can change the color of the component.


<br/>
<h2>Next/Previsous Angular Post</h2>
<br/>
Data Binding<a href="https://fabiana2611.github.io/angular/angular-databinding" class="btn btn-primary">
<img src="/img/angular/previous.png" width="50" height="50" ></a>

<a href="https://fabiana2611.github.io/angular/angular-pipes" class="btn btn-primary">
<img src="/img/angular/next.png" width="50" height="50" ></a>Pipes


<h2>References</h2>

<ul>
	<li>https://angular.io/tutorial/toh-pt3</li>
	<li>https://www.tutorialspoint.com/angular7/angular7_directives.htm</li>
</ul>
