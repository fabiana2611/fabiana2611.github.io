---
layout: post
title:  "Angular Form: Reactive vs Template"
date:   2020-01-23
categories: frontend
permalink: /:categories/angular-reactive-template
---

<p style="text-align: justify;">Hello World!!!</p>
<p style="text-align: justify;">In this post, I'd like to introduce you two approaches to building an <a href="https://angular.io/guide/forms-overview">Angular Form</a>: The <strong>Reactive-driven</strong> form and <strong>Template-driven</strong> form provided by the Angular framework.</p>

<h2>Introduction</h2>
<p style="text-align: justify;">Both use a <a href="https://angular.io/guide/forms-overview#common-foundation">common idea</a> to control the HTML form elements. This happens with <span style="color: #993366;">FormControl</span>, <span style="color: #993366;">FormGroup</span> and <span style="color: #993366;">FormArray </span>[<a href="https://www.tektutorialshub.com/angular/angular-forms-fundamentals/">1</a>]. However, the <strong>Template</strong> does this more implicitly while <strong>Reactive</strong> is more explicit. Moreover, the <strong>first</strong> one uses directives (<span style="color: #993366;">ngModel, ngModelGroup, ngForm</span>) and the <strong>second</strong> one uses classes such as <em><span style="color: #993366;">FormControl, FormGroup and FormBuilder</span></em>. The <strong>Reactive</strong> form allows more control over the data model, tests and validations.</p>

<ol>
	<li style="text-align: justify;"><span style="color: #993366;">FormControl</span>: It's responsible to encapsulate the information regarding an input element (e.g changed value or set a new value). It's created for each form field. The list of the methods you can use to manipulate the elements you can see <a href="https://angular.io/api/forms/AbstractControl">here</a>.</li>
	<li style="text-align: justify;"><span style="color: #993366;">FormGroup</span>: It's a collection of <span style="color: #993366;">FormControls</span>. This is identified by the pair key/value. You can have F<span style="color: #993366;">ormGroup</span> inside the <span style="color: #993366;">FormGroup</span> (nested)</li>
	<li style="text-align: justify;"><span style="color: #993366;">FormArray</span>: is an array of <span style="color: #993366;">FormControls</span>. It doesn't use the pair key/value.</li>
</ol>
<p style="text-align: justify;">To use this control, the first thing first is to import the <span style="color: #993366;">FormsModule</span> if you use <strong>Template</strong> and <span style="color: #993366;">ReactiveFormsModule</span> if you use Reactive form. After that, you should add in the <span style="color: #993366;">imports</span> metadata.</p>

{% highlight ruby %}
import {FormsModule, ReactiveFormsModule} from "@angular/forms";
...
imports: [
  ...
  FormsModule,
  ReactiveFormsModule,
  ...
  ],
  ...
{% endhighlight %}

<h2>Template-Diven Forms</h2>
<p style="text-align: justify;">In this approach, many steps are behind the scenes. <span style="color: var(--color-text);">A top-level </span><span style="color: #993366;">FormGroup</span><span style="color: var(--color-text);"> instance is created implicitly by the form directive. If you need to manipulate the <span style="color: #800080;"><em>ngForm </em></span></span>instance<span style="color: var(--color-text);">, you can export that into a local variable. In the example below, the '<span style="color: #800080;">#myForm'</span> has a reference to the <em style="color: var(--color-text);"><span style="color: #800080;">ngForm</span></em> and can be used in any part of the form.</span></p>

{% highlight ruby %}
<form #myForm="ngForm" (ngSubmit)="onSubmit(myForm)">
  <p>
    <label for="completeName">Complete Name</label>
    <input type="text" id="completeName" name="completeName" ngModel>
  </p>
  <p>
    <label for="email">Email </label>
    <input type="text" id="email" name="email" ngModel>
  </p>
  <p> <button type="submit">Submit</button> </p>
</form>
{% endhighlight %}

<p style="text-align: justify;">Besides this, a <span style="color: #993366;">FormControl</span> instance is created implicitly in each element that uses <em><span style="color: #993366;">ngModel</span> </em>directive. It makes possible to control these elements.</p>
<p style="text-align: justify;">That control of the elements can be done by the simple use of the <em><span style="color: #800080;">ngModel </span></em>directive, such in the example before, or you can use the<em><span style="color: #993366;"> two-way data binding</span></em>. Everything used in this way should be declared in your class to maintain data consistency. Then, it keeps the component model in sync with the <span style="color: #993366;">FormModel</span>. The example below uses the '<em>completename' </em>attribute in the class to be updated.</p>

{% highlight ruby %}
<p>
  <label for="completeName">Complete Name </label>
  <input type="text" id="completename" name="completename"
  [(ngModel)]="completename">
</p>
{% endhighlight %}

<p style="text-align: justify;">To manipulate this form in your component class you can create a reference using <em><span style="color: #993366;">ViewChild</span></em> or by method parameter such used by <em><span style="color: #993366;">onSubmit</span> </em>method:</p>

{% highlight ruby %}
import {NgForm} from "@angular/forms";
...
@ViewChild('myForm',null) myForm: NgForm;
...
setEmail() {
  this.myForm.controls.email.setValue("my@email.com");
};
public onSubmit(myForm: ngForm){
  myForm.controls.email.setValue("newmy@email.com");
}
{% endhighlight %}

If some  form element needs to be validate, you need only add the validator in the template. The template-driven use directives to this.

{% highlight ruby %}
<input id="email" name="email" type="email" #email="ngModel"                 
     [(ngModel)]="email" class="form-control" required email/>
<label for="email">
  <p [class]="email.valid ? 'green-class' : 'danger-class'">{{email}}</p>
</label>
{% endhighlight %}

In case you have to add some conditional you can do this by directives:

{% highlight ruby %}
<input id="email" name="email" type="email" #email="ngModel"
  [(ngModel)]="email" class="form-control"
  [required]="isConditionRequiredOK()"
  [email]="isConditionEmailOK()"/>
{% endhighlight %}

<h2>Reactive Forms</h2>
<p style="text-align: justify;">Here, the developer is responsible to build the model. The <span style="color: #993366;">FormGroup</span> needs to be create explicitly.</p>
<p style="text-align: justify;">You need to import <span style="color: #993366;">FormGroup</span> and <span style="color: #993366;">FormControl</span>. If you use <span style="color: #993366;">Validators</span> then you should import <span style="color: #993366;">Validators</span> as well. The validators can be synchronous or asynchronous. Also, you can <a href="https://angular.io/api/forms/Validator#provide-a-custom-validator">custom a validator</a>.</p>

{% highlight ruby %}
# Component Class
import { FormGroup, FormControl, Validators } from '@angular/forms'
...
myForm = new FormGroup({
  completename: new FormControl(),
  email: new FormControl('', [Validators.required, Validators.email])
  })
{% endhighlight %}

<p style="text-align: justify;">In the page example, the <span style="color: #993366;"><em>formGroup</em> </span>directive is used to bind the form. The <em><span style="color: #993366;">formControlName</span> </em>is the key in the <span style="color: #993366;">FormControl</span>. It bind the input field to a individual form control. The name used to the <em><span style="color: #993366;">formControlName</span> </em> value should be the same name declared in the class.</p>

{% highlight ruby %}
# HTML Template
<form [formGroup]="myForm" (ngSubmit)="onSubmit()">
  <p>
    <label for="completeName">Complete Name</label>
    <input type="text" id="completeName" name="completeName"
       formControlName="completename">
  </p>
  <p>
    <label for="email">Email </label>
    <input type="text" id="email" name="email" formControlName="email">
  </p> <p> <button type="submit">Submit</button> </p> </form>
{% endhighlight %}

To access the control by the class you can do:

{% highlight ruby %}
# Simple way
myForm.get("email").valid
# Nested
myForm.get("superGroup.subGroup").valid
{% endhighlight %}

<h2>Dif: Reactive vs Template</h2>
<center>
  <img src="/img/angular/difreactiveTemplateform.png" width="953" height="409" />
  <a href="https://angular.io/guide/forms-overview#key-differences">Key Differences</a>
</center>
<br/>
<p style="text-align: justify;">Using Template-driven forms you will have less code then using Reactive forms. Then, it can be easier and practical. By other hand, if you need more control to manipulate the controls, the Reactive will be easier. Also, Reactive Forms are more prepared to work with <a href="https://angular.io/guide/forms-overview#testing">unit tests</a>.</p>

<h2>REFERENCES</h2>
<ul>
	<li><a href="https://angular.io/guide/forms-overview">Angular Guide - Forms Overview</a></li>
	<li><a href="https://angular.io/guide/forms#template-driven-forms">Angular Guide - Template-Driven Forms</a></li>
	<li><a href="https://www.javacodegeeks.com/2019/03/angular-6-reactive-form-example.html">jacacodegeeks - Angular6 reactive form example</a></li>
	<li><a href="https://www.tektutorialshub.com/angular/angular-reactive-forms/">tektutorialshub</a><a href="https://www.tektutorialshub.com/angular/formcontrol-in-angular/"> - Form Control in Angular</a></li>
	<li><a href="https://www.tektutorialshub.com/angular/angular-template-driven-forms/">tektutorialshub - Angular Template-driven forms</a></li>
	<li><a href="https://www.tektutorialshub.com/angular/angular-reactive-forms-validation/">tektutorialshub - angular-reactive-forms-validation</a></li>
	<li><a href="https://www.tektutorialshub.com/angular/angular-reactive-forms/">tektutorialshub - angular-reactive-forms</a></li>
	<li><a href="https://www.tektutorialshub.com/angular/angular-forms-fundamentals/">tektutorialshub - Angular Forms Tutorial: Fundamentals & Concepts</a></li>
	<li><a href="https://angularfirebase.com/lessons/basics-reactive-forms-in-angular/">angularfirebase -  Angular Reactive Forms Basics Guide</a></li>
	<li><a href="https://jasonwatmore.com/post/2018/05/11/angular-6-template-driven-forms-validation-example">jasonwatmore - Example template-driven Angular6</a></li>
	<li><a href="https://jasonwatmore.com/post/2018/11/10/angular-7-template-driven-forms-validation-example">jasonwatmore - Example template-driven Angular7</a></li>
	<li><a href="https://jasonwatmore.com/post/2018/05/10/angular-6-reactive-forms-validation-example">jasonwatmore - Angular6 - Reactive Forms Validation Example</a></li>
</ul>
