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


<h3>Releases</h3>

[Rolling Back plan](https://blog.invgate.com/rollback-plan): Redeploy previous Good version (lead to a downtime, hard to deploy what went wrong, lose data created following the deployment). 

[Zero-Downtime releases](https://docs.unity.com/ugs/en-us/manual/game-server-hosting/manual/concepts/zero-downtime-releases) (hot deployment):  switching users from one release to another instantaneously

[Blue/Green Deployments](https://www.redhat.com/en/topics/devops/what-is-blue-green-deployment): instantly releasing the new version (code and features) to 100% of your users by flipping the traffic switch (usually a load balancer or router)

[Canary Release](https://martinfowler.com/bliki/CanaryRelease.html): The process of exposing a new set of features or a new product version to a small subset of users.


<h3>Be continued...</h3>

### ######################

 <!--

Deployment Automation (AWS Certified DevOps Engineer - Professional)

DOMAIN 1: SDLC
- CI/CD
- AWS CodeBuild
- AWS CodeDeploy
- AWS CodePipeline
- Beanstalk
- Blue/Green Deployment
- Canary Deployment
- Lambda@Edge
- A/B Testing
- Automated Test
- CodeArtifact


Continuous delivery: manual approval step
Continuous Deployment: no approval step

Deployment Lifecycle
- AppSec Hooks in CodeDeploy: Start > Applicationstop > DownloadBundle > BeforeInstall > Install > AfterInstall > ApplicationStart > ValidateService > End

Deployment Policies supported in Beanstalck: 
- All at Once (fastest, but cause downtime): Deploys the new version to all instances simultaneously.
- Rolling: Updates a batch of instances at a time; the environment remains available
- Rolling with additional batch: Launches an extra batch of instances to maintain full capacity during deployment. After update, old instances are terminated.
- Immutable: Deploys the new version to a fresh group of instances (a full batch), then swaps them in after successful deployment.
- Traffic splitting: Splits incoming traffic between old and new application versions, allowing gradual exposure.

Rolling Deployments
- Blue/Green > Deployment = Routing production traffic from blue to green environment
- Canary Deployments: is a process where we deploy a new feature and shift some % of traffic to the new feature to perform some analysis to see if feature is successful
- A/B Testing also referred as split testing) is comparing two versions of a web page to see
which one performs better.



DOMAIN 2: Configuration Management and IaC
DOMAIN 3: Resilient Cloud Solution
DOMAIN 4: Monitoring and Logging
DOMAIN 5: Incident and Event Response
DOMAIN 6: Security and Compliance


-->


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
