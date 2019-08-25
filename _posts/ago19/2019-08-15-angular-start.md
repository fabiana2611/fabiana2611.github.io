---
layout: post
title:  "Angular - Start"
date:   2019-08-15
category: "angular"
permalink: /:categories/angular-start
---
<h2>Introduction</h2>
<blockquote><em>Angular is an open-source JavaScript framework for building web applications and apps in JavaScript, HTML, and Typescript which is a superset of JavaScript. [<a href="https://www.tutorialspoint.com/angular7/index.htm">1</a>]</em></blockquote>
<p style="text-align: justify;">The first version was AngularJS. The second version was completely different, which makes these version not compatible. That first version had many problems what makes Angular lose the interest of the developer. Then, the responsible is promising to deliver a new version every 6 months. Angular is owned by Google.</p>
<p style="text-align: justify;">The Angular uses <a href="https://www.typescriptlang.org/">TypeScript</a>. You will code in TypeScript but it will be mapped to JavaScript, what the browser really know.</p>
The three parts of the Angular are:
<ul>
	<li><a href="https://angular.io/api/core" >Angular Core</a>: central part of the angular</li>
	<li><a href="https://cli.angular.io/">Angular CLI: </a>Start new projects</li>
	<li><a href="https://www.tutorialspoint.com/angular_material7/index.htm">Angular Materials</a>: UI Component Library</li>
</ul>
<h2 class="p1">Start</h2>
To start to work with <a href="https://angular.io/guide/setup-local" >Angular</a> you need to have:
<ul class="list">
	<li>Nodejs
<ul>
	<li>Download and install node.js (<a href="https://nodejs.org/en/"><span class="s1">https://nodejs.org/en/</span></a>)</li>
</ul>
</li>
	<li>Npm
<ul>
	<li>It will be installed with nodejs.</li>
</ul>
</li>
	<li>Angular CLI</li>
	<li>IDE for writing your code
<ul>
	<li>Visual Studio Code (you can use other options)</li>
</ul>
</li>
</ul>
<p style="text-align: justify;">The line commands you can need is below. If the <span style="color: #993366;">CLI</span> is old you should uninstall that, clean the cache and install another one.</p>

<pre class="p1"><span class="s2">[sudo] npm install -g npm</span>
<span class="s2">sudo npm uninstall -g angular-cli @angular/cli</span>
<span class="s2">npm cache clean --force</span>
<span class="s2">[sudo] npm install -g @angular/cli</span></pre>
After that, you are ready to create your first project.
<pre>ng new my-project</pre>
Now, go inside the project you created and start the server.
<pre>cd my-project
<span class="s3">ng serve</span>

<span class="s3"><span class="s4">Test: <a href="http://localhost:4200/">http://localhost:4200/</a>.</span></span></pre>

Here is the basic structure that the angular will create for you.

<center>
<img src="/img/angular/basic_structure.png" width="154" height="436" />
</center>
<br/>
<p style="text-align: justify;">Most of the files are related to configurations and we don't have to be worried about that. The file angular.json, for example, has the dependencies and the <span style="color: #993366;">node_modules</span> has the real dependencies.</p>
<p style="text-align: justify;">The <span style="color: #993366;">src</span> folder has the main source code that we will work. The <span style="color: #993366;">app</span> folder has the file that we will work to show in the browser. For every updates, you just need salve your file and the server will be updated and you can see the result in the browser.</p>
<p style="text-align: justify;">For a test, go to the <span style="color: #993366;">app.component.html</span> and change the title. This file also has a variable <span style="color: #993366;">{{ title }}</span> defined in the <span style="color: #993366;">app.component.ts</span>. Change this as well and see the result. The <span style="color: #993366;">app.component.ts</span> is the typescript file that defines the component.</p>
<p style="text-align: justify;">The same <span style="color: #993366;">app.component.ts </span>file has a "<span style="color: #993366;">selector</span>" that define  "<span style="color: #993366;">app-root</span>". You will see that in the <span style="color: #993366;">index.html</span> page. That is all the magic.</p>

<p style="text-align: justify;">For more detail about what does mean each file in the project can see that in <a href="https://angular.io/guide/file-structure">here</a>.</p>

<h2>A simple modification - Module</h2>
<p style="text-align: justify;">A simple test that you can do just is adding a new <a href="https://www.tutorialspoint.com/angular7/angular7_modules.htm">module</a>. The module is a set of functional blocks related to an application domain. The module created by default is the @NgModule. Angular is defined by a set of NgModules, which is a set of functional blocks related to an application domain. It declares a compilation text for a set of components. The <a href="https://angular.io/guide/architecture-modules">NgModule</a> is identified by @NgModule() decorator.</p>

<p style="text-align: justify;">One example is to add a dynamic input text. To do this, delete all the content of the <span style="color: #993366;">app.component.html</span> and put this:</p>

{% highlight ruby %}
< input type = "text" [(ngModel)]= "title" >
< p > { { title } } < /p >
{% endhighlight %}

Now, go to the app.module.ts and import the new module <span style="color: var(--color-text);">and add the module in the imports array.</span>

<img class="  wp-image-1004 aligncenter" src="https://bianoporto.files.wordpress.com/2019/08/ng_module.png" alt="ng_module.png" width="396" height="299" />

Save all files and the result is, what you write in the field it will be shown below.

Other examples you can find <a href="https://angular.io/start/routing">here</a>.
<h2>Adding bootstrap</h2>
<p class="p1">To use bootstrap you need to install that. If you want a specific version you just need to add that on the end of the command.</p>

<pre class="p1">npm install --save bootstrap@3</pre>
<p class="p2"><span class="s1">Refresh your project and the folder will be shown inside the node_modules folder. Now, update the file <span style="color: #993366;">Angular.json</span> adding in <strong>styles</strong> tag "</span><strong><span class="s2">node_modules/bootstrap/dist/css/bootstrap.min.css".</span></strong></p>
<img class="  wp-image-1001 aligncenter" src="https://bianoporto.files.wordpress.com/2019/08/stylesbootstrap-1.png" alt="stylesBootstrap.png" width="390" height="283" />

<br/>
<h2>Next/Previsous Angular Post</h2>
<br/>
<a href="https://fabiana2611.github.io/angular/angular-component" class="btn btn-primary">
<img src="/img/angular/next.png" width="50" height="50" >Component</a>

<h2>References</h2>
<ul>
	<li class="p1"><span class="s1"><a href="https://github.com/angular/angular-cli/wiki">https://github.com/angular/angular-cli/wiki</a></span></li>
	<li class="p1"><span class="s1"><a href="https://www.tutorialspoint.com/angular7/angular7_quick_guide.htm">https://www.tutorialspoint.com/angular7/angular7_quick_guide.htm</a></span></li>
	<li>https://www.udemy.com/the-complete-guide-to-angular-2/</li>
</ul>
