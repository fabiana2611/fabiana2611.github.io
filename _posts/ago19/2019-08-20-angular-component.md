---
layout: post
title:  "Angular - Component"
date:   2019-08-20
category: "frontend"
permalink: /:categories/angular-component
---
<h2>Introduction</h2>

<p style="text-align: justify;">The <a href= "https://fabiana2611.github.io/angular/angular-start">first post</a> about Angular was related to how to create the first project. Now we will give another step, component. </p>

When the project is created, a default component (or root) is present. It is used in the <span style="color: #993366;">index.html</span> to start all the process and to be rendered by Angular.

<h4>How the magic happens?!</h4>

<p style="text-align: justify;">The <span style="color: #993366;">app.component.ts</span> file will have the selector which declare the tag that you will use. The <span style="color: #993366;">index.htm</span> has the reference to the <span style="color: #993366;">app-root</span> tag. Then, Angular will put what is defined to this tag, that is in the <span style="color: #993366;">app.component.html</span>. The main.ts declare the root node (or root component) to start the application.</p>

<center>
<img src="/img/angular/how.png" width="796" height="499"/>
</center>
<br/>

A new component will have the same structure, and to use that you need to put its tag where you wish how many times you guess it's necessary.

<h2>Creating a new Component</h2>

<p style="text-align: justify;">The components are the key feature in Angular that represents the functional parts of the application that interact with Html. It represents the view. Every component has a class with data and behaviours. The class is identified by <span style="color: #993366;">@Component</span> decorator.</p>

<p style="text-align: justify;">To create a component is very simple. The commands are:</p>

{% highlight ruby %}
// Complete command
ng generate component new-cmp
// Simplified command
ng g c new-cmp
// A component inside another one
ng g c component_path/new-cmp
{% endhighlight %}

<p style="text-align: justify;">When you do this, a new component is created with a folder, their files and references in <span style="color: #993366;">app.module.ts</span>. Considering the new components <span style="color: #993366;">servers</span>, the new structure is shown below.</p>

<center>
<img src="/img/angular/new_component.png" width="596" height="499"/>
</center>
<br/>

<p style="text-align: justify;">Every component has:</p>

<ul>
	<li style="text-align: justify;"><strong>new-cmp.component.css</strong>: it's to appearance</li>
	<li style="text-align: justify;"><strong>new-cmp.component.html</strong>: it's displayed on the browser for the component template. Templates are HTML + directives + binding markup. Template directives provide program logic. Binding markup (event, property) connects your application data and the DOM.</li>
	<li style="text-align: justify;"><strong>new-cmp.component.spec.ts</strong>: it's related to unit test</li>
	<li style="text-align: justify;"><strong>new-cmp.component.ts</strong>: it defines the module, properties, etc. The class implements OnInit. The method ngOnInit created is called when the class is executed.</li>
</ul>

<h2>Component Metadata</h2>

<p style="text-align: justify;">The CLI generated three metadata properties inside of <strong>new-cmp.component.ts</strong>:</p>

<ul>
	<li style="text-align: justify;"><strong>selector:</strong> the component's CSS element selector. It's possible declare the tag that will be used or such a tag's attribute.</li>
  <li style="text-align: justify;"><strong>templateUrl:</strong> the location of the component's template file. It's possble use just 'template' and add code inline.</li>
  <li style="text-align: justify;"><strong>styleUrls:</strong> the location of the component's private CSS styles.</li>
</ul>

Every metadata can be declared inline commands.

<h2>Lifecycle</h2>
<p style="text-align: justify;">Every component has a <a href="https://angular.io/guide/lifecycle-hooks#lifecycle-hooks">lifecycle</a> controlled by Angular that creates, render the component and its children, checks for updates, and destroy the component to remove from DOM.</p>

<center>
<img src="/img/angular/lifecycle.png" width="596" height="129"/>
</center>
<br/>

In terms of “calls”, the lifecycle can be executed through the list of methods:

<center>
<img src="/img/angular/lifecycle_call.png" width="156" height="200"/>
</center>
<br/>

<p style="text-align: justify;">It's possible to work inside the phases to do several treatments using interfaces. One example is the OnInit interface. Then, use their methods to implement some behaviour that is necessary for the specific phase. To see the sequence os methods see <a href="https://angular.io/guide/lifecycle-hooks#lifecycle-sequence">here</a>.</p>

<br/>
<h2>Next/Previsous Angular Post</h2>
<br/>
Start<a href="https://fabiana2611.github.io/angular/angular-start" class="btn btn-primary">
<img src="/img/angular/previous.png" width="50" height="50" ></a> <a href="https://fabiana2611.github.io/angular/angular-databinding" class="btn btn-primary">
<img src="/img/angular/next.png" width="50" height="50" ></a>Data Binding


<h2>References</h2>

<ul>
	<li>https://angular.io/tutorial/toh-pt3</li>
	<li>https://www.tutorialspoint.com/angular7/angular7_components.htm</li>
</ul>
