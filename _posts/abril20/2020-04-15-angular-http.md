---
layout: post
title:  "Angular - HTTP Request"
date:   2020-04-15
category: "frontend"
permalink: /:categories/angular-http
---

<h2>Introduction</h2>
<p style="text-align: justify;">An application communicates with the backend by an Http Request. This request goes to the server which access database, files or other resources necessaries on the server-side.</p>

<center>
<img class="  wp-image-1161 aligncenter" src="/img/angular/angularhttp.png" alt="angularhttp" width="352" height="232" />
<br>
</center>

<p style="text-align: justify;">The application using Angular does the HTTP request through the <a href="https://angular.io/guide/http">HttpClient</a> which uses XMLHttpRequest. The HttpClient is inside the <em>common/http</em> package.</p>

<p style="text-align: justify;">To use this API you should import <span style="color: var(--color-text);">HttpClientModule in AppModule. To use, you need to inject that.</span></p>
<div>
<pre>// 1. Declaration
import { HttpClient } from '@angular/common/http';

<span class="lit">@</span><a class="code-anchor" href="https://angular.io/api/core/NgModule"><span class="lit">NgModule</span></a><span class="pun">({</span><span class="pln">
  imports</span><span class="pun">:</span> <span class="pun">[</span>
    ...
    <a class="code-anchor" href="https://angular.io/api/common/http/HttpClientModule"><span class="typ">HttpClientModule</span></a><span class="pun">,
</span>    ...


// 2. Using
<span class="kwd">import</span> <span class="pun">{</span> <a class="code-anchor" href="https://angular.io/api/common/http/HttpClient"><span class="typ">HttpClient</span></a> <span class="pun">}</span> <span class="kwd">from</span> <span class="str">'@angular/common/</span><a class="code-anchor" href="https://angular.io/api/common/http"><span class="str">http</span></a><span class="str">'</span><span class="pun">;</span>

<span class="lit">@</span><a class="code-anchor" href="https://angular.io/api/core/Injectable"><span class="lit">Injectable</span></a><span class="pun">()</span>
<span class="kwd">export</span> <span class="kwd">class</span> <span class="typ">YourService</span> <span class="pun">{</span>
  <span class="kwd">constructor</span><span class="pun">(</span><span class="kwd">private</span> <a class="code-anchor" href="https://angular.io/api/common/http"><span class="pln">http</span></a><span class="pun">:</span> <a class="code-anchor" href="https://angular.io/api/common/http/HttpClient"><span class="typ">HttpClient</span></a><span class="pun">)</span> <span class="pun">{</span> <span class="pun">}</span>
<span class="pun">}</span></pre>
</div>

<h2>Access the backend</h2>
The Http Request has four parts:
<ul>
	<li>Http Verb: POST, GET, PUT, DELETE</li>
	<li>URL (API Endpoint): /clients/1</li>
	<li>Headers (Metadata): {Content-Type: application/json}</li>
	<li>Body: { title: "My new Post"}</li>
</ul>

<p style="text-align: justify;">A simple example to access the backend is to rescue data from the server using the verb GET. The return of that request is an <em>observable</em> that can be used in the subscribe call. The complete example you can see <a href="https://github.com/fabiana2611/br-prev-analisys/blob/master/src/app/core/http/open-data-br.service.ts">here</a>.</p>

<div>
<pre>this.http.get('http://domain.com/opendata/AIn01')
   .subscribe (resp => console.log(resp));</pre>
</div>

<p style="text-align: justify;">The return can be mapped to a local model defined as an interface. However, if you need the <a href="https://angular.io/guide/http#reading-the-full-response">complete response</a> you can cast to the HttpResponse.</p>

<pre><span class="kwd">// Your model
export</span> <span class="kwd">interface</span> <span class="typ">YourModel</span> <span class="pun">{</span><span class="pln">
  name</span><span class="pun">:</span> <span class="kwd">string</span><span class="pun">;</span><span class="pln">
  email</span><span class="pun">:</span> <span class="kwd">string</span><span class="pun">;</span>
<span class="pun">}

// Casting to your model
this.http.get<<span class="typ">YourModel</span>>('http://domain.com/opendata/AIn01')
  .subscribe (resp => console.log(resp.name + ":"+ resp.email));

// Complete Response
<span class="pln">yourMethod</span>(): <span class="typ">Observable</span><<a class="code-anchor" href="https://angular.io/api/common/http/HttpResponse"><span class="typ">HttpResponse</span></a><<span class="typ">YourModel</span>>> {
<span class="kwd">  return</span> <span class="kwd">this</span>.<span class="pln">http</span>.<span class="kwd">get</span><<span class="typ">YourModel</span>>(
<span class="kwd">       'http://domain.com/opendata/AIn01'</span>,
       {<span class="pln"> observe</span>: <span class="str">'response'</span> });
}
</span></pre>

<p style="text-align: justify;">In case to send data to the server, your need to change the verb. For example, if you will send data, you need to use <a href="https://angular.io/guide/http#making-a-post-request">POST</a> or <a href="https://angular.io/guide/http#making-a-put-request">PUT</a> verb.</p>

<pre><span class="kwd">this</span><span class="pun">.</span><span class="pln">http</span><span class="pun">.</span><span class="pln">post</span><span class="pun"><</span><span class="typ">YourModel</span><span class="pun">>(
    'http://domain.com/opendata/AIn01'</span><span class="pun">,</span><span class="pln">yourObject</span><span class="pun">)</span></pre>
You can follow the same idea to <a href="https://angular.io/guide/http#making-a-delete-request">DELETE</a>.

<p style="text-align: justify;">With this API also is possible to handle <a href="https://angular.io/guide/http#error-handling">errors</a>, using <a href="https://angular.io/guide/http#observables-and-operators">operators</a> to manage the data, customize the <a href="https://angular.io/guide/http#http-headers">header</a>.</p>

<h2>References</h2>
<ul>
	<li><a href="https://angular.io/guide/http" >Angular IO - HTTP</a></li>
</ul>
