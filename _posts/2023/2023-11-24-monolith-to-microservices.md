---
layout: post
title:  "Monolith to Microservices"
date:   2023-11-24
categories: arch books
permalink: /:categories/monolith-to-microservices
---

<p><center>
  <a href="https://www.oreilly.com/library/view/monolith-to-microservices/9781492047834/"><img src="/img/books/monolith-to-microservices.png" /></a>
</center></p>

<p style="text-align: justify;">The book presents some strategies to migrate from a monolithic architecture to microservices. It gives an introduction to both and discusses how to make the migration work in the company and patterns that can support this goal. It mentions the fact that the view and strategy should be shared with the company and that people should embrace it. Also, the book raised the question of whether migration is really necessary and used the concepts of DDD to find the Bounded Context.</p>

<p>Some <a href="https://microservices.io/post/refactoring/2020/08/21/ten-principles-for-refactoring-to-microservices.html">principles</a> can resume the first part:</p>
<ul>
  <li>Make the most of your monolith</li>
  <li>Adopt microservices for the right reasons</li>
  <li>It’s not just architecture</li>
  <li>Get the support of the business (Identify the components, group of components and dependencies)</li>
  <li>Migrate incrementally</li>
  <li>Know your starting point</li>
  <li>Begin with the end in mind</li>
  <li>Migrate high-value modules first</li>
  <li>Success is improved velocity and reliability</li>
  <li>If it hurts, don’t do it</li>
</ul>

<br />
<h2>Patterns</h2>

<h3><b><u>Strangler Fig Application</u></b></h3>

<ul>
  <li><b>Benefits:</b> reduced risk, faster benefits, small changes, easier rollbacks.</li>
  <li><b>Summary: </b>Copy or rewrite functionalities from the monolith; implement new functionality in microservice, redirect calls until have all funcionalities in microservice and not need the monolith anymore. It's possible to use proxy to do that.</li>
  <li>Links:
    <ul>
      <li><a href="https://martinfowler.com/bliki/StranglerFigApplication.html">[Martin Fowler] StranglerFigApplication</a></li>
      <li><a href="https://learn.microsoft.com/en-us/azure/architecture/patterns/strangler-fig">[Microsoft] StranglerFigApplication</a></li>
      <li><a href="https://developer.confluent.io/patterns/compositional-patterns/strangler-fig/">[Developer Confluent] StranglerFigApplication</a></li>
    </ul>
  </li>
</ul>

<p><center>
  <iframe width="360" height="215" src="https://www.youtube.com/embed/8h3moilCpQ4?si=C9uYx99wYLUYRYPs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</center></p>

<h3><b><u>UI Decomposition</u></b></h3>

<ul>
  <li>Reflect the migration</li>
  <li>It can be Widget or Page level. Also work with micro frontend.</li>
  <li>It allows vertical slices of the functionality to be migrated</li>
</ul>

<h3><b><u>Brach by Abstraction</u></b></h3>

<ul>
  <li>Alternative when the code in monolith is being improved yet.</li>
  <li>Summary: it creates an abstraction of an existent functionality and change the clienti to use it. Then a new implementation should be created to use the microservice and then change the client to use the microservice. When the process is finished should do the clenup to use only the microservice. </li>
  <li>Links:
    <ul>
      <li><a href="https://martinfowler.com/bliki/BranchByAbstraction.html">[Martin Fowler] BranchByAbstraction</a></li>
      <li><a href="https://trunkbaseddevelopment.com/branch-by-abstraction/">[Trunk Based Development] BranchByAbstraction</a></li>
    </ul>
  </li>
</ul>

<p><center>
  <iframe width="360" height="215" src="https://www.youtube.com/embed/vDVxwR_nMOs?si=_MVIKB8s9mpPIsih" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</center></p>


<h3><b><u>Parallel Run</u></b></h3>

<ul>
  <li>Alternative when is necessary to verify is the new solution has the same result of the old one.</li>
  <li>Used when the changes are high risk</li>
  <li>Techniques: Spy and GitHub Scientis</li>
</ul>

<h3><b><u>Decorating Collaborator</u></b></h3>

<ul>
  <li>It can be used when is necessary to add some feature but cannot change the monolith</li>
  <li>Use a proxy to redirect to the new functionality.</li>
  <li>It is better when the information required is in request and response</li>
</ul>


<h3><b><u>Change data Capture</u></b></h3>

<ul>
  <li>Based on the data changes and cannot check it by monolith</li>
</ul>

<p><center>
  <iframe width="360" height="215" src="https://www.youtube.com/embed/ARWNnnDGPag?si=WhJ02EAvwDp3U6MJ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</center></p>

<br />
<h2>Database Patterns</h2>

<p><b><u>Shared Database</u></b>: It is better to read-only static reference data and Database-as-a-Service <a href="https://www.linkedin.com/pulse/shared-database-pattern-microservices-arpit-bhayani/">[1]</a><a href="https://www.enterpriseintegrationpatterns.com/patterns/messaging/SharedDataBaseIntegration.html">[2]</a><a href="https://www.baeldung.com/cs/microservices-db-design#shared-db">[3]</a></p>

<p><b><u>Database View</u></b>: (1) Create View to legacy; (2) Useful to read-only <a href="https://overcoded.dev/posts/BC-34">[1]</a><a href="https://www.oreilly.com/library/view/monolith-to-microservices/9781492047834/ch04.html#ch05c-materialized-view">[2]</a></p>

<table>
  <tr>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/PI8UrOAZs2U?si=_SswrkYchJQsucch" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></td>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/vLLkNI-vkV8?si=O7Hd5xHIrD_it2UI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></td>
  </tr>
</table>

<p><b><u>Database Wrapping Service</u></b><a href="https://www.oreilly.com/library/view/monolith-to-microservices/9781492047834/ch04.html#ch05-schema-as-a-service-pattern">[1]</a><a href="https://overcoded.dev/posts/BC-35">[2]</a></p>
<ul>
  <li>Allow control what can be shared what should be hidden</li>
  <li>Use in a complex schema, </li>
  <li>Similar to the View but the logic is in code and can have write logics.</li>
</ul>

<p><b><u>Database as a Service</u></b><a href="https://www.oreilly.com/library/view/monolith-to-microservices/9781492047834/ch04.html#pattern-database-as-a-service-interface">[1]</a><a href="https://www.ibm.com/topics/dbaas">[2]</a></p>
<ul>
  <li>Create a read-only database to a specific goal to be exposed externally behind an API service</li>
  <li>Point: how to update when change: change data capture system (ex: debezium) or  batch process to copy data or listener events fired</li>
</ul>

<p><center>
  <iframe width="360" height="215" src="https://www.youtube.com/embed/34hgRvgbPMY?si=5xZM7Y6lpNOJIJPa" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
  <iframe width="360" height="215" src="https://www.youtube.com/embed/qfiOVB3yMHQ?si=j7GDCahezn9ZZKxp" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</center></p>


<p><b><u><a href="https://www.oreilly.com/library/view/monolith-to-microservices/9781492047834/ch04.html#pattern-aggregate-exposing-monolith">Aggregate Exposing Monolith</a></u></b></p>
<ul>
  <li>Microservice needs to interact with agregated data that is in monolith yet</li>
  <li>Access those data by an API</li>
</ul>

<p><b><u>Change Data Ownership</u></b>: Microservice needs data that in monolith but under the control of the new extracted service <a href="https://www.oreilly.com/library/view/monolith-to-microservices/9781492047834/ch04.html#pattern-change-data-ownership">[1]</a></p>

<p><b><u>Scynchronize Data in Application</u></b>: Data synchronization jobs are by far the most common type of integration job, during which we take data from one or more systems and move it into another (keeping the data in sync)—in our case, Salesforce. Data can flow from one system to another, and back. Sometimes this causes data conflicts that must be dealt with. Getting synchronizations working right can be tricky, particularly when there are heavy transformations and/or summarizations involved.  <a href="https://www.oreilly.com/library/view/developing-data-migrations/9781484242094/html/463790_1_En_9_Chapter.xhtml">[1]</a></p>

<ul>Steps:
  <li>1. Bulk synchronie data </li>
  <li>2. Synchronize on write, read from old schema.</li>
  <li>3. Synchronize on write, read from new schema.</li>
  <li>4. Decommission old schema.</li>
</ul>

<p><em>Use it when split schema before split the application code and be sure about the synchronization between micro and monolith.</em><a href="https://hasanenko.medium.com/data-synchronization-patterns-c222bd749f99">[2]</a></p>


<p><b><u>Tracer Writer</u></b></p>
<ul>
  <li>There are the both database and is used a new service that will get in the new database. The old database can be read but only write in the new database. It reduce the mantainance cost.</li>
  <li>It's necessary to take care about the consistency between the database.</li>
</ul>

<p><b><u>Split Database: Repository per bouded context</u></b></p>
<ul>
  <li>This patterns is used when decide split the database before the code</li>
  <li>It is a logic way to separate de data by the context using repository pattern. The application can have meny repositories interface to access the same database.</li>
  <li>It is good to focus in monolith and understand the best way to do that. That repository layer will help to see what microservices can exist.</li>
</ul>


<p><b><u>Split Database: Database per bouded context</u></b></p>
<ul>
  <li>This patterns is used when decide split the database before the code</li>
  <li>It is phical way to separate the data by context. That decomposition happen before separate the code. For this, each bounded context has its own database.</li>
  <li>One point to keep the eys is the maintannace of that structure if spend long time with monolith yet.</li>
</ul>


<p><b><u>Split the code first: Monolith as data access layer</u></b></p>
<ul>
  <li>Create a service in monolith to access the database.</li>
  <li>Best when the code that manage the data is sting in monolith and not migrated</li>
</ul>


<p><b><u>Split the code first: Multischema storage</u></b> </p>
<ul>
  <li>Persist part of the new databa with new schema in the new database.</li>
  <li>One point is that one entity can have part of its data in one schema and the others in the other database. When the app have a new functionality it can be good</li>
</ul>


<p><b><u>Split Table</u></b>: When different bounded context use parts of a table can be useful to microservice split those tables.</p>

<p><b><u>Move Fireign-key Relationship to Code</u></b></p>
<ul>
  <li>Split two tables that has a relationship between then.</li>
  <li>To have the foreign-key in the new schema brings some points as consistence (delete) and performance (join).</li>
  <li>It can be done or avoiding deletion or be sure the other system can survive without that information.</li>
  <li>Patterns: 
    <ul>
      <li>dupplicate static data -> each service has its own copy of data</li>
      <li>dedicated reference data schema -> realocate the code to be access to both schemas</li>
      <li>static reference data library -> add the data in a library to be shared. It's trick in case multiple technologies, then is necessary to have different version of the library. better to small valumes of data.</li>
      <li>static reference data service: create a service -> the main discussion is the cost.</li>
    </ul>
  </li>
</ul>


<h3><b>Transaction</u></h3>

<p><b><u>Two-Phase</u></b> commits algorithm: transactionla changes in distributed system where many process need to be executed as part of a bigger operation.</p>
<ul>
  <li>1. Voting phase: exist a coordenator to contact the parts and ask for confirmation</li>
  <li>2. commit phase: if all the parts agreed about change the state then go to commit. If at least one fail all the operation is aborted.</li>
</ul>

<p><em>cannot guarantee those commits happen exactly in the same time</em></p>
<p><em>Used in short-lived operations to avoid block system with big operations</em></p>
  
<p><b><u>Distributed transactions - Just say No</u></b>: Let the satate in a single database and mange the stage by a single service</p>

<p><b><u>Saga</u></b> <a href="https://www.baeldung.com/cs/microservices-db-design#1-saga-pattern">[1]</a></p>
<ul>
  <li>It is used when you need break the data but don't want to mange distributed transaction and to manage multiple operation without lock the system</li>
  <li>Long Lived Transactions (LLT): transactions can spend long time and persist in database.</li>
  <li>LLTs should be breaking into a sequence of transactions. Each onde has a short live and change a smal part of database.</li>
  <li>In case of failure: 
    <ul>
      <li><b>backward recovery</b>: rollback / clean up / undo previous commits / it is new transaction to revert</li>
      <li><b>forward recovery</b>: continue the transaction from the point of the failure</li>
    </ul>
  </li>
</ul>

<br />
<h2>Be continued...</h2>
<h3>Never Stop</h3>
<h3>Evolutionary point of view in the Architecture Style</h3>

<br />
<h3>Reference</h3>

<ul>
  <li><a href="https://danlebrero.com/2022/02/09/monolith-to-microservices-summary/">Book notes: Monolith to Microservices: Evolutionary Patterns to Transform Your Monolith</a></li>
  <li><a href="https://learn.microsoft.com/en-us/azure/architecture/microservices/migrate-monolith">Migrate a monolithic application to microservices using domain-driven design</a></li>
  <li><a href="https://semaphoreci.com/blog/monolith-microservices">12 Ways to Improve Your Monolith Before Transitioning to Microservices</a></li>
  <li><a href="https://martinfowler.com/articles/break-monolith-into-microservices.html  ">How to break a Monolith into Microservices</a></li>
  <li><a href="https://ifgeekthen.nttdata.com/es/descomposicion-de-monolitos-patrones-de-arquitectura-aplicados-en-aws-segunda-parte">[Descomposición de Monolitos: Patrones de Arquitectura aplicados en AWS (Segunda Parte)</a></li>
  <li><a href="https://dzone.com/articles/design-patterns-for-microservices">Design Patterns for Microservices</a></li>
  <li><a href="https://refactorizando.com/en/patterns-to-migrate-from-monolith-to-microservices/">Patterns to migrate from Monolith to Microservices</a></li>
  <li><a href="https://martinfowler.com/articles/extract-data-rich-service.html">How to extract a data-rich service from a monolith</a></li>
</ul>











