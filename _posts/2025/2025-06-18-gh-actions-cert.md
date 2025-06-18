---
layout: post
title:  "Dive in Github Actions"
date:   2025-06-18
categories: infra
permalink: /:categories/gh-actions-cert
---


<p>This first post about <a href="https://fabiana2611.github.io/infra/github-actions">GitHub Actions</a> I covered the main terms used for that. Now, I'm adding notes considering the certification.</p>

<em>Series: 
[Foundation](https://fabiana2611.github.io/infra/github-foundation)>
[Copilot](https://fabiana2611.github.io/infra/github-copilot)>
[Actions Overview](https://fabiana2611.github.io/infra/github-actions)>
[Dive in Actions](https://fabiana2611.github.io/infra/gh-actions-cert)
</em>

<!-- ##################################################################### -->

<br />
<hr>
<br />
<h2>Initial Concepts</h2>

<ul>
    <li>GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows build, test, and deployment automation. GitHub provides Linux, Windows, and macOS virtual machines to run your workflows, or you can host your own self-hosted runners in your own data center or cloud infrastructure <a href="https://docs.github.com/en/actions/about-github-actions/understanding-github-actions">[understand action]</a></li>
    <li>Actions are the building blocks that power your workflow. <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/using-pre-written-building-blocks-in-your-workflow">[building blocks]</a></li>
    <li>Components: 
        <ul>
            <li>The workflow is triggered when an <b>event</b> occurs (e.g a pull request). The workflow contains one or more <b>jobs</b> which can run in <u>sequential order or in parallel</u>. Each job will run inside its own <u>virtual machine runner</u>, or inside a <u>container</u>, and has one or more <b>steps</b> that either run a <u>script</u> or run an <u>action</u>, which is a reusable extension that can simplify the workflow <a href="https://docs.github.com/en/actions/about-github-actions/understanding-github-actions#the-components-of-github-actions">[components]</a><a href="https://docs.github.com/en/actions/using-workflows/about-workflows">[about workflow]</a><a href="https://docs.github.com/en/actions/using-jobs/using-jobs-in-a-workflow">[using jobs]</a></li>
            <li>Jobs
                <ul>
                    <li>Jobs run in <u>parallel by default</u>. To do in sequence use <b>'needs'</b> <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/using-jobs-in-a-workflow">[jobs]</a></li>  
                    <li>Unlimited number of jobs</li>
                    <li>Dependent jobs in a workflow are used to define the sequential execution order within the workflow <a href="https://docs.github.com/en/actions/using-jobs/using-jobs-in-a-workflow">[jobs in workflow]</a></li>      
                </ul>
            </li>
            <li>Steps
                <ul>
                    <li>Steps represent individual tasks within a job. In the context of workflow, a job is often broken down into smaller steps <a href="https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idsteps">[jobs and steps]</a></li>        
                    <li>You can use the if conditional to prevent a step from running unless a condition is met. It can be expression and use Functions<a href="https://docs.github.com/en/actions/using-jobs/using-conditions-to-control-job-execution">[conditional]</a><a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/evaluate-expressions-in-workflows-and-actions#status-check-functions">[check functions]</a></li>
                    <li>The <b>timeout-minutes</b> keyword is used to set a maximum duration for the execution of individual commands within a step (Default: 360) <a href="https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idtimeout-minutes">[timeout]</a></li>
                    <li>GitHub adds two additional steps to each job to set up and complete the job's execution (<b>Set up job</b> and <b>Complete job</b>)<a href="https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/using-workflow-run-logs#viewing-logs-to-diagnose-failures">[view logs]</a> The <b>Set up job</b> step show the GITHUB_TOKEN permissions<a href="https://docs.github.com/en/actions/security-for-github-actions/security-guides/automatic-token-authentication#modifying-the-permissions-for-the-github_token">[token permission]</a>, Operation System and details of images (Runner Image section shows links to preinstalled Software) <a href="https://docs.github.com/en/actions/using-github-hosted-runners/using-github-hosted-runners/about-github-hosted-runners#preinstalled-software-for-github-owned-images">[preinstalled]</a></li>
                </ul>
            </li>
        </ul>
    </li>
    <li>CI using GitHub Actions offers workflows that can build the code in your repository and run your tests <a href="https://docs.github.com/en/actions/about-github-actions/about-continuous-integration-with-github-actions">[CI]</a></li> 
    <li>CD with GitHub Actions provides features that give you more control over deployments. It's possible use OpenID Connect (OIDC) to interact with cloud <a href="https://docs.github.com/en/actions/about-github-actions/about-continuous-deployment-with-github-actions">[CD]</a></li>
    <li>You can use CLI. GitHub CLI is preinstalled on all GitHub-hosted runners. For each step that uses GitHub CLI, you must set an environment variable called GH_TOKEN to a token with the required scopes. <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/using-github-cli-in-workflows">[CLI]</a></li>
    <li>You can use GitHub Actions workflows to run scripts. <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/adding-scripts-to-your-workflow">[scripts]</a></li>
</ul>

<!-- ##################################################################### -->

<br />
<hr>
<br />
<h2>Security</h2>

<ul>
    <li>GH gives support to OpenID Connect (OIDC) <a href="https://docs.github.com/en/actions/security-for-github-actions/security-hardening-your-deployments/about-security-hardening-with-openid-connect">[about OIDC]</a><a href="https://docs.github.com/en/actions/using-github-hosted-runners/connecting-to-a-private-network/using-an-api-gateway-with-oidc">[api with oidc]</a></li>
    <li>Controlling permissions for GITHUB_TOKEN. The GITHUB_TOKEN lasts until a job finishes or a maximum of 24 hours, whichever comes first <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/controlling-permissions-for-github_token">[token]</a><a href="https://docs.github.com/en/actions/security-guides/automatic-token-authentication">[token auth]</a></li>
    <li>Protection Rules:
        <ul>
            <li>When a workflow job references an environment, the job won't start until all of the environment's protection rules pass <a href="https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment">[use env]</a></li>
            <li>In case workflow requires review, If a job is rejected the workflow fails as the job did not meet the approval criteria set for the review process <a href="https://docs.github.com/en/actions/managing-workflow-runs/reviewing-deployments#approving-or-rejecting-a-job">[approve and reject]</a></li>
        </ul>    
    </li>
    <li>GitHub automatically redacts secrets printed to workflow logs by replacing them with placeholders. <a href="https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions#redacting-secrets-from-workflow-run-logs">[secrets in logs]</a></li>
    <li>To store secrets larger than 48 KB, you have to use encryption with GPG. The encrypted file is stored in the repository, and the decryption passphrase is stored as a secret on GitHub. <a href="https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions#limits-for-secrets">[limits for secrets]</a></li>
    <li>Programmatically access workflow logs: needs  owner, repo, and run_id <a href="https://docs.github.com/en/rest/actions/workflow-runs?apiVersion=2022-11-28#download-workflow-run-logs">[download logs]</a></li>
    <li>Automated release prioritizes security by ensuring that only dependencies are committed to tagged release commits and builds are performed during a release. <a href="https://docs.github.com/en/actions/creating-actions/releasing-and-maintaining-actions#results">[releasing and maintaining]</a></li>
</ul>


<!-- ##################################################################### -->

<br />
<hr>
<br />
<h2>Trigger Workflow</h2>

<ul>
    <li>Workflow triggers are events that cause a workflow to run. These events occur in workflow's repository, outside of GitHub, manually or scheduled <a href="https://docs.github.com/en/actions/writing-workflows/about-workflows">[about woarkflow]</a><a href="https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows">[events trigger]</a>
        <ul>Steps <a href="https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/triggering-a-workflow">[triggering workflows]</a>:
          <li>An event occurs on your repository. The event has an associated commit SHA and Git ref.</li>
          <li>GitHub searches the .github/workflows directory in the root of your repository for workflow files that are present in the associated commit SHA or Git ref of the event.</li>
          <li>A workflow run is triggered for any workflows that have 'on:' values that match the triggering event. Some events also require the workflow file to be present on the default branch of the repository in order to run.</li>
          <li>Each workflow run will use the version of the workflow that is present in the associated commit SHA or Git ref of the event. When a workflow runs, GitHub sets the GITHUB_SHA (commit SHA) and GITHUB_REF (Git ref) environment variables in the runner environment. </li>   
        </ul>
    </li>
    <li>The workflow can be triggered, for example, when an issue has been opened, edited, or milestoned; when a commit or a tag is pushed; when a repository is created from a template; when a discussion has been created, edited, or answered.<a href="https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows">[events trigger]</a><a href=""></a><a href=""></a></li>
    <li>You can use activity <b>types</b> and <b>filters</b> to further control when your workflow will run. <a href="https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/triggering-a-workflow#using-event-activity-types">[event activity type]</a><a href="https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/triggering-a-workflow#using-filters">[using filters]</a>
        <ul>
            <li>In case the workflow has as filter both branches and paths filter, the workflow will only run when both branches and paths are satisfied.</li>
            <li>The 'branches-ignore' can be used for exclusions.</li>
            <li>The branch and branch-ignore can not be used for the same event. <a href="https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#onpull_requestpull_request_targetbranchesbranches-ignore">[target branch and ignore]</a></li>
        </ul>
    </li>
    <li>If you want to manually trigger a specific job in a workflow, you can use an environment that requires approval from a specific team or user. <a href="https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/triggering-a-workflow#using-environments-to-manually-trigger-workflow-jobs">[manual trigger]</a></li>
    <li>The 'on' keyword is used to specify the events (e.g push) that should trigger a workflow.<a href="https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows">[Events to trigger]</a><a href="https://docs.github.com/en/actions/using-workflows/triggering-a-workflow">[trigger]</a></li>
    <li>Use on.ENV_NAME.types to define the type of activity that will trigger a workflow run.<a href="https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#onevent_nametypes">[types]</a></li>
</ul>

<!-- ##################################################################### -->

<br />
<hr>
<br />
<h2>Runners</h2>

<ul>
    <li>jobs.job_id.runs-on <a href="https://docs.github.com/en/actions/writing-workflows/choosing-where-your-workflow-runs/choosing-the-runner-for-a-job">[choose runner]</a></li>
    <li>Types:
        <ul>
            <li>GitHub-hosted runner: 
                <ul>
                    <li>Each job runs in a fresh instance of a runner image specified by runs-on <a href="https://docs.github.com/en/actions/writing-workflows/choosing-where-your-workflow-runs/choosing-the-runner-for-a-job#standard-github-hosted-runners-for-public-repositories">[standar hosted runner]</a><a href="https://docs.github.com/en/actions/using-github-hosted-runners/using-github-hosted-runners/about-github-hosted-runners">[about]</a></li>
                    <li>For jobs run on GitHub-hosted runners, <b>Set up job</b> records <u>details of the runner image</u>, and includes a link to the list of preinstalled tools that were present on the runner machine. <a href="https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/using-workflow-run-logs#viewing-logs-to-diagnose-failures">[view logs]</a></li>
                </ul>
            </li>        
            <li>Larger runner: 
                <ul>
                    <li>Customized use case. More resources. Allow static IPs <a href="https://docs.github.com/en/actions/using-github-hosted-runners/using-larger-runners/about-larger-runners">[large runners]</a><a href="https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners/about-github-hosted-runners#ip-addresses">[ip]</a><a href="https://docs.github.com/en/actions/using-github-hosted-runners/using-larger-runners/about-larger-runners#machine-sizes-for-larger-runners">[size]</a></li>
                </ul>
            </li>
            <li>Self-hosted runner: 
                <ul>
                    <li>more control. It can be in a virtual machine or dedicated hardware <a href="https://docs.github.com/en/actions/writing-workflows/choosing-where-your-workflow-runs/choosing-the-runner-for-a-job#choosing-self-hosted-runners">[self-hosted runner]</a><a href="https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners">[about]</a></li>
                    <li>Self-hosted runner can communicate through a proxy server configuring the proxy settings by environment variables: 'https_proxy: PROXY_URL_TRAFFIC'. <a href="https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/using-a-proxy-server-with-self-hosted-runners">[self-hosted proxy]</a></li>
                    <li>When troubleshooting connectivity issues with a self-hosted runner and validating its access to GitHub services, the development team must use the --check feature alongside the runner's URL and authentication token.  <a href="https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/monitoring-and-troubleshooting-self-hosted-runners#checking-self-hosted-runner-network-connectivity">[connectivity]</a></li>
                    <li>The primary purpose of custom labels for self-hosted runners is to route jobs to specific types of runners based on the labels assigned to those runners<a href="https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/using-self-hosted-runners-in-a-workflow#using-custom-labels-to-route-jobs">[label to route jobs]</a></li>
                    <li>By default, self-hosted runners will automatically perform a software update whenever a new version of the runner software is available.  <a href="https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/autoscaling-with-self-hosted-runners#controlling-runner-software-updates-on-self-hosted-runners">[self-hosted updates]</a></li>
                    <li>Monitor the status of the self-hosted runners: offline, idle, active <a href="https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/monitoring-and-troubleshooting-self-hosted-runners#checking-the-status-of-a-self-hosted-runner">[checking status]</a></li>
                </ul>
            </li>
        </ul>
    </li>
    <li>New runners are automatically assigned to a default group <a href="https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/managing-access-to-self-hosted-runners-using-groups#moving-a-self-hosted-runner-to-a-group">[move to a group]</a></li>
    <li>Custom labels in GitHub Actions operate cumulatively, meaning a runner must have all assigned labels to be eligible to process a job. <a href="https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/using-self-hosted-runners-in-a-workflow#using-custom-labels-to-route-jobs">[custom labels]</a></li>
    <li>Using a combination of GitHub-hosted and self-hosted runners can be beneficial when dealing with resource-intensive tasks. <a href="https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners/about-github-hosted-runners">[hosted runner]</a><a href="https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners">[self-hosted runner]</a></li>
    <li>Runner groups help segregate runners based on team-specific expenses. Runner groups enable effective management and control over resources, ensuring cost allocation aligns with the organization's chargeback model <a href="https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/managing-access-to-self-hosted-runners-using-groups#about-runner-groups">[runner groups]</a></li>
</ul>


<!-- ##################################################################### -->

<br />
<hr>
<br />
<h2>Marketplace</h2>

<ul>
    <li>GitHub Marketplace is a central location for you to find actions created by the GitHub community. <a href="https://github.com/marketplace?type=actions">[marketplace action]</a></li>
    <li>You can add the action you've created to the GitHub Marketplace by tagging it as a new release and then publishing it. <a href="https://docs.github.com/en/actions/creating-actions/publishing-actions-in-github-marketplace">[marketplace]</a></li>
    <li>When drafting a new release and publishing an action to GitHub Marketplace, it is essential that the action's metadata file's category matches an existing GitHub Marketplace category<a href="https://docs.github.com/en/actions/creating-actions/publishing-actions-in-github-marketplace">[marketplace]</a></li>
    <li>Publishing: <a href="https://docs.github.com/en/actions/creating-actions/publishing-actions-in-github-marketplace">[marketplace]</a>
        <ul>
            <li>The action must be in a public repository</li>
            <li>Each repository must contain a single action</li>
            <li>The action's metadata file must be in the root directory</li>
            <li>The name in the action's metadata file must be unique on the GitHub Marketplace</li>
        </ul>
    </li>
    <li>How to decide to use or not an action: <a href="https://learn.microsoft.com/en-us/training/modules/github-actions-automate-tasks/2-github-actions-automate-development-tasks">[automate tasks]</a>
        <ul>
            <li>Review the action's action.yml file to make sure the code does what it says it does</li>
            <li>Check if the action is verified in the GitHub Marketplace</li>
            <li>Check if the action is in the GitHub Marketplace</li>
        </ul>
    </li>
</ul>


<!-- ##################################################################### -->

<br />
<hr>
<br />
<h2>Variables</h2>

<ul>
    <li>Variable precedence: If a variable with the same name exists at multiple levels, the variable at the lowest level takes precedence. <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/store-information-in-variables#configuration-variable-precedence">[variable precedence]</a></li>
    <li>Naming convention <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/store-information-in-variables#naming-conventions-for-configuration-variables">[variable naming]</a></li>
    <li>It is possible to use environment variables using the appropriate syntax for the shell you are using on the runner (e.g $NAME) or use contexts (e.g ${{ CONTEXT.PROPERTY }}). The difference is that the context will be interpolated and replaced by a string before the job is sent to a runner. <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/store-information-in-variables#using-the-env-context-to-access-environment-variable-values">[context variable]</a></li>
    <li>Passing values between steps and jobs <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/store-information-in-variables#passing-values-between-steps-and-jobs-in-a-workflow">[passing values]</a> <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/passing-information-between-jobs">[passing info]</a></li>
    <li>Context <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/accessing-contextual-information-about-workflow-runs">[about]</a><a href="https://docs.github.com/en/actions/using-workflows/triggering-a-workflow#using-event-information">[event information]</a></li>
    <li>Setting a default shell and working directory <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/setting-a-default-shell-and-working-directory">[default shell]</a></li>
    <li>The ‘env’ key in the workflow file sets a custom environment variable for a single workflow. The scope of a custom variable set by this method is limited to the element in which it is defined. <a href="https://docs.github.com/en/actions/learn-github-actions/variables#defining-environment-variables-for-a-single-workflow">[def env variables]</a></li>
    <li>Default Environment Variables: <a href="https://docs.github.com/en/actions/learn-github-actions/variables#default-environment-variables">[default env variables]</a>
        <ul>
            <li>Default environment variables are set by GitHub and are available at every step in a workflow. They provide information about the workflow run and repository. </li>
            <li>The GITHUB_REPOSITORY default environment variable provides the owner and repository name (in the format owner/repository) for the repository where the workflow is running. </li>      
            <li>The RUNNER_OS environment variable provides the operating system of the runner executing the job. Possible values are Linux, Windows, or macOS. </li>  
            <li>The default environment variables starting with "GITHUB_" and "RUNNER_" cannot be overwritten using the GITHUB_ENV file in a workflow.<a href="https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions#setting-an-environment-variable">[env. variables]</a><a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/store-information-in-variables#default-environment-variables">[workflow - default variables]</a></li>
            <li>It is recommended that you use the default environment variables to reference the filesystem rather than using hard-coded file paths</li>
        </ul>
    </li>
    <li>
        <ul>Workflow command
            <li>Workflow commands are used to interact with the runner during the execution of a step, providing a way to pass information, set environment variables, or perform other actions related to the workflow <a href="https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions">[workflow command]</a><a href="https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions#using-workflow-commands-to-access-toolkit-functions">[toolkit]</a></li>
            <li>Send info to summary: echo "### Hello world! :rocket:" >> $GITHUB_STEP_SUMMARY <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions#adding-a-job-summary">[add summary]</a></li>
            <li>Recommended practice for treating environment variables in GitHub Actions across different operating systems and shells:  treat environment variables as case-sensitive <a href="https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions">[workflow commands]</a></li>
            <li>GITHUB_PATH environment variable can be used to to add the a path (e.g. /tmp directory) to the PATH. It can be done using 'echo "/tmp" >> $GITHUB_PATH' <a href="https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions">[workflow commands]</a></li>
        </ul>
    </li>
</ul>


<!-- ##################################################################### -->

<br />
<hr>
<br />
<h2>Workflows</h2>

<ul>
    <li>Workflow syntax: <a href="https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions">[syntax]</a>
        <ul>
            <li>YAML: newlines and indentation; doesn’t allow literal tab characters for indentation.<a href="https://learnxinyminutes.com/docs/yaml/">[YAML]</a></li>   
            <li>Reference action: Git ref, SHA, tag, or branch. <a href="https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions">[metadata syntax]</a></li>     
        </ul>
    </li>
    <li>Run commands<a href="https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners/about-github-hosted-runners">[About runners]</a></li>
    <li>GitHub provides a token (unique GITHUB_TOKEN secret) that you can use to authenticate on behalf of GitHub Actions. <a href="https://docs.github.com/en/actions/security-guides/automatic-token-authentication">[Token]</a></li>
    <li>Avoid passing secrets between processes from the command line it can be visible<a href="https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions#using-secrets-in-a-workflow">[secrets]</a></li>
    <li>One way to ensure that a script file is executable in a workflow job is to manually grant execute permission to the script file on the runner.<a href=""></a></li>
    <li>Jobs that reference an environment configured with required reviewers will wait for an approval before starting: Status -> 'Waiting'; and will fail in 30 days in case not approved<a href="https://docs.github.com/en/actions/managing-workflow-runs/reviewing-deployments">[reviewing depyments]</a></li>
    <li>Matrix:
        <ul>
            <li>The matrix strategy will generate a job for each combination of values from the specified dimensions. The matrix keyword is used within the strategy configuration of the job to define a matrix of different job configuration<a href="https://docs.github.com/en/actions/using-jobs/using-a-matrix-for-your-jobs#using-a-matrix-strategy">[matrix]</a><a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/running-variations-of-jobs-in-a-workflow">[variation of jobs]</a></li>
            <li>GitHub limits the maximum number of jobs generated by a matrix to 256 jobs per workflow run <a href="https://docs.github.com/en/actions/using-jobs/using-a-matrix-for-your-jobs#using-a-matrix-strategy:~:text=A%20matrix%20will%20generate%20a%20maximum%20of%20256%20jobs%20per%20workflow%20run.%20This%20limit%20applies%20to%20both%20GitHub%2Dhosted%20and%20self%2Dhosted%20runners.">[limits]</a></li>   
        </ul>
    </li>
    <li>Cache
        <ul>
            <li>Caching dependencies helps reduce network utilization, runtime, and cost by avoiding the need to download dependencies for every workflow run<a href="https://docs.github.com/en/actions/using-workflows/caching-dependencies-to-speed-up-workflows">[cache]</a></li>
            <li>restore-keys allows you to specify a list of alternative restore keys. These keys are used sequentially in the order provided to find and restore a cache in case of a cache miss. <a href="https://docs.github.com/en/actions/using-workflows/caching-dependencies-to-speed-up-workflows#managing-caches">[managing cache]</a></li>        
            <li>Use cache: The cache action in GitHub Actions automatically creates a new cache if a cache miss occurs during the workflow. This ensures that the necessary dependencies or artifacts are cached for future runs, improving the overall performance and efficiency of the workflow. <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/caching-dependencies-to-speed-up-workflows">[cache]</a><a href="https://docs.github.com/en/actions/using-workflows/caching-dependencies-to-speed-up-workflows#managing-caches">[manage cache]</a></li>
        </ul>
    </li>
    <li>Deploy in cloud <a href="https://docs.github.com/en/actions/deployment/deploying-to-your-cloud-provider/deploying-to-amazon-elastic-container-service">[aws container]</a><a href="https://docs.github.com/en/actions/deployment/deploying-to-your-cloud-provider/deploying-to-azure/deploying-to-azure-kubernetes-service">[azure kubernates]</a><a href="https://docs.github.com/en/actions/deployment/deploying-to-your-cloud-provider/deploying-to-google-kubernetes-engine">[google kubernetes]</a></li>   
    <li>Artifacts <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/storing-and-sharing-data-from-a-workflow">[storing and sharing data]</a>
        <ul>
            <li>Custom retention periods can be configured for individual artifacts using the actions/upload-artifact action in a workflow<a href="https://docs.github.com/en/actions/using-workflows/storing-workflow-data-as-artifacts">[store artificat]</a></li>
            <li>The expiration date of a specific artifact can be checked by the execution of a specific API call that retrieves the expiration date information associated with that artifact. The date can be checked by the 'expires_at' value returned by the “Actions” API <a href="https://docs.github.com/en/actions/using-workflows/storing-workflow-data-as-artifacts">[artifact]</a></li>
            <li>Download the artifacts from the "Artifacts" section of the workflow run associated with the `build` job<a href="https://docs.github.com/en/actions/managing-workflow-runs/downloading-workflow-artifacts">[download artifact]</a></li>
            <li>The level of access required to download workflow artifacts is 'read' <a href="https://docs.github.com/en/actions/managing-workflow-runs/downloading-workflow-artifacts">[download artifact]</a></li>
        </ul>
    </li>
    <li>You can view a GitHub Actions workflow run status for a pull request on the pull request before a merge, on the checks tab of the pull request and within the GitHub Actions tab of the repository<a href="https://docs.github.com/en/actions/using-workflows/triggering-a-workflow">[trigger]</a></li>
    <li>The "Choose a workflow" page shows a selection of recommended starter workflows<a href="https://docs.github.com/en/actions/learn-github-actions/using-starter-workflows">[starter workflows]</a></li>
    <li>Workflows are defined in the .github/workflows <a href="https://docs.github.com/en/actions/using-workflows/about-workflows">[about]</a><a href="https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions">[workflow syntax]</a></li>
    <li>Monitor: <a href="https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/monitoring-workflows/about-monitoring-workflows">[about]</a>
        <ul>
            <li>By default, the artifacts and log files generated by workflows are retained for 90 days before they are automatically deleted. You can adjust the retention period depending on the type of repository <a href="https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#configuring-the-retention-period-for-github-actions-artifacts-and-logs-in-your-repository">[retention period]</a></li>
            <li>GitHub Actions use the Checks API to output statuses, results, and logs for a workflow. GitHub creates a new check suite for each workflow run. The check suite contains a check run for each job in the workflow, and each job includes steps <a href="https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/using-workflow-run-logs">[run logs]</a><a href="https://docs.github.com/en/rest/checks?api">[cheks api]</a></li>
            <li>The logs can be viewed in "Actions" tab. In case a pull request, it can be viewd on the "Checks"  tab<a href="https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/using-workflow-run-logs"></a></li>
            <li>Workflow badges in a private repository are not accessible externally to prevent embedding or linking from unauthorized sources<a href="https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/adding-a-workflow-status-badge">status badge</a></li>
            <li>Adding the parameter "?branch=BRANCH-NAME" to the workflow status badge URL allows you to specify the branch for which you want to display the status. </li>
            <li>"View workflow file" option in the failed run's menu allow view the workflow file associated with a failed run. <a href="https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/viewing-workflow-run-history">[hostory]</a></li>
            <li>Enabling debug logging in the GitHub repository settings increases the verbosity of the job's logs, providing more detailed information that can help troubleshoot issues with the JavaScript action. This is a common first step to gather additional diagnostic information about the failed job. <a href="https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/enabling-debug-logging">[debbug]</a></li>
            <li>To enable step debug logging, set the following secret or variable in the repository that contains the workflow: ACTIONS_STEP_DEBUG to true. If both the secret and variable are set, the value of the secret takes precedence over the variable <a href="https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/enabling-debug-logging">[debug logging]</a></li>
            <li>In GitHub Actions, debug messages printed using workflow commands are not displayed in the logs by default. They are only shown when debug logging is explicitly enabled for the workflow run. If debug logging is not enabled, the debug messages will not appear in the logs, even though they were printed successfully. You must create a secret named ACTIONS_STEP_DEBUG with the value true to see the debug messages set by this command in the log. <a href="https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/enabling-debug-logging">[enabling debug]</a><a href="https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions">[workflow command]</a></li>
        </ul>
    </li>
    <li>Migrate to GH Actions <a href=" https://docs.github.com/en/actions/migrating-to-github-actions/using-github-actions-importer-to-automate-migrations/automating-migration-with-github-actions-importer">[migration]</a></li>
    <li>Billing and limits <a href="https://docs.github.com/en/actions/administering-github-actions/usage-limits-billing-and-administration">[admin]</a></li>
    <li>Metrics <a href="https://docs.github.com/en/actions/administering-github-actions/viewing-github-actions-metrics">[metrics]</a></li>
    <li>Schedule
        <ul>
            <li>You can schedule a workflow to run at specific UTC times using POSIX cron syntax. So using the on: schedule: cron then the correct expression, you can customize your workflow to run on weekdays only. <a href="https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#schedule">[schedule]</a></li>
            <li>GitHub allows you to run scheduled workflows once every five minutes.<a href="https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#onschedule:~:text=The%20shortest%20interval%20you%20can%20run%20scheduled%20workflows%20is%20once%20every%205%20minutes.">[schedule]</a></li>
        </ul>
    </li>
    <li>continue-on-error allows the workflow to continue even if the step fails <a href="https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idcontinue-on-error">[job contibue error]</a></li>
</ul>



<!-- ##################################################################### -->

<br />
<hr>
<br />
<h2>Actions</h2>

<ul>
    <li>In GitHub Actions, workflow files are stored in the .github/workflows directory within the code repository <a href="https://docs.github.com/en/actions/using-workflows/about-workflows#create-an-example-workflow">[create workflow]</a></li>
    <li>The outputs key in the action's metadata syntax is used to declare the outputs produced by the action. These outputs can then be consumed by subsequent steps in the workflow. <a href="https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions">[action metadata syntax]</a></li>
    <li>GitHub issues scoped installation tokens to runners that have read access to the repository containing the actions and automatically expire after one hour, ensuring access control and security. <a href="https://docs.github.com/en/actions/creating-actions/sharing-actions-and-workflows-with-your-organization">[sharing actions]</a></li>
    <li>Print a debug message to the log: `echo "::debug::message"` <a href="https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions#setting-a-debug-message">[debug msg]</a></li>
    <li>The full SHA value must be used when use the commit's SHA for release management <a href="https://docs.github.com/en/actions/creating-actions/releasing-and-maintaining-actions">[release actions]</a></li>
    <li>A composite action allows for consolidating multiple workflow steps into a single action <a href="https://docs.github.com/en/actions/creating-actions/about-custom-actions#composite-actions">[composite]</a></li>
    <li>Semantic versioning (SemVer) provides a systematic approach to versioning (MAJOR.MINOR.PATCH) <a href="https://resources.github.com/learn/pathways/automation/advanced/building-your-first-custom-github-action/">[build action]</a></li>
    <li>All actions require a metadata file (action.yml or action.yaml) that defines the inputs, outputs, and runs configuration for the action.<a href="https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions">[action metadata syntax]</a></li>
    <li>In GitHub Actions, the exit code of an action determines its success or failure status. A zero exit code indicates success, allowing the workflow to execute subsequent tasks. Conversely, a nonzero exit code signifies failure, leading to canceling concurrent actions and skipping future actions in the workflow. <a href="https://docs.github.com/en/actions/creating-actions/setting-exit-codes-for-actions">[exit code]</a></li>
    <li>Execute commands directly on the runner using the run keyword <a href="https://docs.github.com/en/actions/learn-github-actions/essential-features-of-github-actions#adding-scripts-to-your-workflow">[adding scripts]</a></li>
    <li>
        <ul>Custom actions:
            <li>For distribute a custom action: provide a clear and concise description of the action's functionality and selecting the most relevant category <a href="https://resources.github.com/learn/pathways/automation/advanced/building-your-first-custom-github-action/">[building custom action]</a></li>
            <li>JavaScript actions, composite actions, docker container actions <a href="https://docs.github.com/en/actions/creating-actions/about-custom-actions">[about]</a></li>
            <li>JavaScript
                <ul>
                    <li>JavaScript actions require that the runs statement takes two arguments:  'using' and 'main'<a href="https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action">[create js action]</a></li>
                    <li>JavaScript actions in GitHub repositories differ from traditional Node.js projects in their development and distribution processes. They include dependent packages alongside the code and support tagged releases for direct publication to GitHub Marketplace. Due to their integration with various APIs, robust end-to-end testing is encouraged to ensure functionality and security.<a href="https://docs.github.com/en/actions/creating-actions/releasing-and-maintaining-actions#about-javascript-actions">[javascript actions]</a></li>        
                </ul>
            </li>
            <li>Docker
                <ul>
                    <li>The Dockerfile is required for containerized actions, as it specifies the environment and dependencies needed to run the custom action within a container. Containerized actions offer a more isolated and reproducible environment for the action to execute in, making the Dockerfile an essential component for these types of actions. Docker container actions can only be executed on runners with a Linux operating system <a href="https://docs.github.com/en/actions/creating-actions/about-custom-actions">[custom action]</a><a href="https://docs.github.com/en/actions/creating-actions/dockerfile-support-for-github-actions">[docker support]</a><a href="https://docs.github.com/en/actions/creating-actions/dockerfile-support-for-github-actions">[docker container action]</a></li>
                    <li>Checking the GitHub Actions logs provides detailed information about the execution of Docker container actions, including any errors encountered during startup or execution, aiding in troubleshooting. <a href="">[dockerfile support]</a></li>
                    <li>To access an environment variable corresponding to an input in a Docker container action, you must pass the input using the args keyword in the action metadata file. This ensures that the input is correctly passed to the Docker container environment <a href="https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions#example-specifying-inputs">[action metadata syntax]</a></li>
                    <li>The URL for the GitHub Container Registry is ghcr.io. <a href="https://docs.github.com/en/actions/publishing-packages/publishing-docker-images#publishing-images-to-github-packages">[gh container registry]</a></li>
                    <li>Running jobs in a container: Use jobs.JOB_ID.container to create a container to run any steps in a job that don't already specify a container. <a href="https://docs.github.com/en/actions/writing-workflows/choosing-where-your-workflow-runs/running-jobs-in-a-container">[run in a container]</a></li>        
                </ul>
            </li>
            <li>Release:
                <ul>
                    <li>Manage action release: use tags, branches or SHA. <a href="https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/using-pre-written-building-blocks-in-your-workflow#using-release-management-for-your-custom-actions">[action release]</a></li>
                    <li>When no version is specified (e.g. uses: actions/checkout ) then it means that the latest version of the action will be used by default <a href="https://docs.github.com/en/actions/learn-github-actions/finding-and-customizing-actions">[finding and customizing]</a></li>
                    <li>Best practices for release: Create and validate a release on a release branch before creating a tag; Use semantic versioning; release major versions with a beta tag to indicate their status to distinguish between stable releases and those that are still in development or testing phases; introduce a new major version tag for changes that will break existing workflows; move the major version tag to point to the Git ref of the current release <a href="https://docs.github.com/en/actions/creating-actions/releasing-and-maintaining-actions">[releasing actions]</a></li>
                </ul>
            </li>
            <li>Toolkit
                <ul>
                    <li>Use GitHub Actions Toolkit to provides the right packages and avoid other binaries <a href="https://docs.github.com/en/actions/creating-actions/about-custom-actions#javascript-actions">[custom actions - javascript]</a></li>
                    <li>GitHub Packages supports: JavaScript (npm), Ruby (gem), Java (nvm), .NET (dotnet)<a href="https://docs.github.com/en/packages/learn-github-packages/introduction-to-github-packages#about-github-packages">[packages]</a><a href="https://docs.github.com/en/actions/publishing-packages/publishing-nodejs-packages">[publishing node packages]</a><a href="https://docs.github.com/en/packages/managing-github-packages-using-github-actions-workflows/publishing-and-installing-a-package-with-github-actions">[publishing and install packages]</a></li>    
                </ul>
            </li>
        </ul>
    </li>
</ul>


<!-- ##################################################################### -->

<br />
<hr>
<br />
<h2>Manage GitHub Actions for the enterprise</h2>


<ul>
    <li>Actions can be disabled for all organizations or only for a specific one  <a href="https://docs.github.com/en/enterprise-cloud@latest/admin/policies/enforcing-policies-for-your-enterprise/enforcing-policies-for-github-actions-in-your-enterprise">[policy]</a></li>
    <li>To access encrypted secrets within actions and workflows for GitHub Actions, developers can utilize the secrets context provided by GitHub Actions. <a href="https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions#using-secrets-in-a-workflow">[secrets]</a></li>
    <li>Important balance between security (e.g. IP address) and operational efficiency <a href="https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners/about-github-hosted-runners">[hosted runners]</a></li>
    <li>Syntax to reference a secret: `${{ secrets.secret_name }}` <a href="https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions#creating-secrets-for-an-environment">[secrets]</a></li>
    <li>Workflow templates ensure automation is reused and maintained in your enterprise (public and private repositories of the organization) <a href="https://docs.github.com/en/actions/using-workflows/creating-starter-workflows-for-your-organization">[create workflow]</a></li>
    <li>Organization-template workflow has as benefits: promotes consistency, best practices and saves time <a href="https://docs.github.com/en/actions/using-workflows/creating-starter-workflows-for-your-organization">[create workflows]</a></li>
    <li>To effectively manage and collaborate on your organization's diverse reusable components in GitHub Actions workflows, enforce a standardized naming convention across all teams. <a href="https://docs.github.com/en/actions/using-workflows/reusing-workflows">[reuse workflow]</a> <a href="https://docs.github.com/en/actions/sharing-automations/avoiding-duplication">[avoiding duplication]</a></li>
    <li>Reusable workflows can be in the same repository or a different one. In case to set up multiple reusable workflows in your organization, it might be a good idea to set up a common workflow repository.<a href=""></a></li>
    <li>Sharing actions<a href="https://docs.github.com/en/actions/creating-actions/sharing-actions-and-workflows-from-your-private-repository">[sharing actions and workflows]</a></li>
    <li>To protect sensitive projects while leveraging custom GitHub Actions, you can allow GitHub Actions workflows in your private repository to access another private repository containing the custom action or reusable workflow. This approach ensures that actions or workflows stored in private repositories can be used within workflows defined in other private repositories owned by the same organization or user, preserving security and privacy. <a href="https://docs.github.com/en/actions/creating-actions/sharing-actions-and-workflows-from-your-private-repository">[sharing from private]</a></li>
    <li>You can choose to disable GitHub Actions for all repositories in your organization or only allow specific repositories. You can also limit the use of public actions and reusable workflows so that people can only use local actions and reusable workflows within your organization. <a href="https://docs.github.com/en/organizations/managing-organization-settings/disabling-or-limiting-github-actions-for-your-organization#managing-github-actions-permissions-for-your-organization">[managin permissions]</a></li>
    <li>It's possible to create an organization-level secret and configure a policy to limit access to only the specific repositories that can use it <a href="https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions#creating-secrets-for-an-organization">[secrets for organization]</a></li>
    <li>Runner groups are used to collect sets of runners and create a security boundary around them. It makes possible to configure which organizations or repositories are permitted to run jobs on those sets of machines <a href="https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/managing-access-to-self-hosted-runners-using-groups">[runners group]</a></li>
</ul>


<!-- ##################################################################### -->

<br />
<hr>
<br />
<h3>References</h3>
<ul>
  <li><a href="https://assets.ctfassets.net/wfutmusr1t3h/2mMJ6nECbUAdiQMTObbPw6/67cfbffa68fed774a1d280c6c1346635/github-actions-exam-preparation-study-guide__3_.pdf">Study Guide</a></li>
  <li><a href="https://www.udemy.com/course/github-actions-exams/?srsltid=AfmBOopFI7MpPNNBCDrJr8zmDTEWYGNa4sC3dcF0JlhsZGk7k70XUyb0&couponCode=LETSLEARNNOW">Udemy: NEW - GitHub Actions Certification - Practice Exams 2025
</a></li>
  <li><a href="https://www.udemy.com/course/learn-github-actions-ci-cd-devops-pipelines/?srsltid=AfmBOopW3vg9DxTD976SK1AawvP01spofZOexrc2Ytx6Gtd2KhqseI4C&couponCode=LETSLEARNNOW">Udemy: Learn Github Actions for CI/CD DevOps Pipelines</a></li>
</ul>  
