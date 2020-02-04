---
layout: post
title:  "Angular Router"
date:   2020-02-04
categories: frontend
permalink: /:categories/angular-router
---

<p style="text-align: justify;">Routing is the concept you will use when your app needs to navigate. The difference between using an Angular router and a common link is the performance.</p>
<p style="text-align: justify;"><span style="text-decoration: underline;">One option</span> to start to work with the router in your project is to add a constant in the AppModule class and declare that in the <em>imports</em> attribute.</p>

<div>
<pre>import { Routes, RouterModule } from '@angular/router';
...
const appRoutes: Routes = [
{ path: '', component: HomeComponent },
<span class="pun">{</span><span class="pln"> path</span><span class="pun">:</span> <span class="str">'**'</span><span class="pun">,</span><span class="pln"> component</span><span class="pun">:</span> <span class="typ">PageNotFoundComponent</span> <span class="pun">}</span>
{ path: 'home', component: HomeComponent },
{ path: 'contactus', component: ContactusComponent }

...
@NgModule({
    ...
   imports: [
      ...
      RouterModule.forRoot(appRoutes)
   ]
];
...

export class AppModule { }

</pre>
</div>
<em>The <span style="color: #993366;">'**' </span>is the wildcard, used to redirect any page that is not mapped.</em>
<p style="text-align: justify;"><em>Pay attention that the paths don't have the slash (/), representing the <strong>absolute path. </strong>More detail to use relative paths you can see <a href="https://angular.io/guide/router#relative-navigation">here</a>.</em></p>
<p style="text-align: justify;"><span style="text-decoration: underline;">Another option</span> to the route is, in the creating moment, where you say " to the question "<em>Would you like to add Angular routing?</em>". It will create the <span style="color: #993366;">app-routing.module.ts</span> file and add in <span style="color: #993366;">app.module.ts</span>. The constant <em><span style="color: #993366;">Routes </span></em>is where you will put all of the addresses used by your app to navigate.</p>
<p style="text-align: justify;"><img src="/img/angular/start-routing.png" alt="start-routing.png" width="744" height="512" /></p>
<p style="text-align: justify;">If you say "<em>no</em>", yet is possible to add the router manually in another moment of your development.</p>

<h2>A Simple Example</h2>
<p style="text-align: justify;">To test the use of routing let's <a href="https://fabiana2611.github.io/angular/angular-component">create components</a> to navigate. The first example (based on <a href="https://www.tutorialspoint.com/angular7/angular7_routing.htm">tutorialspoint</a>) I created the component <span style="color: #993366;"><em>home</em></span> and <em><span style="color: #993366;">contactus</span></em>. After that, I added the pair <span style="color: #993366;"><em>path</em></span> and <em><span style="color: #993366;">component</span></em> into <span style="color: #993366;"><em>Routes</em></span> constant, then export this const, and finally, add this into app.module.ts.</p>
<img src="/img/angular/routing-path.png" width="744" height="312" />
<p style="text-align: justify;">To test that, update the app.component.html and click on the links. You will see the result.</p>
<center>
<img src="/img/angular/test-html.png" width="364" height="181" />
</center>

<a href="https://angular.io/guide/router#router-outlet"><em>The <code>RouterOutlet</code> is a directive from the router library that is used like a component.</em></a>

The <a href="https://angular.io/guide/router#router-links">routerLink</a> is responsible for the navigation. Also, you can retrieve the <a href="https://angular.io/guide/router#router-state">router state</a> using the tree created at the end of the navigation lifecycle.

Also, you can add another attribute to indicate if the link is active or not. It's possible just use <em><span style="color: #993366;">class='active'</span></em> from bootstrap or use a <a href="https://angular.io/guide/router#active-router-links">second solution</a>:

{% highlight ruby %}
<a routerLinkActive= "active" routerLink="/home">Home</a>
<a routerLinkActive= "active" routerLink="/contactus">Contactus</a>
{% endhighlight %}

If you need to use <a href="https://angular.io/guide/router#route-parameters">parameter</a> to route, you can add the parameter in the router map or by link.
<pre>// router map
<span class="pun">{</span><span class="pln"> path</span><span class="pun">:</span> <span class="str">'contactu/:id'</span><span class="pun">,</span><span class="pln"> component</span><span class="pun">:</span> <span class="typ">ContactusComponent</span> <span class="pun">}</span>
// By link
<span class="tag"><</span><a class="code-anchor" href="https://angular.io/api/router/RouterLinkWithHref"><span class="tag">a</span></a><span class="pln"> [</span><a class="code-anchor" href="https://angular.io/api/router/RouterLink"><span class="atn">routerLink</span></a><span class="pln">]</span><span class="pun">=</span><span class="atv">"['contactus, contact.id]"</span><span class="tag">></span></pre>

<h2>Conclusion</h2>
The router is not a big deal to start to create. However, it is an important part of a project and should have a good plan to not be a mess.

A simple example you can see in my <a href="https://github.com/fabiana2611/br-prev-analisys">gitHub</a>.

<h2>References</h2>
<ul>
	<li><a href="https://www.tutorialspoint.com/angular7/angular7_routing.htm">Tutorial Point - Routing</a></li>
	<li><a href="https://angular.io/start/routing">Angular.io - Start routing</a></li>
</ul>
