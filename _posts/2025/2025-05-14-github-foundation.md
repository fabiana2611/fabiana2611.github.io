---
layout: post
title:  "GitHub Foundation"
date:   2025-05-14
categories: infra
permalink: /:categories/github-foundation
---

<p>Hare are some notes about GitHub Foundation. The concepts were extracted from documentation and Udemy training.</p>

<ol>
  <li><a href="#d1">Basic</a></li>
  <li><a href="#d2">Repositories</a></li>
  <li><a href="#d3">Collaboration</a></li>
  <li><a href="#d4">Development</a></li>
  <li><a href="#d5">Project Management</a></li>
  <li><a href="#d6">Privacy, Security, and Administration</a></li>
  <li><a href="#d7">Community</a></li>
</ol>


<br />
<h2>Introduction to Git and GitHub</h2>


<h3 id="d1">Git and GitHub Basics</h3>

<ul>
  <li><b>Open Source</b>: 
    <ul>
      <li><em>open source software (OSS) refers to software that features freely available source code, which users may view, modify, adopt, and share for both commercial and noncommercial purposes.</em><a href="https://github.com/resources/articles/software-development/what-is-open-source-software">[1]</a></li>
    </ul>
  </li>
  <li><b>Version Control</b>: 
    <ul>
      <li><em>A version control system (VCS) is a program or set of programs that tracks changes to a collection of files facilitating collaboration, and maintaining a history of modifications. Another name for a VCS is a software configuration management (SCM) system. </em> <a href="https://learn.microsoft.com/en-us/training/modules/intro-to-git/1-what-is-vc">[1]</a></li>
      <li>VCS does not aim to ensure compliance with industry regulations as files are created or changed<a href="https://docs.github.com/en/get-started/using-git/about-git">[1]</a></li>
    </ul>
  </li>
  <li><b>Distributed Version Control</b>: 
    <ul>
      <li><em>Every developer has a full copy of the project and project history. It means DVCSs don't need a constant connection to a central repository.</em> <a href="https://docs.github.com/en/get-started/using-git/about-git#about-version-control-and-git">[1]</a></li>
      <li><em>Git is distributed, which means that a project's complete history is stored both on the client and on the server. </em><a href="https://learn.microsoft.com/en-us/training/modules/intro-to-git/1-what-is-vc">[2]</a></li>
    </ul>
  </li>
  <li><b>Git</b><a href="https://learn.microsoft.com/en-us/training/modules/intro-to-git/1-what-is-vc">[1]</a>: 
    <ul>
      <li>Decentralized or distributed version control system. Git is free and open-source. Git's de-facto standard status: wide adoption and integration into other tools. </li>
      <li>Terminology: Working tree; repository; hash; object (blob, tree, commit, tag); commit; branch; remote; command, subcommand and options</li>
    </ul>
  </li>
  <li>
    <b>GitHub repository</b>: 
    <ul>
      <li><em>Repository (repo): The directory, located at the top level of a working tree, where Git keeps all the history and metadata for a project.</em> <a href="https://learn.microsoft.com/en-us/training/modules/intro-to-git/1-what-is-vc">[1]</a></li>      
    </ul>
  </li>
  <li><b>Commit</b>: 
    <ul>
      <li>As a verb, committing changes means you put a copy (of the file, directory, or other "stuff") in the repository as a new version. When the command is invoked, the work is saved to a snapshot. As a noun, a commit is the small chunk of data that gives the changes you committed a unique identity. The data that's saved in a commit includes the author's name and e-mail address, the date, comments about what you did (and why), an optional digital signature, and the unique identifier of the preceding commit. <a href="https://learn.microsoft.com/en-us/training/modules/intro-to-git/3-basic-git-commands">[1]</a></li>
    </ul>
  </li>
  <li><b>Branching</b>: 
    <ul>
      <li>A branch is a named series of linked commits. The most recent commit on a branch is called the head. The default branch, which is created when you initialize a repository, is called main, often named master in Git. The head of the current branch is named HEAD. <a href="https://learn.microsoft.com/en-us/training/modules/intro-to-git/1-what-is-vc">[1]</a></li>
    </ul>
  </li>
  <li><b>GitHub</b>: 
    <ul>
      <li><em>GitHub is a web-based app that lets you host files in repositories, collaborate on work, and track changes to files over time. Version tracking on GitHub is powered by the open source software Git. Whenever you update a repository on GitHub, Git tracks the changes you make.</em><a href="https://docs.github.com/en/get-started/using-github/connecting-to-github#introduction">[1]</a></li>
      <li><em>GitHub hosts Git repositories and provides developers with tools to ship better code through command line features, issues (threaded discussions), pull requests, code review, or the use of a collection of free and for-purchase apps in the GitHub Marketplace. </em></li>
      <li><em>GitHub is a cloud platform that uses Git as its core technology. GitHub acts as the remote repository. </em><a href="https://learn.microsoft.com/en-us/training/modules/intro-to-git/1-what-is-vc">[2]</a></li>
    </ul>
  </li>
  <li><b>Git vs GitHub</b>: 
    <ul>
      <li>The main difference between Git and GitHub is that Git is a distributed version control system that you install and run locally on your computer. It helps you track changes to your code over time. GitHub, on the other hand, is a web-based platform that provides hosting for Git repositories. It adds many collaborative features on top of Git, such as issue tracking, pull requests, and a web interface for managing your code. Think of Git as the engine for version control, and GitHub as a popular online service that uses Git as its engine and provides a social and collaborative environment for developers. [from Gemini]</li>
    </ul>
  </li>
  <li><b>GitHub flow</b>: 
    <ul>
      <li><em>"GitHub flow": create branch or fork, edit and preview files, commit changes, and create a pull request; besides upload/download files from/to your computer.</em> <a href="https://docs.github.com/en/get-started/using-github/github-flow#following-github-flow">[1]</a></li>
    </ul>
  </li>
</ul>


<h3>CLI</h3>

<ul>
  <li>Working from local: <a href="https://docs.github.com/en/get-started/git-basics/set-up-git">Git</a> and <a href="https://docs.github.com/en/github-cli/github-cli/about-github-cli">GH</a></li>
  <li>GraphQL:
    <ul>
      <li><a href="https://docs.github.com/en/graphql/overview/about-the-graphql-api">The GitHub GraphQL API offers flexibility and the ability to define precisely the data you want to fetch</a></li>
      <li><a href="https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/using-the-api-to-manage-projects">You can use the GraphQL API to automate your projects</a></li>
    </ul>
  </li>
  <li><a href="https://docs.github.com/en/get-started/using-git/about-git#github-and-the-command-line">Basic command line</a></li>
  <li><a href="https://education.github.com/git-cheat-sheet-education.pdf">Git Cheat Sheet</a></li>
</ul>


{% highlight ruby %}
git init demo
git status
git show 09e90cd7
git log --oneline
git help commit
git revert HEAD README.md
git checkout -- README.md
git diff 09e90cd7 HEAD

// Alias:
git log --oneline --graph --decorate --all
git config --global alias.hist "log --oneline --graph --decorate --all"
git config --global --list
git hist -- README.md

// connections
git remote -v

// Set default branch
git config --global init.defaultBranch main

// tag
git tag mytag mybranch
git tag
git tag -a v0.1-beta -m "Release 0.1 (Beta)" 85fe102 
git show v0.1-beta
git push origin mytag
git push --tags
{% endhighlight %}


<h3>GitHub Entities</h3>

<em>Every user has an GH account. Accounts allow you to organize and control access to that code.</em>

<ul>
  <li><b>GitHub accounts (personal, organization, enterprise)</b>:
    <ul>
      <li><a href="https://docs.github.com/en/get-started/learning-about-github/types-of-github-accounts#user-accounts">User account:</a>
        <ul>
          <li>Personal account: if you signed up for your own account on GitHub.com, you are using a personal account</li>
          <li>Managed account: account created by an enterprise on GitHub Enterprise Cloud. You can create your own private repositories</li>
          <li>Machine users are accounts created to automate an activity</li>
        </ul>        
      </li>
      <li><a href="https://docs.github.com/en/get-started/learning-about-github/types-of-github-accounts#organization-accounts">Organization account:</a>
        <ul>
          <li>Organizations are shared accounts where a large number of people can collaborate across many projects at once. </li>
          <li>Organizations are limited to owning 100,000 repositories.</li>
          <li>An organization account enhances collaboration between multiple users</li>
        </ul>
      </li>
      <li><a href="https://docs.github.com/en/get-started/learning-about-github/types-of-github-accounts#enterprise-accounts">Enterprise account:</a>
        <ul>
          <li>Centrally manage policy and billing for multiple organizations and enable innersourcing between the organizations. </li>
          <li>Allows central management of multiple organizations</li>
        </ul>
      </li>
    </ul>
  </li>
  <li><b>GitHub’s products for personal accounts (free, pro)</b>: 
    <ul>
      <li>All personal accounts can own an unlimited number of public and private repositories, with an unlimited number of collaborators on those repositories.</li>
      <li>GitHub Free: private repositories owned by your personal account have a limited feature set. You can upgrade to GitHub Pro to get a full feature set for private repositories. <a href="https://docs.github.com/en/get-started/learning-about-github/types-of-github-accounts#personal-accounts">[1]</a></li>
    </ul>
  </li>
  <li><b>GitHub’s products for organization accounts (free for organizations, teams)</b>: 
    <ul>
      <li> You can use organizations for free, with GitHub Free, which includes limited features on private repositories.<a href="https://docs.github.com/en/get-started/learning-about-github/types-of-github-accounts#organization-accounts">[1]</a></li>
      <li>Organization owners can assign roles to individuals and teams giving them different sets of permissions in the organization<a href="https://docs.github.com/en/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization">[1]</a></li>
      <li>You can manage a person's access to a repository owned by your organization.<a href="https://docs.github.com/en/organizations/managing-user-access-to-your-organizations-repositories/managing-repository-roles/managing-an-individuals-access-to-an-organization-repository">[1]</a></li>
      <li>You can invite former organization members to rejoin your organization, and choose whether to restore the person's former role, access permissions, forks, and settings<a href="https://docs.github.com/en/organizations/managing-membership-in-your-organization/reinstating-a-former-member-of-your-organization">[1]</a></li>
      <li>Before requiring two-factor authentication (2FA), you can notify users about the upcoming change and verify who already uses 2FA<a href="https://docs.github.com/en/organizations/keeping-your-organization-secure/managing-two-factor-authentication-for-your-organization/preparing-to-require-two-factor-authentication-in-your-organization">[1]</a></li>
      <li>Teams are groups of organization members that reflect your company or group's structure with cascading access permissions and mentions<a href="https://docs.github.com/en/organizations/organizing-members-into-teams/about-teams">[1]</a></li>
    </ul>
  </li>
  <li>Deployment options for GitHub Enterprise<a href="https://docs.github.com/en/enterprise-cloud@latest/admin/overview/about-github-for-enterprises#about-deployment-options">[1]</a>:
    <ul>
      <li>GH Enterprise Cloud: Hosted by GH</li>
      <li>GH Enterprise Server: hosted in your own GH instance (on-premises or cloud service)</li>
    </ul>
  </li>
  <li><b>Features in the user profile (metadata, achievements, profile readme, repositories, pinned repositories,stars, etc.)</b>:
    <ul>
      <li>Your profile page tells people the story of your work through the repositories you're interested in, the contributions you've made, and the conversations you've had.<a href="https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/customizing-your-profile/about-your-profile">[1]</a></li>
      <li>You can add a README to your GitHub profile to tell other people about yourself.<a href="https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/customizing-your-profile/managing-your-profile-readme">[1]</a></li>
      <li>You can PIN gists and repositories to your profile so other people can quickly see your best work.<a href="https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/customizing-your-profile/pinning-items-to-your-profile">[1]</a></li>
      <li>Organization's profile page shows basic information about your organization.<a href="https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/customizing-your-profile/about-your-organizations-profile">[1]</a></li>
    </ul>
  </li>
</ul>


<h3>GitHub Markdown</h3>

<ul>
  <li>Markdown is a lightweight markup language for formatting text in README files, issues, and comments on GitHub. It provides a simple and readable way to style text and add elements such as headers, lists, links, and images. It's NOT specific to GitHub. <a href="https://docs.github.com/en/contributing/writing-for-github-docs/using-markdown-and-liquid-in-github-docs">[1]</a><a href="https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/quickstart-for-writing-on-github">[2]</a><a href="https://github.com/adam-p/markdown-here/wiki/markdown-cheatsheet">[3]</a><a href="https://www.markdownguide.org/getting-started/">[4]</a></li>
</ul>

<h3>GitHub Desktop</h3>

<ul>
  <li>GitHub Desktop is a free, open source application that helps you to work with files hosted on GitHub or other Git hosting services.<a href="https://docs.github.com/en/desktop/overview/about-github-desktop">[1]</a></li>
  <li><b>GitHub Desktop vs github.com</b>: GitHub Desktop is a graphical user interface (GUI) for interacting with GitHub, a website where you can host and manage Git repositories. It allows you to perform common Git operations like cloning, committing, pushing, and pulling, but through a visual interface instead of using the command line. Github.com is the website itself, where you can host repositories, create issues, and collaborate with others. [from Gemini]</li>
</ul>


<h3>GitHub Mobile</h3>

<ul>
  <li>Triage, collaborate, and manage your work on GitHub from your mobile device<a href="https://docs.github.com/en/get-started/using-github/github-mobile">[1]</a></li>
  <li>Features: web-based code editing in PR; read, review, and collaborate on issues and pull requests <a href="https://github.com/features">[1]</a></li>
</ul>


<br />
<hr>
<br />
<h2 id="d2">Working with GitHub Repositories</h2>

<ul>
  <li><b>Best practices</b><a href="https://docs.github.com/en/repositories/creating-and-managing-repositories/best-practices-for-repositories">[1]</a>: 
    <ul>
      <li>Create a README file for every repository; </li>
      <li>single repository to streamline collaboration, creating pull requests between branches instead of between repositories.</li>
      <li>Forking is best suited for accepting contributions from people who are unaffiliated with a project, such as open-source contributors; </li>
      <li>To track large files in a Git repository, GitHub recommends using Git Large File Storage (Git LFS) </li>
    </ul>
  </li>
  <li><b>Recommended file</b> for a new repo that provide essential information about the project, help contributors understand the codebase, and maintain transparency in the development process: .gititnore, a contributing file to document the guidelines on how people should contribute to your project, a <a href="https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository">licence</a> that communicates how users can use the files contained in the repository, <a href="https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes">readme</a>, <a href="https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners">CODEOWNERS</a></li>
  <li>README
    <ul>
      <li>Goal: why your project is useful, what they can do with your project, how they can use it, Where users can get help, Who maintains and contributes<a href="https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes">[1]</a></li>
      <li>Where to put: .github, root and docs; using that precedence </li>
      <li>License: public repo needs that to be free to use by others. Without a license, the default copyright laws apply, meaning that you retain all rights to your source code and no one may reproduce, distribute, or create derivative works from your work <a href="https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository">[1]</a></li>
      <li>Codeowners: You can use a CODEOWNERS file to define individuals or teams that are responsible for code in a repository.<a href="https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners">[1]</a></li>
      <li><a href="https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/classifying-your-repository-with-topics">Topics</a>: To help other people find and contribute to your project</li>
    </ul>
  </li>
  <li>How to
    <ul>
      <li><a href="https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository">Create a new repository</a></li>
      <li><a href="https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository">Clone a repository</a></li>
      <li>Add files to a repository<a href="https://docs.github.com/en/repositories/working-with-files/managing-files/creating-new-files">[1]</a><a href="https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository">[2]</a></li>
      <li><a href="https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository#adding-a-file-to-a-repository-using-the-command-line">Add a file to a repository using the command line</a></li>
      <li><a href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-and-deleting-branches-within-your-repository">Create a new branch</a></li>
      <li><a href="https://docs.github.com/en/get-started/exploring-projects-on-github/saving-repositories-with-stars">Save a repository with stars</a></li>
      <li>View repository insights<a href="https://docs.github.com/en/issues/planning-and-tracking-with-projects/viewing-insights-from-your-project/about-insights-for-projects">[1]</a></li>
      <li>Create repository templates (generate new repositories with the same directory structure, branches, and files) <a href="https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository">[1]</a><a href="https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template">[2]</a></li>
    </ul>
  </li>
  <li>Different features to maintaining a repository: Access Control and Permissions, <a href="https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-branches-in-your-repository">Branch Management</a>, <a href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests">Pull Requests</a>, <a href="https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues">Issue Tracking</a>, Managing <a href="https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/managing-labels">labels</a> and <a href="https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/about-milestones">Milestones</a>, <a href="https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases">Releases</a>, <a href="https://docs.github.com/en/actions/about-github-actions/understanding-github-actions">Github Action</a>, <a href="https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings">Repository Setting</a>, <a href="https://docs.github.com/en/get-started/git-basics/ignoring-files">.gitignore file</a>, <a href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/about-pull-request-reviews">Code review tools</a></li>
  <li><a href="https://docs.github.com/en/get-started/using-github/exploring-early-access-releases-with-feature-preview">Feature previews</a></li>
  <li>You can restrict who has access to a repository by choosing a repository's visibility: public, internal, or private<a href="https://docs.github.com/en/enterprise-cloud@latest/repositories/creating-and-managing-repositories/about-repositories#about-repository-visibility">[1]</a><a href="https://docs.github.com/en/enterprise-cloud@latest/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/setting-repository-visibility">[2]</a></li>
  <li>We recommend that regular collaborators work from a single repository to streamline collaboration, creating pull requests between branches instead of between repositories. Forking is best suited for accepting contributions from people who are unaffiliated with a project, such as open-source contributors.<a href="https://docs.github.com/en/repositories/creating-and-managing-repositories/best-practices-for-repositories">[1]</a></li>
</ul>


<br />
<hr>
<br />
<h2 id="d3">Collaboration Features</h2>

<h3>Issues</h3>

<ul>
  <li>Issues can be used to plan, discuss, and track work. Issues can track bug reports, new features and ideas, and anything else you need to write down or discuss with your team. You can also break your work down further by adding sub-issues and easily browse the full hierarchy of work to be done. <a href="https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues#stay-up-to-date">[1]</a></li>
  <li>You can classify issues, pull requests, and discussions by creating, editing, applying, and deleting labels. <a href="https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/managing-labels">[1]</a></li>
  <li>You can create a branch to work on an issue directly from the issue page and get started right away <a href="https://docs.github.com/en/issues/tracking-your-work-with-issues/creating-a-branch-for-an-issue">[1]</a></li>
  <li>You can configure your project's built-in workflows to automatically archive items that match a filter <a href="https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/archiving-items-automatically">[1]</a></li>
  <li>Projects is an adaptable, flexible tool for planning and tracking work on GitHub. <a href="https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects"><[1]</a></li>
  <li>Best Practices: Break down large issues into smaller issues, communicate, Make use of the description, README, and status updates, use views, Have a single source of truth, use automation, Use different field types, <a href="https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/best-practices-for-projects">[1]</a></li>
  <li>You can assign multiple people to each issue or pull request. A paid account can have up to 10 people assigned. Private repositories on the free plan are limited to one person per issue or pull request. <a href="https://docs.github.com/en/issues/tracking-your-work-with-issues/assigning-issues-and-pull-requests-to-other-github-users">[1]</a></li>
  <li>You can link a pull request or branch to an issue to show that a fix is in progress and to automatically close the issue when the pull request or branch is merged. <a href="https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue">[1]</a></li>
  <li><a href="https://docs.github.com/en/account-and-profile/managing-subscriptions-and-notifications-on-github/viewing-and-triaging-notifications/customizing-a-workflow-for-triaging-your-notifications#checking-your-highest-notification-priorities">Checking your highest notification priorities</a>:
    <ul>
      <li>Pull requests where your review is requested: reason:review-requested</li>
      <li>Events where your username is @mentioned: reason:mention</li>
      <li>Events where a team you're a member of is @mentioned: reason:team-mention</li>
      <li>CI workflow failures for a specific repository: reason:ci-activity and repo:owner/repo-name</li>
    </ul>
  </li>
  <li>GitHub users with at least read access, including those without write access, can create an issue. GitHub allows any user, regardless of their level of access or affiliation, to create issues on a repository. This inclusivity supports open collaboration and contribution.<a href="https://docs.github.com/en/issues/tracking-your-work-with-issues/creating-an-issue">[1]</a></li>
  <li>Discussions are used for general conversations and collaboration, while issues are specific items that need attention, such as bugs or feature requests. <a href="https://foundations.projectpythia.org/foundations/github/github-issues.html#">[1]</a></li>
  <li>issue templates merely provide text that contributors can remove and replace with their own input, but a form enables you to build structured forms with required fields and easy-to-follow steps to ensure you don't miss important details<a href="https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms">[1]</a></li>
</ul>


<h3>Pull requests</h3>

<ul>
  <li><a href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request">Create a pull request to propose and collaborate on changes to a repository. These changes are proposed in a branch, which ensures that the default branch only contains finished and approved work</a></li>
  <li><a href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-branches">Use a branch to isolate development work without affecting other branches in the repository. Each repository has one default branch, and can have multiple other branches. You can merge a branch into another branch using a pull request.</a></li>
  <li><a href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/reviewing-proposed-changes-in-a-pull-request">In a pull request, you can review and discuss commits, changed files, and the differences (or "diff") between the files in the base and compare branches</a></li>
  <li><a href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/about-forks">A fork is a new repository that shares code and visibility settings with the original “upstream” repository.</a></li>
  <li>The "Files changed" tab in a pull request on GitHub displays the proposed changes as they would appear post-merge. Additions are shown in green and prefixed by a + sign, while removals are displayed in red and prefixed by a - sign. <a href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-comparing-branches-in-pull-requests">[1]</a></li>
</ul>


<h3>Discussions</h3>

<ul>
  <li>GitHub Discussions is a collaborative communication forum for the community around an open source or internal project<a href="https://docs.github.com/en/discussions/quickstart">[1]</a></li>
  <li>You can pin a discussion above the list of discussions for the repository or organization or to a specific category. The globally pinned discussions will be shown in addition to the discussions pinned to a specific category.<a href="https://docs.github.com/en/discussions/managing-discussions-for-your-community/managing-discussions#pinning-a-discussion">[1]</a></li>
</ul>


<h3>Notifications</h3>

<ul>
  <li>Notifications provide updates about the activity on GitHub that you've subscribed to. You can use the notifications inbox to customize, triage, and manage your updates<a href="https://docs.github.com/en/account-and-profile/managing-subscriptions-and-notifications-on-github/setting-up-notifications/about-notifications">[1]</a></li>
</ul>


<h3>Gists, Wikis, and GitHub Pages</h3>

<ul>
  <li><b>Gists</b> provide a simple way to share code snippets with others. Every gist is a Git repository. If you are signed in to GitHub when you create a gist, the gist will be associated with your account. Gists can be public or secret. you can fork or clone any gist, even if you aren't the original author. You can also view a gist's full commit history, including diffs<a href="https://docs.github.com/en/get-started/writing-on-github/editing-and-sharing-content-with-gists/creating-gists">[1]</a><a href="https://docs.github.com/en/get-started/writing-on-github/editing-and-sharing-content-with-gists/forking-and-cloning-gists">[2]</a></li>
  <li><b>Wikis</b>: Every repository on GitHub comes equipped with a section for hosting documentation, called a wiki.<a href="https://docs.github.com/en/communities/documenting-your-project-with-wikis/about-wikis">[1]</a> </li>
  <li><b>Github Pages</b>: You can use GitHub Pages to showcase some open source projects, host a blog, or even share your résumé <a href="https://docs.github.com/en/pages/quickstart">[1]</a></li>
  <li>To create a new Gist, you should go to the Gist homepage. This is the dedicated space for managing and creating Gists on GitHub.<a href="https://docs.github.com/en/get-started/writing-on-github/editing-and-sharing-content-with-gists/creating-gists">[1]</a></li>
</ul>


<br />
<hr>
<br />
<h2 id="d4">Modern Development</h2>

<ul>
  <li><b>Actions</b>:
    <ul>
      <li>GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline. You can create workflows that build and test every pull request to your repository, or deploy merged pull requests to production<a href="https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions">[1]</a><a href="https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions">[2]</a></li>
      <li>Workflows can be reused<a href="https://docs.github.com/en/actions/using-workflows/reusing-workflows#access-to-reusable-workflows">[1]</a></li>
      <li>Events that trigger workflows: PR, push, open an issue<a href="https://docs.github.com/en/actions/about-github-actions/understanding-github-actions">[1]</a><a href="https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows#about-events-that-trigger-workflows">[2]</a></li>
    </ul>
  </li>
  <li><a href="https://docs.github.com/en/apps/github-marketplace/github-marketplace-overview/about-github-marketplace-for-apps">Marketplace</a>:
    <ul>
      <li>GitHub Marketplace connects you to developers who want to extend and improve their GitHub workflows. You can list free and paid tools for developers to use in GitHub Marketplace. GitHub Marketplace offers developers two types of tools: GitHub Actions and Apps, and each tool requires different steps for adding it to GitHub Marketplace.</li>
      <li>GitHub Marketplace is a central location for finding actions created by the GitHub community. You can search and browse actions directly in your repository's workflow editor. From the sidebar, you can search for a specific action, view featured actions, and browse featured categories. You can also view the number of stars an action has received from the GitHub community.<a href="https://docs.github.com/en/actions/learn-github-actions/finding-and-customizing-actions">[1]</a>
    </ul>
  </li>
  <li><a href="https://docs.github.com/en/copilot/overview-of-github-copilot/about-github-copilot-individual">Copilot</a>: 
    <ul>
      <li>GitHub Copilot is an AI coding assistant that helps you write code faster and with less effort, allowing you to focus more energy on problem solving and collaboration</li>
      <li>Implementing Copilot Business for users allows the organization to configure the service to meet company-wide policies and exclude specific files from being evaluated. <a href="https://docs.github.com/en/copilot/about-github-copilot/what-is-github-copilot">[1]</a></li>
      <li>It is trained on all languages that appear in public repositories. For each language, the quality of suggestions you receive may depend on the volume and diversity of training data for that language. Languages with less representation in public repositories may produce fewer or less robust suggestions.<a href="https://docs.github.com/en/copilot/about-github-copilot/what-is-github-copilot">[1]</a></li>
    </ul>
  </li>
  <li><a href="https://docs.github.com/en/codespaces/overview">Codespace</a>:
    <ul>
      <li>A codespace is a development environment that's hosted in the cloud. Each codespace you create is hosted by GitHub in a Docker container, running on a virtual machine.</li>
      <li>You can connect to your codespaces from your browser, from Visual Studio Code, from the JetBrains Gateway application, or by using GitHub CLI. When you connect, you are placed within the Docker container. You have limited access to the outer Linux virtual machine host.</li>
      <li>Inactive codespaces are automatically deleted. You can choose how long your stopped codespaces are retained, up to a maximum of 30 days. However, because GitHub Codespaces incurs storage charges, you may prefer to reduce the retention period by changing your default period in your personal settings for GitHub Codespaces.<a href="https://docs.github.com/en/codespaces/setting-your-user-preferences/configuring-automatic-deletion-of-your-codespaces">[1]</a></li>
      <li>You can store sensitive information, (tokens, service principals, credentials), that you want to access in your codespaces via environment variables. You can add development environment secrets to your personal account that you want to use in your codespaces<a href="https://docs.github.com/en/codespaces/managing-your-codespaces/managing-your-account-specific-secrets-for-github-codespaces">[1]</a></li>
    </ul>
  </li>
</ul>


<br />
<hr>
<br />
<h2 id="d5">Project Management</h2>

<ul>
  <li>The roadmap layout provides a high-level visualization of your project across a configurable timespan, and allows you to drag items to affect their start and target dates or selected iteration. <a href="https://docs.github.com/en/issues/planning-and-tracking-with-projects/customizing-views-in-your-project/changing-the-layout-of-a-view#about-the-roadmap-layout">[1]</a></li>
  <li>Projects is designed to integrate with external tools and services. This provides more options to customize the project boards and workflows for issues, pull requests, and much more. <a href="https://docs.github.com/en/issues/organizing-your-work-with-project-boards/managing-project-boards/about-project-boards">[1]</a><a href="https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects">[2]</a></li>
  <li>Projects (classic) on GitHub help you organize and prioritize your work. You can create projects (classic) for specific feature work, comprehensive roadmaps, or even release checklists. With projects (classic), you have the flexibility to create customized workflows that suit your needs. <a href="https://docs.github.com/en/issues/organizing-your-work-with-project-boards/managing-project-boards/about-project-boards">[1]</a><a href="https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects">[2]</a></li>
  <li><a href="https://docs.github.com/en/issues/planning-and-tracking-with-projects/viewing-insights-from-your-project/about-insights-for-projects">Using insights to create chart</a>:
    <ul>
      <li><b>current chart</b>: visualize the current status of items assigned to each team member in real-time</li>
      <li><b>user chart</b>: displays information related to individual users, such as their activity or contributions, rather than the distribution of assigned items among team members.</li>
      <li><b>historical chart</b>: it focuses on visualizing data over a period of time in the past</li>
      <li><b>project chart</b>: typically provides an overview of the project's progress, milestones, or tasks, rather than focusing on individual team members' assignments.</li>
    </ul>
  </li>
  <li>Information is synced automatically to your project as you make changes, updating your views and charts. When you change information about a pull request or issue in your project, the pull request or issue reflects that information.<a href="https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects">[1]</a><a href="https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/about-milestones">[2]</a></li>
  <li>Milestones in GitHub are designed for grouping and tracking related issues, making it efficient for tracking and reporting purposes.<a href="https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/creating-and-editing-milestones-for-issues-and-pull-requests">[1]</a></li>
  <li>You can assign multiple people to each issue or pull request, including yourself, anyone who has commented on the issue or pull request, anyone with write permissions to the repository, and organization members with read permissions to the repository. Anyone with write access to a repository can assign issues and pull requests.<a href="https://docs.github.com/en/issues/tracking-your-work-with-issues/assigning-issues-and-pull-requests-to-other-github-users"></a></li>
  <li>GitHub Save Replies allows you to save and reuse responses <a href="https://docs.github.com/en/get-started/writing-on-github/working-with-saved-replies/creating-a-saved-reply">[1]</a></li>
  <li>Labels on GitHub can be used to categorize and filter issues or pull requests based on their characteristics, such as priority, type, status, or any custom criteria. This helps in organizing and prioritizing tasks, making it easier for team members to identify and work on specific items efficiently.<a href="https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/managing-labels">[1]</a></li>
  <li>You can view your project as a high-density table, as a kanban board, or as a timeline-style roadmap. While changing the layout of a GitHub project, there are Table layout, board layout, or roadmap layout are the only three layouts that GitHub Projects provides.<a href="https://docs.github.com/en/issues/planning-and-tracking-with-projects/customizing-views-in-your-project/changing-the-layout-of-a-view">[1]</a></li>
  <li>You can either create an organization project or a user project. To create an organization project, you need a GitHub organization<a href="https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/quickstart-for-projects">[1]</a></li>
</ul>


<br />
<hr>
<br />
<h2 id="d6">Privacy, Security, and Administration</h2>

<ul>
  <li><a href="https://docs.github.com/en/enterprise-cloud@latest/admin/identity-and-access-management/understanding-iam-for-enterprises/about-identity-and-access-management">Administrators must decide how users will access the enterprise's resources on GitHub.</a></li>
  <li><a href="https://docs.github.com/en/enterprise-cloud@latest/admin/identity-and-access-management/understanding-iam-for-enterprises/about-saml-for-enterprise-iam">You can use SAML single sign-on (SSO) to centrally manage access to organizations owned by your enterprise on GitHub.com.</a></li>
  <li><a href="https://docs.github.com/en/enterprise-cloud@latest/admin/identity-and-access-management/understanding-iam-for-enterprises/about-enterprise-managed-users">Learn how your enterprise can manage the lifecycle and authentication of users on GitHub from your identity provider (IdP)</a></li>
  <li><a href="https://docs.github.com/en/code-security/getting-started/github-security-features">GitHub's security features help keep your code and secrets secure in repositories and across organizations.</a></li>
  <li><a href="https://docs.github.com/en/get-started/learning-about-github/access-permissions-on-github">With roles, you can control who has access to your accounts and resources and the level of access each person has</a></li>
  <li><a href="https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-user-account-settings/permission-levels-for-a-personal-account-repository">A repository owned by a personal account has two permission levels: the repository owner and collaborators</a></li>
  <li>Within GitHub repositories you can disable:  wikis, sponsorship, issues, discussions, actions <a href="https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository">[1]</a><a href="https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository">[2]</a><a href="https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/disabling-projects-in-a-repository">[3]</a></li>
  <li>GitHub makes extra security features available to customers under an Advanced Security license (GHAS): Code scanning, Secret scanning, Dependency review <a href="https://docs.github.com/en/get-started/learning-about-github/about-github-advanced-security">[1]</a></li>
  <li>You can give organization members, outside collaborators, and teams of people different levels of access to repositories owned by an organization by assigning them to roles.<a href="https://docs.github.com/en/organizations/managing-user-access-to-your-organizations-repositories/managing-repository-roles/repository-roles-for-an-organization">[1]</a></li>
  <li>GitHub offers security features that help keep data secure in repositories and across organizations. The security tab of a GitHub repository provides information on security policies, dependency alerts, security advisories, and vulnerability scans including details about identified security vulnerabilities in the repository's code. <a href="https://docs.github.com/en/code-security/getting-started/github-security-features">[1]</a></li>
  <li>GitHub Enterprise Cloud administrators can allow people to use a personal account on GitHub.com to access your enterprise's resources and optionally configure additional SAML access restriction, or can provision and control enterprise accounts using your identity provider (IdP) with Enterprise Managed Users.<a href="https://docs.github.com/en/enterprise-cloud@latest/admin/identity-and-access-management/understanding-iam-for-enterprises/about-identity-and-access-management">[1]</a></li>
  <li>You can configure two-factor authentication (2FA) using a TOTP app on mobile or desktop or via text message. After you have configured 2FA using a TOTP app or via text message, you can add security keys as an alternate 2FA method.<a href="https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication">[1]</a></li>
  <li>If you lose access to your two-factor authentication credentials, you can use your recovery codes, or another recovery option, to regain access to your account.  Using recovery codes provides the ability to automatically regain entry into your account.<a href="https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/recovering-your-account-if-you-lose-your-2fa-credentials#using-a-two-factor-authentication-recovery-code">[1]</a></li>
  <li>Internal visibility for a repository: You can use internal repositories to practice "innersource" within your enterprise. Members of your enterprise can collaborate using open source methodologies without sharing proprietary information publicly.  You can only create internal repositories if you use GitHub Enterprise Cloud with an enterprise account. An enterprise account is a separate type of account that allows a central point of management for multiple organizations.<a href="https://docs.github.com/en/enterprise-cloud@latest/repositories/creating-and-managing-repositories/about-repositories#about-internal-repositories">[1]</a></li>
  <li>Branch protection is used to prevent accidental or unauthorized changes to branches by setting restrictions on who can push or merge changes to the branch. This helps maintain the integrity of the codebase and ensures that only approved changes are made to critical branches. protection rules, which define whether collaborators can delete or force push to the branch and set requirements for any pushes to the branch <a href="https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches">[1]</a><a href="https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/managing-a-branch-protection-rule">[2]</a></li>
  <li>Manage collaborators by repository setting<a href="https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/managing-teams-and-people-with-access-to-your-repository">[1]</a></li>
  <li>An organization's news feed shows other people's activity on repositories owned by that organization<a href="https://docs.github.com/en/enterprise-server/organizations/collaborating-with-groups-in-organizations/about-your-organizations-news-feed">[1]</a></li>
  <li>Billing managers can: Upgrade or downgrade the account; Add, update, or remove payment methods; View payment history; Download receipts; View, invite, and remove billing managers; Start, modify, or cancel sponsorships; In addition, all billing managers will receive billing receipts by email on the organization's billing date<a href="https://docs.github.com/en/organizations/managing-peoples-access-to-your-organization-with-roles/adding-a-billing-manager-to-your-organization#permissions-for-billing-managers">[1]</a></li>
</ul>


<br />
<hr>
<br />
<h2 id="d7">Benefits of the GitHub Community</h2>

<ul>
  <li><a href="https://learn.microsoft.com/en-us/training/modules/contribute-open-source/2-identify">Contribution</a></li>
  <li><a href="https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates">Issue and pull request templates</a></li>
  <li><a href="https://github.com/orgs/community/discussions">Community Discussion</a></li>
  <li><a href="https://docs.github.com/en/discussions/managing-discussions-for-your-community/moderating-discussions#marking-a-comment-as-an-answer">You can mark a comment in the discussion as an answer to the discussion if a discussion is within a category that accepts answers.</a></li>
  <li><a href="https://docs.github.com/en/get-started/quickstart/be-social#following-people">Following people</a></li>
  <li><a href="https://docs.github.com/en/account-and-profile/managing-subscriptions-and-notifications-on-github/viewing-and-triaging-notifications/managing-notifications-from-your-inbox">Use your inbox to quickly triage and sync your notifications across email and mobile</a></li>
  <li>GitHub doesn't enforce legal compliance for open-source projects. it provides features like license templates <a href="https://github.com/resources/whitepapers/how-github-secures-open-source-software">[2]</a></li> 
  <li>When you follow organizations on GitHub, you'll see their public activity on your personal dashboard. This activity includes new discussions, sponsorships, and repositories.<a href="https://docs.github.com/en/get-started/exploring-projects-on-github/following-organizations">[1]</a></li>
  <li>Open-source software development is based on principles of open communication, collaborative contribution from a diverse community, and the distribution of software that is accessible to everyone. These principles promote transparency and inclusivity<a href="https://resources.github.com/open-source/what-is-open-source-software/">[1]</a></li>
  <li>To make your pull request template visible in the repository's root directory, name the pull request template pull_request_template.md.<a href="https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository">[1]</a></li>
  <li>A fork is a new repository that shares code and visibility settings with the original upstream code repository. Forks are often used to iterate on ideas or changes before they are proposed back to the upstream repository, such as in open source projects or when a user does not have write access to the upstream repository.  Developers can use forks to propose changes related to fixing a bug without impacting the original upstream repository.<a href="https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo">[1]</a></li>
  <li>Issue templates are helpful when you want to provide guidance for opening issues while allowing contributors to specify the content of their issues. If you want contributors to provide specific, structured information when they open issues, issue forms help ensure that you receive your desired information<a href="https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates#issue-templates">[1]</a></li>
</ul>



<br />
<hr>
<br />
<h3>References</h3>
<ul>
  <li><a href="https://docs.github.com/en/get-started/showcase-your-expertise-with-github-certifications/about-github-certifications">About GitHub Certifications</a></li>
  <li><a href="https://assets.ctfassets.net/wfutmusr1t3h/1kmMx7AwI4qH8yIZgOmQlP/79e6ff1dfdee589d84a24dd763b1eef7/github-foundations-exam-study-guide__1_.pdf">Study Guide</a></li>
  <li><a href="https://www.udemy.com/course/github-foundations-certification/?srsltid=AfmBOopCCmdWaYhRMlgIymrfOd-DnSB68CuFWDZrtTrmclDl1i4LodBM&couponCode=CP130525">Udemy: NEW - GitHub Foundations Certification - Practice Exams 2025
</a></li>
<li><a href="https://www.udemy.com/course/github-ultimate/?srsltid=AfmBOopO7KO66lRt82xtU6bfnPvSnWdAk-rhXBKPpGtBedhPnObDlQOp">Udemy: GitHub Ultimate: Master Git and GitHub - Beginner to Expert
</a></li>
</ul>  
