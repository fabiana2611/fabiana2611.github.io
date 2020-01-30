---
layout: post
title:  "Angular - Best Practices"
date:   2020-01-30
categories: frontend
permalink: /:categories/angular-best-practices
---

<p style="text-align: justify;">Hello guys!</p>
<p style="text-align: justify;">I'm new in Angular and one of the confusion to me is to understand the better way to program. I usually work in the back-end, and I'm not sure if the best practice in the back is also the best to the front.</p>
<p style="text-align: justify;">Because of that, I listed some usual points regarding the best practice using Angular which helped me to start this new development track. The detail about how to use each one of them you can access the links.</p>

<h2>List of Some Best Practices</h2>
<em><strong>Angular Guide</strong></em>
<ul>
	<li><span style="color: #993366;">Put the<strong> logic</strong> in the <em>ts</em> file. Use the HTML only for the <strong>presentation</strong>. [<a href="https://angular.io/guide/styleguide#put-presentation-logic-in-the-component-class">Ref</a>]</span></li>
	<li><span style="color: #993366;">Add <strong>complex logic</strong> in a <strong>service</strong> [<a href="https://angular.io/guide/styleguide#delegate-complex-component-logic-to-services">Ref</a>]</span></li>
	<li><span style="color: #993366;"><strong>Separate</strong> template and CSS in different files and reference them in '\*.ts' [<a href="https://angular.io/guide/styleguide#extract-templates-and-styles-to-their-own-files">Ref</a>]</span></li>
	<li><span style="color: #993366;"><strong>Small methods</strong> are more legible and easier for maintenance. Who much speak get in conflict by themselves. [<a href="https://angular.io/guide/styleguide#small-functions">Ref</a>]</span></li>
	<li><span style="color: #993366;"><strong>Reuse</strong> what is possible</span> [<a href="https://angular.io/guide/styleguide#t-dry-try-to-be-dry">Ref</a>]</li>
	<li><span style="color: #993366;">If the file names have more then one word, then it should be separated by <strong>dash</strong> (-)[<a href="https://angular.io/guide/styleguide#naming">Ref</a>]</span></li>
	<li><span style="color: #993366;">Create the <strong>structure based on the feature </strong>[<a href="https://angular.io/guide/styleguide#overall-structural-guidelines">Ref</a>]</span></li>
	<li><span style="color: #993366;">Use '<strong>Shared Module</strong>' if you have many components, directives or pipes used in many parts of the project. [<a href="https://angular.io/guide/styleguide#shared-feature-module">Ref</a>]</span></li>
	<li><span style="color: #993366;">Choice <strong>lazy</strong> load to make your application lighter</span> [<a href="https://angular.io/guide/styleguide#lazy-loaded-folders">Ref</a>]</li>
	<li><span style="color: #993366;">Use the<strong> Single Responsibility</strong> principle to everything in Angular [<a href="https://angular.io/guide/styleguide#single-responsibility">Ref</a>]</span></li>
	<li><span style="color: #993366;">Use <strong>@Input</strong> and <strong>@Output</strong> decorators <em><span style="text-decoration: underline;">instead of</span> </em><strong>@Directives</strong> and <strong>@Component</strong> <strong>properties </strong>[<a href="https://angular.io/guide/styleguide#decorate-input-and-output-properties">Ref</a>]</span></li>
	<li><span style="color: #993366;">Use <strong>@Injectable()</strong> decorator <span style="text-decoration: underline;"><em>instead of</em></span> the <strong>@Inject</strong> parameter decorator [<a href="https://angular.io/guide/styleguide#use-the-injectable-class-decorator">Ref</a>]</span></li>
	<li><span style="color: #993366;">Use <strong>directives</strong> to standardized a behaviour [<a href="https://angular.io/guide/styleguide#directives">Ref</a>]</span></li>
</ul>
<em><strong>Code Structure [<a href="https://www.freecodecamp.org/news/best-practices-for-a-clean-and-performant-angular-application-288e7b39eb6f/">1</a>] [<a href="https://code-maze.com/angular-best-practices/">2</a>] [<a href="https://itnext.io/choosing-a-highly-scalable-folder-structure-in-angular-d987de65ec7">3</a>] [<a href="https://www.zeolearn.com/magazine/angular-best-practices">4</a>] [<a href="https://aglowiditsolutions.com/blog/angular-best-practices/">5</a>]</strong></em>
<ul>
	<li><span style="color: #993366;">Use <strong>trackBy</strong> <span style="text-decoration: underline;"><em>instead</em> </span><strong>ngFor</strong></span>
- <span style="color: #993366;">Update the DOM only to the element related</span></li>
	<li><span style="color: #993366;">Use <strong>const</strong> <span style="text-decoration: underline;"><em>instead of</em></span>  <strong>let</strong> if the value will not change</span></li>
	<li><span style="color: #993366;">Use <strong>Pipeable operators</strong> when you are using <strong>RxJs</strong></span></li>
	<li><span style="color: #993366;">Use <strong>types</strong> to the declarations and <span style="text-decoration: underline;"><em>avoid</em> </span>the use of '<strong>any</strong>'. It makes the results more predictable.</span></li>
	<li><span style="color: #993366;">Choice <strong>chaining operators</strong> instead of a subscription inside other</span></li>
	<li><span style="color: #993366;">Create <strong>small components</strong> reusable, avoiding internal logic.</span></li>
	<li><span style="color: #993366;">If a <strong>string</strong> has a limited value, specify that.</span></li>
	<li><span style="color: #993366;">Use <strong>AngularCLI</strong> to be more productive</span></li>
	<li><span style="color: #993366;">The <strong>Class name</strong> should you <strong>camel-case style</strong></span></li>
	<li><span style="color: #993366;">Copy arrays or objects using the <strong>immutability</strong></span></li>
	<li><span style="color: #993366;">Use <strong>index.js</strong> </span></li>
	<li><span style="color: #993366;">Write a limit of <strong>400 lines</strong> by file</span></li>
	<li><span style="color: #993366;">A <strong>function</strong> must have a limit of <strong>75 lines</strong></span></li>
	<li><span style="color: #993366;">Use Interface</span></li>
	<li><span style="color: #993366;">Add one empty line between imports and module such as third party and application imports and third-party module and custom module</span></li>
</ul>

<h2>REFERENCES</h2>
<ul>
	<li>https://angular.io/guide/styleguide</li>
	<li>https://www.freecodecamp.org/news/best-practices-for-a-clean-and-performant-angular-application-288e7b39eb6f/</li>
	<li>https://code-maze.com/angular-best-practices/</li>
	<li>https://aglowiditsolutions.com/blog/angular-best-practices/</li>
	<li>https://itnext.io/choosing-a-highly-scalable-folder-structure-in-angular-d987de65ec7</li>
	<li>https://www.zeolearn.com/magazine/angular-best-practices</li>
</ul>
