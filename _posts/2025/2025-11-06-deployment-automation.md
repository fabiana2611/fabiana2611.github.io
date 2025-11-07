---
layout: post
title:  "Deployment Automation"
date:   2025-11-06
categories: infra
permalink: /:categories/deployment
---

Here is an overview about Deployment. It is part of my understanding about the concepts around the deployment automation. Work In Progress... 

<h3>Concepts</h3>

<p style="text-align: justify;"><a href="https://fabiana2611.github.io/books/infra/ci">Continuous integration</a> is the process to have the code shared faster and validate it. It means "the rapid feedback and the reduction the time when some error is the detected to fix it"</p>

- Development + Unit Test
- Build + Integration Test/Regression Test

<p style="text-align: justify;"><a href="https://continuousdelivery.com/">Continuous Delivery</a> the the process to get the software ready to be executed and apply in some environment to be available to the user. This process needs a validation before the deployment</p>

<p style="text-align: justify;"><a href="https://www.amazon.es/gp/product/1098146727/ref=ox_sc_act_title_1?smid=A1AT7YVPFBWXBL&psc=1">The continuous deployment</a> is similar to delivery but it does not need any approval</p>

- Staging + Load Test/Performance Test
- Production + A/B Test / Canary Analysis

<p style="text-align: justify;"><a href="https://fabiana2611.github.io/infra/infra-pipeline">Pipeline</a> is the process compused of many steps to connect the parts from code creation to user</p>

- commit
- Acceptance stage
- UAT/Capacity/ PROD


<table>
  <tr>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/42UP1fxi2SY?si=j7qqZROTrw13xfqV" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></td>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/LNLKZ4Rvk8w?si=BZl6ex0ibl6gdLH5" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></td>
  </tr>

</table>

<h3>Deployment</h3>

Pratices:
- build once
- repitable for all envs
- smoke-Test your deployments
- Deploy ina similar PROD env before
- Automation (CI/CD pipeline)
- each change should be propagate through the pipeline
- If pipeline fail in some part, all the pipeline should be stopped
- Automating the release
- Automatint unit tests and code Analysis
- Automating Acceptence Tests
- Deployment process must be Idempotent
- Eliminate manual steps
- IaC (Terraform)
- Rollback strategy
- Monitor


Build Tools: 
- Make 
- Ant
- Maven


Deployment Strategies:
- Downtime deployment
- Rolling deployment without replacement
- Rolling deployment with replacement
- Blue/Green deployment: deploying the new code and infrastructure to the Green environment.
- Canary deployment: The process of pushing a new version of code to a small subset of servers or infrastructure.
- [Feature toggle deployment](https://martinfowler.com/bliki/KeystoneInterface.html)
- Promotion deployment


Other Strategies:
- [Keynotes](https://martinfowler.com/bliki/KeystoneInterface.html): 
- [DarkLaunching](https://martinfowler.com/bliki/DarkLaunching.html):


Testing Strategies:
- Canary test pattern
- A/B test pattern
- Shadow test pattern


<table>
  <tr>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/AWVTKBUnoIg?si=MlJWXe5zSm2jdotp" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></td>
    <td><iframe width="360" height="215" src="https://www.youtube.com/embed/zFMgpxG-chM?si=P1o3jQ3xOV3QEmFM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe></td>
  </tr>

</table>


<h3>Releases</h3>

[Rolling Back plan](https://blog.invgate.com/rollback-plan): Redeploy previous Good version (lead to a downtime, hard to deploy what went wrong, lose data created following the deployment). 

[Zero-Downtime releases](https://docs.unity.com/ugs/en-us/manual/game-server-hosting/manual/concepts/zero-downtime-releases) (hot deployment):  switching users from one release to another instantaneously

[Blue/Green Deployments](https://www.redhat.com/en/topics/devops/what-is-blue-green-deployment): instantly releasing the new version (code and features) to 100% of your users by flipping the traffic switch (usually a load balancer or router)

[Canary Release](https://martinfowler.com/bliki/CanaryRelease.html): The process of exposing a new set of features or a new product version to a small subset of users.


<h3>Be continued...</h3>


 


<br />
<h3>References</h3>
<ul>
  <li><a href="https://www.oreilly.com/library/view/fundamentals-of-devops/9781098174583/">Book: Fundamentals of DevOps and Software Delivery</a></li>
  <li><a href="https://continuousdelivery.com/">continuousdelivery.com</a></li>
  <li><a href="https://martinfowler.com/books/continuousDelivery.html">Book - Continuous Delivery</a></li>
  <li><a href="https://www.ibm.com/cloud/learn/continuous-deployment">Continuous Deployment</a></li>
  <li><a href="https://martinfowler.com/bliki/ContinuousDelivery.html">Martin Fowler - ContinuousDelivery</a></li>
  <li><a href="https://martinfowler.com/bliki/DeploymentPipeline.html">Martin Fowler - DeploymentPipeline</a></li>
  <li><a href="https://blog.bytebytego.com/p/a-crash-course-in-cicd">A Crash Course in CI/CD</a></li>
  <li><a href="https://www.youtube.com/watch?v=_higfXfhjdo">Youtube: Everything You NEED to KNOW About Web Applications</a></li>
  <li><a href="https://cloud.google.com/architecture/application-deployment-and-testing-strategies">Google Doc: Application Deployment</a></li>
  <li><a href="https://www.youtube.com/watch?v=_TVNCTK808I">CHEF vs PUPPET vs ANSIBLE vs SALTSTACK</a></li>
  <li><a href="https://launchdarkly.com/blog/blue-green-deployments-versus-rolling-deployments/">Blue-green vs. rolling deployments: pros, cons & implementation</a></li>
</ul>  
