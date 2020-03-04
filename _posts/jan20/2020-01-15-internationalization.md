---
layout: post
title:  "Internationalization in Angular"
date:   2020-01-15
categories: frontend
permalink: /:categories/internationalization-angular
---

<blockquote><em>Internationalization is the process of designing and preparing your app to be usable in different languages.</em></blockquote>
<p style="text-align: justify;">The internationalization allows the application to translate to different languages and related formats such as data, for example.</p>
<p style="text-align: justify;">The internationalization is a feature that you can use if your application needs different languages but also you can use this if it is necessary has <a href="https://medium.com/@TuiZ/how-to-split-your-i18n-file-per-lazy-loaded-module-with-ngx-translate-3caef57a738f">different labels to the same component in a different context</a>.</p>
You will find these many languages, including in <a href="https://docs.oracle.com/javase/8/docs/technotes/guides/intl/index.html">java</a> and <a href="https://angular.io/guide/i18n">angular</a> as well.
<h2>Install</h2>
<p style="text-align: justify;">To prepare your application to the use of this resource you need to install to modules, the <span style="color: #993366;">core</span> and <span style="color: #993366;">http-loader</span>:</p>

<pre>"npm install @ngx-translate/core @ngx-translate/http-loader --save"</pre>
<h2>Configurations and Declarations</h2>
<p style="text-align: justify;">Also, you need to define where these files will be after the build. This configuration is inside the '<span style="color: #993366;">angular.json'</span> file in the property <span style="color: #993366;">assets</span>.</p>
<p style="text-align: justify;">Everything defined inside this property will be copied to the <span style="color: #993366;">dist </span>folder. If your file is inside the <span style="color: #993366;">i18n</span> folder, then, it should be declared in the <span style="color: #993366;">assets</span> to be found by the application.</p>

<pre>"architect": {
  "build": {
    "builder": "@angular-devkit/build-angular:browser",
    "options": {
       ...
       "assets": [
       "src/assets/i18n"
...</pre>
<p style="text-align: justify;">Your class <span style="color: #993366;">AppModule</span> should import the classes related to a translator and a method that you can explicitly define where to find your file.</p>
<p style="text-align: justify;">If you declare the folder for the files, it should be the same declared in the <span style="color: #993366;">assets</span> property. A good example you can see <a href="https://www.codeandweb.com/babeledit/tutorials/how-to-translate-your-angular8-app-with-ngx-translate">here</a>.</p>

<pre>...
import {TranslateLoader, TranslateModule} from "@ngx-translate/core";
import {TranslateHttpLoader} from "@ngx-translate/http-loader";
...
@NgModule({
   ...
   imports: [
     ...
     // ngx-translate and the loader module
     TranslateModule.forRoot({
       loader: {
         provide: TranslateLoader,
         useFactory: HttpLoaderFactory,
         deps: [HttpClient]
      }
    })
   ],
   ...
})
...
export function HttpLoaderFactory(http: HttpClient) {
return new TranslateHttpLoader(http, './assets/i18n/', '.json');
}</pre>
If you have more than one source you can declare the list:
<pre>export function HttpLoaderFactory(http: HttpClient) {
     return new MultiTranslateHttpLoader(http, [
         {prefix: './assets/i18n/', suffix: '.json'},
         {prefix: './assets/i18n/countries', suffix: '.json'}
         ]);
}</pre>
<p style="text-align: justify;"><a href="https://indepth.dev/implementing-multi-language-angular-applications-rendered-on-server/#existing-solution-2-fix-via-importing-json-files-directly">Another way</a> to declare the <span style="color: #993366;">translate</span> file is in the import, where explicitly you add the path:</p>

<pre>import * as translationEn from './assets/i18n/en.json';
import * as translationEs from './assets/i18n/es.json';</pre>
<em>PS: You can use different formats, not only <span style="color: #993366;">json</span>. In <a href="https://angular.io/guide/i18n">Angular guide</a> you can see the use of a different format.</em>
<h2>Using</h2>
<p style="text-align: justify;">To use the <span style="color: #993366;">translate</span> file you have to reference the key declared in your translate file with <a href="https://www.codeandweb.com/babeledit/tutorials/how-to-translate-your-angular8-app-with-ngx-translate">pies and directive</a>. It's possible using parameters as well.</p>

<pre><strong>Pipe</strong>: translation pipe — { { 'yourkey' | translate } }
<strong>Pipe and param</strong>: <p>{ { 'yourkey' | translate: { 'name':'YourPameter'} } }</p>
<strong>Directive</strong>: <element [translate]="'yourkey'"></element>
<strong>Directive and param</strong>: <p [translate]="'yourkey'" [translateParams]="{name: 'YourParam'}"></p></pre>
<h2>Using more than one fragments</h2>
<p style="text-align: justify;">Sometimes, use only one file to describe all the applications can make the maintenance a little hard. Then, it maybe better to break in small files.</p>
<p style="text-align: justify;">The problem is that the translation needs to use only one complete file (<span style="color: #993366;">[en,fr].json</span>). One solution is to add a preprocessing to converge all these files to one.</p>
<p style="text-align: justify;">There is a module that can do this. It's <a href="https://www.npmjs.com/package/ngx-i18n-combine">ngx-i18n-combine</a>. The problem is that the module adds a new level (the name of the file) in the final file. It's good if you have duplicate keys. It will avoid conflicts. If you are expected this it will not be a problem. You just need to remember this when using the Html files.</p>
<p style="text-align: justify;">However, that extra level can be a problem. Another solution is to use module <a href="https://www.npmjs.com/package/json-concat">json-concat</a>. It will only add each file on the and separated by a comma and all the <span style="color: #993366;">json</span> file will be inside the "{}". The problem is the opposite of the <span style="color: #993366;">combine</span>. If you have duplicate keys it will be a problem. You need to know your files to make the better decision of which module to use.</p>
<p style="text-align: justify;">In both cases, it's necessary to have a <a href="https://docs.npmjs.com/misc/scripts">script</a> defined in the <span style="color: #993366;"><em>package.json</em></span> in the "scripts" tag. The scripts should be executed before the build.</p>

<pre>"scripts": {
"concat-json": "json-concat src/i18n/bp src/i18n/fragments src/assets/i18n/en.json",
"combine-json": "ngx-i18n-combine -i ./src/i18n/fragments -o src/assets/i18n/en.json"</pre>
<p style="text-align: justify;">Pay attention to the output source. It should be the same declared in <span style="color: #993366;">assets</span> property in the '<em><span style="color: #993366;">angular.json</span></em>' file. The build will get this file and add it to the <span style="color: #993366;">dist</span> folder. Both module you can give folder such input or a list of files.</p>

<h2>Asynchronous</h2>

<p style="text-align: justify;">If you need pass parameters to the message in your json but the values cames from a service, for example, when the page is rendered there is a possibility that your message will not populate with the parameters.</p>

<p style="text-align: justify;">To guarantee the correct renderization with the values you need to use the <a href="https://alligator.io/angular/ngx-translate/#translateservice">asynchroous way</a> to use the translate service.</p>

In your init method add the code below. It will put the parameters in the messages as soon as the data is recovered.

<pre>
//json files
{
  "firstName": "Your first name is {{paramFirstName}}",
  "lastName": "Your name is {{paramLastName}}"
}

// ngOnInit method
  this.translate.get(['firstName', 'lastName'],
      [{paramFirstName: "Maria"}, { paramLastName: "Silva"}]})
    .subscribe(translations => {
      this.firstName = translations['firstName'];
      this.lastName = translations['lastName'];
    });
</pre>

<h2>Conclusion</h2>
<p style="text-align: justify;">The use of the translate is not a big deal. If you are migrating probably you will have some incompatibilities issues regarding with version.</p>
<p style="text-align: justify;">The big decision, in fact, is if you will use a big file or fragments. Don't worry. There's no right answer. Take your decision and go on.</p>

<h2>References</h2>
<ul>
	<li><a href="https://alligator.io/angular/ngx-translate/">Alligator</a></li>
	<li><a href="https://github.com/ngx-translate/core/issues/199">GitHubIssue</a></li>
</ul>
