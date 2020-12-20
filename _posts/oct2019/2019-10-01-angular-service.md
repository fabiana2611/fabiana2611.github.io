---
layout: post
title:  "Angular - Service"
date:   "2019-10-01"
category: "frontend"
permalink: /:categories/angular-service
---

<p style="text-align: justify;">The service is a good option when you need sharing data through the application or do some task such connect some other site, call a REST, etc.</p>
You can create a service using the <span style="color: #993366;">@angular/cli</span> by the command:
<pre class="result notranslate">ng g service myservice</pre>
<p style="text-align: justify;">Or by yourself creating a new file inside the folder you choose. On the top of the class you should to declare the <em><span style="color: #993366;">@Injectable</span></em>. It is the Dependence Injection (DI) responsible to instantiate the object.</p>

<div>
<pre>import { Injectable } from '@angular/core';
@Injectable()
export class MyService { ... }</pre>
</div>
<p style="text-align: justify;">If the service is specific to your component you just need to declare the service inside the '<a href="https://angular.io/guide/dependency-injection-providers#dependency-providers"><span style="color: #993366;">provider</span></a>' of your component to be available to Angular inject this service. Also the constructor should declare parameters which services will be used. Some github examples you can see here: <a href="https://github.com/fabiana2611/br-prev-analisys/blob/master/src/app/core/http/open-data-br.service.ts">[1]</a>, <a href="https://github.com/fabiana2611/br-prev-analisys/blob/master/src/app/modules/acidente-trabalho/acidente.service.ts">[2]</a>, <a href="https://github.com/fabiana2611/br-prev-analisys/blob/master/src/app/modules/beneficios/beneficio.service.ts">[3]</a> and <a href="https://github.com/fabiana2611/br-prev-analisys/blob/master/src/app/modules/contribuicao/contribuicao.service.ts">[4]</a></p>

<pre>
@Component({
     selector: 'my-app',
     templateUrl: './my-app.component.html',
     providers: [MyService]
})
export class MyComponent {
     constructor(private myservice:MyService){}
... }
</pre>
 
<p style="text-align: justify;">If it is a service that you need to use in many situations in your app and, for example, need to preserve the state of the data, you need to declare this service in a higher level. It is necessary because, when you navigate to other component and get back, the state will be restarted. Then, one example is to declare inside the <span style="color: #993366;">app.component.ts</span>.</p>

<div>
<pre>@Component({
   selector: 'app-root',
   templateUrl: './app.component.html',
   providers: [MyService]
})
export class AppComponent implements OnInit { ... }</pre>
</div>

<div id="dep_inj">
<h2>Dependency Injector</h2></div>

The Angular dependency injector is a <a href="https://angular.io/guide/hierarchical-dependency-injection">hierarchical injector</a>. Then you create a service to a component it will be available to all its child components. All of them will have the same instance of the service.
<ol>
	<li style="text-align: justify;">The <strong>highest</strong> <strong>level</strong> is the <span style="color: #993366;">AppModule</span>. Then, any instance declared in this level will be available to all the app.</li>
	<li style="text-align: justify;">The <strong>second level</strong>, one level below is the <span style="color: #993366;">AppComponent</span>. The instance created in this level will be available to all of its children, but not to the <span style="color: #993366;">AppModule</span> level. The instance is propagate only to the lowest level.</li>
	<li style="text-align: justify;">The last level, the <strong>lowest level</strong>, where there are no children, the instances create in this level will be available only to this component. And if in a higher level the same service is provided, the local instance will be override.</li>
</ol>
<p style="text-align: justify;">There are <a href="https://angular.io/guide/hierarchical-dependency-injection#two-injector-hierarchies">two types of the hierarchies</a> in Angular. When you use <span style="color: #993366;">@Injection</span> or <span style="color: #993366;">@NgModule</span> to the injection, it is called <span style="color: #993366;">ModuleInjector</span>. However, if you use @Directive or @Component to provide the injection it is called <span style="color: #993366;">ElementInjector</span>.</p>

<h2>References</h2>
<ul>
	<li><a href="https://www.tutorialspoint.com/angular7/angular7_services.htm">Tutorials Point</a></li>
	<li><a href="https://angular.io/guide/architecture-services">Angular IO - Service</a></li>
	<li><a href="https://angular.io/guide/dependency-injection">Angular IO - Dependency Injection</a></li>
	<li><a href="https://www.udemy.com/course/the-complete-guide-to-angular-2/">The complete guide to angular 2 (Udemy)</a></li>
</ul>
