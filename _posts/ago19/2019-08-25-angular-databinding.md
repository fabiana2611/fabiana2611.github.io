---
layout: post
title:  "Angular - Data Binding"
date:   2019-08-25
category: "angular"
permalink: /:categories/angular-databinding
---

<p style="text-align: justify;">Data binding is a way to put and push data from/to HTML. It is responsible for the communication between the typescript code (business logic) and the template (HTML). Then, data binding connects the templates and the components. It happens by interpolation, property and event binding.</p>

<center>
  <a href="https://angular.io/generated/images/guide/architecture/component-databinding.png">
    <img src="https://angular.io/generated/images/guide/architecture/component-databinding.png" width="400" height="300" />
  </a><br/>
  <em>From Angular.io</em>
</center><br/>

<h2>Interpolation</h2>

<p style="text-align: justify;">The expression to use the interpolation is the double curly ({ {data} }) used in the HTML file. Inside is added the property name declared in the <em>component.ts</em>.</p>

<center>
  <img src="/img/angular/interpolation.png" width="700" height="126" />
</center>
<br/>

<h2>Property Binding</h2>

<p style="text-align: justify;">Now, the expression use brackets ([prop]="data"). it is used to set properties of target elements. It is one-way in because is only possible to set a value in property target from component and not to send a value from target to component. Usually, you can do a similar operation using interpolation or property. <em><a href="https://angular.io/guide/template-syntax#property-binding-vs-interpolation" >However, when setting an element property to a non-string data value, you must use property binding</a></em>.</p>

<center>
  <img src="/img/angular/property.png" width="700" height="166" />
</center>
<br/>

<h2>Event Binding</h2>

<p style="text-align: justify;">It is to respond DOM events ((event)="expression"). The object can be used by the component. To use the event is necessary to pass this object using '$'. The method in component can declare the type with <a href="https://angular.io/guide/user-input#get-user-input-from-the-event-object">any</a>, which not specify the type. Or  with 'Event', for example, and you should <a href="https://angular.io/guide/user-input#type-the-event">do a cast to get the value</a>.</p>

<center>
  <img src="/img/angular/property.png" width="700" height="166" />
</center>
<br/>

<br/>
<h2>Next/Previsous Angular Post</h2>
<br/>
<a href="https://fabiana2611.github.io/angular/angular-component" class="btn btn-primary">
<img src="/img/angular/previous.png" width="50" height="50" >Component</a>

<h2>References</h2>
<ul>
<li>https://www.tutorialspoint.com/angular7/angular7_data_binding.htm</li>
<li>https://angular.io/guide/architecture-components</li>
<li>https://angular.io/guide/displaying-data#interpolation</li>
<li>https://angular.io/guide/template-syntax#property-binding</li>
<li>https://angular.io/guide/user-input#binding-to-user-input-events</li>
<li>https://www.tutorialspoint.com/angular7/angular7_event_binding.htm</li>
</ul>
