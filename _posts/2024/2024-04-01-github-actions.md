---
layout: post
title:  "Github Actions overview"
date:   2024-04-01
categories: infra
permalink: /:categories/github-actions
---


<blockquote>GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline. <a href="GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline. ">[Github]</a></blockquote>

<em>Series: 
[Foundation](https://fabiana2611.github.io/infra/github-foundation)>
[Copilot](https://fabiana2611.github.io/infra/github-copilot)>
[Actions](https://fabiana2611.github.io/infra/github-actions)>
[Dive in Actions](https://fabiana2611.github.io/infra/gh-actions-cert)
</em>

<h2>Intro</h2>

<p><b>Github is: </b></p>
<ul>
  <li>Cloud repository storage (push, pull); </li>
  <li>Code management and collarative development (issues, projects, PR); </li>
  <li>Automation and CI/CD (github actions, github App)</li>
</ul>

<p style="text-align: justify;"><b>Workflow automation service</b> in Github automate all kinds of repository-related process and actions around the code inside the repositories</p>
<ul>
  <li>Code Deployment: CI (code changes are automatically built, tested and merged with existent code) and CD (publishing new version of App after the integration - automate code testing, building, deployment)</li>
  <li>Code and repository Management: Automate code reviews, issue management, etc</li>
</ul>


<p><b>Fork: </b> </p>
<ul>
  <li>The feature that clone a repository for another github account</li>
  <li>The target account will have its own repository on github based in another github repository</li>
  <li>It makes possible to create a PR from an account to the original repo</li>
</ul>

<br />
<h2>Key Elements</h2>

<p><b>Workflow: </b><a href="https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions#workflows">[1]</a></p>
<ul>
  <li>Workflows are attached to repositories. </li>
  <li>The first step to the automation process is create a workflow.</li>
  <li>It includes one or more jobs.</li>
  <li>It can be executed after an event</li>
  <li>You can create a new one by Action menu <a href="https://docs.github.com/en/actions/learn-github-actions/using-starter-workflows#choosing-and-using-a-starter-workflow">[1.1]</a></li>
</ul>

<p><b>Job: </b><a href="https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions#jobs">[2]</a></p>
<ul>  
  <li>It is a process to be executed</li>
  <li>Every job define runner (a execution environment - machine and OS) <a href="https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions#runners">[2.1]</a></li>
  <li>A workflow can have multiple jobs and every job gets its own runner (it's own virtual machine)</li>
  <li>The jobs are executed in parallel as default, or can configure to sequencial order.</li>
  <li>Also is possible add condicional to run a job. </li>
  <li>Jobs have steps that will be executed in the order of their definition</li>
  <li>Job Artifacts (output files, etc): used for sharing log file, app binary, etc <a href="https://docs.github.com/en/actions/using-workflows/storing-workflow-data-as-artifacts">[2.2]</a></li>
</ul>

<p><b>Step: </b></p>
<ul>  
  <li>The steps define what will be done (download, install dependencies, etc).</li>
  <li>Step is a shell script (command in command line that should be executed) or an action (another building block).</li>
  <li>It can have conditions</li>
</ul>

<p><b>Action: </b><a href="https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions#actions">[3]</a></p>
<ul>  
  <li>It is a predefined script that perform a task. </li>
  <li>A typically complex frequently repeated task</li>
  <li>You can use your own or can use a third party actions</li>
  <li>Marketplace is where you can find common actions <a href="https://github.com/marketplace?type=actions">[3.1]</a></li>
</ul>
   
<p><b>Event: </b> (Workflow Triggers) <a href="https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions#events">[4]</a></p>
<ul>  
  <li>The events define when a given workflow will be executed <a href="https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows">[4.1]</a></li>
  <li>Repository-related: push, PR, create, fork, issues, issue_comment, watch, discussion</li>
  <li>Otther: workflow_dispatch, repository_dispach, schedule, workflow_call</li>
  <li>By default, PRs based on forks do NOT trigger a workflow for sacirity reasons</li>
</ul>


<p style="text-align: justify;">Here is an example how it works. The image bellow you can see the sequence of jobs being executed (test, deploy, download and report) and others two in a parallel execution. If one of the sequencial steps fail the other jobs in the sequence will not be executed.</p>

<p>
  <center>
      <img src="/img/git/actions-sequence.png" width="100%" height="100%"/><br />
  </center>
</p>

<p style="text-align: justify;">The code that represent the image you can see in <a href="https://github.com/fabiana2611/gh-second-action/blob/master/.github/workflows/deploy.yml">github repo</a>. You can read more detail about the file here: <a href="https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions#understanding-the-workflow-file">Understanding the workflow file</a>.</p>


<br />
<h2>More</h2>

<p style="text-align: justify;"><b>Contexts:</b> are a way to access information about workflow runs, variables, runner environments, jobs, and steps. <a href="https://docs.github.com/en/actions/learn-github-actions/contexts">[Context]</a></p>


<p style="text-align: justify;"><b>Expressions:</b> use it to programmatically set environment variables in workflow files and access contexts. <a href="https://docs.github.com/en/actions/learn-github-actions/expressions">[Expressions]</a></p>

<p style="text-align: justify;"><b>Default environment variables:</b> are available to every step in a workflow <a href="https://docs.github.com/en/actions/learn-github-actions/variables#default-environment-variables">[Default Variables]</a>.</p>


<p style="text-align: justify;"><b>Custom Action: </b> You can customize your own actions using different approaches <a href="https://docs.github.com/en/actions/creating-actions/about-custom-actions">[Custom Action]</a></p>
<ul>
  <li>JavaScriptActions (node_module us bit ignired but pushed)</li>
  <li>Docker Actions</li>
  <li>Composite Actions</li>
</ul>

<p style="text-align: justify;"><b>Reuse:</b> The workflows can be reused to avoid duplication <a href="https://docs.github.com/en/actions/using-workflows/reusing-workflows">[Reuse]</a>.</p>

<p style="text-align: justify;"><b>Cache:</b>It's possible to use cache to use something already done and avoid do the same process again <a href="https://docs.github.com/en/actions/using-workflows/caching-dependencies-to-speed-up-workflows">[Cache]</a>.</p>

<p style="text-align: justify;"><b>Secrets: </b>It allows to have secrets that can be the same or change by environment <a href="https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions">[Secrets]</a>.</p>

<p style="text-align: justify;"><b>Matrix strategy:</b> run same job in different configuration. Jobs are executed in parallel <a href="https://docs.github.com/en/actions/using-jobs/using-a-matrix-for-your-jobs">[Matrix]</a>.</p>


<p>Security and Permissions</p>
<ul>
  <li><a href="https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions#understanding-the-risk-of-script-injections">script injection</a></li>
  <li><a href="https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions#using-third-party-actions">malicious third-party actions</a></li>
  <li>permission issue</li>
  <li><a href="https://docs.github.com/en/actions/security-guides/encrypted-secrets">More on Secrets</a></li>
  <li><a href="https://docs.github.com/en/actions/security-guides/automatic-token-authentication">Using GITHUB_TOKEN</a></li>
  <li><a href="https://securitylab.github.com/research/github-actions-preventing-pwn-requests/">Preventing Fork Pull Requests Attacks</a></li>
  <li><a href="https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect">Security Hardening with OpenID Connect</a></li>
</ul>  


<br />
<h3>References</h3>
<ul>
  <li><a href="https://www.udemy.com/course/github-actions-the-complete-guide/?couponCode=ST12MT030524">Udemy: GitHub Actions - The Complete Guide</a></li>  
  <li><a href="https://docs.github.com/en/actions">Github Actions</a></li>  
</ul>  
