---
layout: post
title:  "GitHub Copilot"
date:   2025-05-27
categories: infra
permalink: /:categories/github-copilot
---

<p>Hare are some notes about GitHub Copilot. The concepts were extracted from documentation and Udemy training.</p>

<center><img src="/img/git/github-copilot.png" height="30%" width="30%"/></center> 

<h2>Definition</h2>

<p style="text-align: justify;"><em>GitHub Copilot is an AI coding assistant that helps you write code faster and with less effort, allowing you to focus more energy on problem solving and collaboration</em><a href="https://docs.github.com/en/copilot/about-github-copilot/what-is-github-copilot">[What is]</a><a href="https://docs.github.com/en/copilot/quickstart">[QuickStart]</a><a href=" https://github.com/copilot">[Immersive view]</a></p>

<h2>Machine Learn</h2>

<ul>
  <li>Supervised: input label - e.g algorithm: classification, Regression</li>
  <li>Unsupervised: without input label - e.g. algorithm: clustering</li>
  <li>Reinforced: feedback - e.g. algorithm: Decision making</li>
  <li>Process: input text -> tokenization([create, a, file]) -> embedding generation (each token is converted into a vector embbedings) -> model processing</li>
</ul>

<h2>Characteristics</h2>

<ul>
  <li>Probabilistic: may generate different outputs for the same input</li>
  <li>Coding related questions</li> 
  <li>Primary English</li>
  <li>Uses OpenAI’s Codex model</li>
  <li>Can generate source code, documentation, git ignore, commit messages, unit test</li>
  <li>It is available in IDE, GH Mobile, command line and Github.com (only Enterprise)</li>
</ul>

<h2>Features <a href="https://docs.github.com/en/copilot/about-github-copilot/what-is-github-copilot#copilot-features">[1]</a><a href="https://docs.github.com/en/copilot/about-github-copilot/github-copilot-features">[2]</a></h2>

<ul>
  <li>Code suggestions</li>
  <li><a href="https://docs.github.com/en/copilot/responsible-use-of-github-copilot-features/responsible-use-of-github-copilot-code-review">Code Review</a></li>
  <li>Understand the context of the code</li>
  <li>Multi language support</li>
  <li>Inteligent debugging</li>
  <li>Code refactoring</li>
  <li>Security assistence</li>
  <li>Writing documentation</li>
  <li>Autocomple</li>
  <li>Automate the creation of projects and related directories</li>
  <li>Chat</li>
  <li>Support in the <a href="https://docs.github.com/en/copilot/responsible-use-of-github-copilot-features/responsible-use-of-github-copilot-in-the-cli">CLI</a>
    <ul> 
      <li>Generate shell commands by describing intent in plain language</li>
      <li>Suggesting shell commands based on natural language input, helping with syntax and automating repetitive tasks</li>
      <li>Install GitHub CLI (gh)
        <ol>
          <li>Authenticate with 'gh auth login'</li>
          <li>Run 'gh extension install github/gh-copilot'</li>
          <li>'gh extension install github/copilot-cli' (integrates Copilot CLI into the GitHub CLI ecosystem)</li>
          <li>Test if is correctly installed: 'gh extension list'</li>
        </ol>
      </li>
    </ul>
  </li>
  <li>AI-generated <a href="https://docs.github.com/en/copilot/responsible-use-of-github-copilot-features/responsible-use-of-github-copilot-pull-request-summaries">PR summaries</a> (only for Enterprise). It analyzes the diff of the code changes, the commit history, and comments</li>
  <li><a href="https://docs.github.com/en/copilot/using-github-copilot/guides-on-using-github-copilot/refactoring-code-with-github-copilot">Refactor</a>, <a href="https://docs.github.com/en/copilot/using-github-copilot/guides-on-using-github-copilot/using-copilot-to-migrate-a-project">migrate a project</a>, <a href="https://docs.github.com/en/copilot/using-github-copilot/guides-on-using-github-copilot/writing-tests-with-github-copilot">write tests</a>, <a href="https://docs.github.com/en/copilot/using-github-copilot/guides-on-using-github-copilot/modernizing-legacy-code-with-github-copilot">modernize legacy code</a>, <a href="https://docs.github.com/en/copilot/using-github-copilot/guides-on-using-github-copilot/upgrading-java-projects-with-github-copilot">upgrading java projects</a>, <a href="https://docs.github.com/en/copilot/using-github-copilot/guides-on-using-github-copilot/choosing-the-right-ai-tool-for-your-task">Choosing the right AI tool for your task</a></li>
</ul>

<h2>Training</h2>

<ul>
  <li>It is trained on all languages that appear in public repositories (including open-source repositories). The quality of suggestions depends on the volume and diversity of training data for each language</li>
  <li>Largin training Dataset in public repo > Neural Network Arch based on transformer in unsupervised leraning (learned pattern and struture without label) > use Supervised learn for during fine tuning process (learn from examples helps to understand the context and improve the accuracy) > outcome: Codex model (descendent of GptTree; based on transformer archtecture)</li>
  <li>GitHub Copilot’s model is trained on a static dataset that includes publicly available code and is not updated in real-time. The suggestions may be outdated because of some old or deprecated code</li>
  <li>Proprietary code from private repositories is explicitly excluded from GitHub Copilot’s training dataset to protect user privacy and ensure compliance with ethical standards. </li>
</ul>

<h2>How it works</h2>

<ul>
  <li>Transmits the code and its surrounding context to a large language model (e.g. Codex), which is hosted remotely (cloud-based models)</li>
  <li>Only the code currently working on ( and metadata), such as a few lines or function definitions, is sent to OpenAI’s servers for processing. The model generates suggestions based on the context actively edited, without needing access the entire project or any other unrelated data</li>
  <li>(1) The request is sent to GitHub Copilot's servers (anonymized, encrypted data), (2) forwarded to a proxy server that pre-processes the data (such as context and completion suggestions). The proxy filters user inputs, removing sensitive or personally identifiable information before sending the data to the cloud-based model, which means the suggestions are based on a sanitized version of the data, without leaking private code or sensitive data. (3) Then pass to the model. Once the model generates a suggestion, (4) it undergoes post-processing through the proxy server before being (5) sent back to your IDE</li>
  <li>It sends small snippets of code (a few lines around the cursor) to GitHub’s servers, where an AI model processes the data and generates relevant code completions. These snippets are temporarily processed to provide real-time suggestions</li>
  <li>No user-specific data is stored or logged persistently. The processing is done in memory and the data is discarded once the suggestions are generated</li>
  <li>Duplication: 
    <ul>
      <li>GitHub Copilot is designed to avoid suggesting code that matches more than 150 characters from any single block in publicly available repositories</li>
      <li>The duplication detector filter compares generated code suggestions against a database of popular, open-source repositories and flags suggestions if a certain similarity threshold is met.</li>
      <li>The duplication filter prevents Copilot from suggesting exact matches to publicly available code, ensuring that its suggestions are not direct copies of existing repositories. However, it does not completely eliminate similar code from being suggested.</li>
    </ul>
  </li>      
  <li>Telemetry:
    <ul>
      <li>GitHub Copilot collects anonymized telemetry data, which may be shared with Microsoft and GitHub to improve services.</li>
      <li>Telemetry data may be collected, and snippets of user code can be logged for debugging purposes</li>
      <li>Telemetry collection from Copilot can offer insights into how much time is saved, how often suggestions are accepted, and even areas where Copilot may not be helpful</li>
      <li>The GitHub Productivity API allows teams to track how frequently developers accept Copilot’s suggestions</li>
    </ul>
  </li>
  <li>Since Copilot is trained on vast datasets of publicly available code, it tends to generate widely used, conventional coding patterns. This makes it useful for common programming tasks but less innovative for highly specific, custom, or domain-specific solutions. Developers may need to modify or refine the suggestions to better fit unique use cases.</li>
  <li>Regularly reviewing AI-generated code for bias is a critical step in responsible AI use </li>
  <li>Using Copilot in private mode limits the scope of suggestions and reduces the risk of sensitive data leakage. Excluding sensitive files from Copilot’s context is a safeguard that ensures Copilot doesn’t suggest code based on sensitive internal data. This is a best practice for maintaining privacy while still using Copilot's benefits.</li>
  <li>GitHub Copilot generates suggestions from a model trained on publicly available code, which uses pattern recognition and natural language processing (NLP) to match your input to relevant code. It uses natural language processing (NLP) and pattern recognition techniques to identify relevant code based on the context of the user's current input, generating suggestions that match the programming style and libraries in use.</li>
  <li>GitHub Copilot uses a limited context window to process a portion of the code at a time. The suggestions are based on the code within this window, which means that in longer files or complex codebases, suggestions may not fully reflect the overall structure or intent of the project because parts of the code fall outside the context window.</li>
  <li>Pressing Ctrl+Space manually requests GitHub Copilot to generate code suggestions in supported IDEs like Visual Studio Code. This works in scenarios where Copilot does not auto-suggest completions but the user still wants assistance.</li>          
  <li>GitHub Copilot Chat prioritizes inline comments and existing code context when generating responses</li>
  <li>GitHub Copilot provides multiple code suggestions when invoked via the appropriate keyboard shortcut (e.g., pressing Ctrl+Enter or Alt+] in some IDEs)</li>
</ul> 

<h2>Chat</h2>

<ul>
  <li>Inputs are sent directly to OpenAI’s Codex API for processing</li>
  <li>You can select the AI models<a href="https://docs.github.com/en/copilot/using-github-copilot/ai-models/choosing-the-right-ai-model-for-your-task">[1]</a></li>
  <li>Coding-related questions, explanations for code snippets, debugging help, and real-time code suggestions based on current coding environment <a href="https://docs.github.com/en/copilot/using-github-copilot/copilot-chat/getting-started-with-prompts-for-copilot-chat">[1]</a></li>
  <li>Prompt engineering: Start general, then get specific; give examples; Break complex tasks into simpler tasks; Avoid ambiguity; Indicate relevant code; Experiment and iterate; Keep history relevant; Follow good coding practices <a href="https://docs.github.com/en/copilot/using-github-copilot/copilot-chat/prompt-engineering-for-copilot-chat">[1]</a></li>
  <li>Very effective for helping developers understand unfamiliar code by explaining its functionality, dependencies, and usage</li>
  <li>Includes built-in feedback mechanisms (rate by clicking thumbs-up or thumbs-down buttons) </li>
  <li>Feedback about GitHub Copilot Chat is through the in-editor feedback button, which allows users to send context-specific feedback while using Copilot</li>
  <li>Builds a prompt by extracting relevant portions of the currently open file, taking into account the user’s cursor position, function signatures, surrounding comments, and contextual code </li>
  <li>it cannot execute code directly within the chat interface</li>
  <li>The <a href="https://docs.github.com/en/copilot/using-github-copilot/copilot-chat/asking-github-copilot-questions-in-github-mobile">mobile has the chat feature</a>, but with some limitations of quality</li>
  <li>Edit mode is use for more granular control: choose files to let Copilot make changes<a href="https://docs.github.com/en/copilot/using-github-copilot/guides-on-using-github-copilot/choosing-the-right-ai-tool-for-your-task#using-copilot-chat-in-edit-mode">[1]</a></li>
  <li>Chat for debbuging:  developer describe issues in natural language, and based on the context of the surrounding code, it provides suggestions for how to address potential bugs</li>
  <li>Improve GitHub response relevance and performance in large codebases limiting the number of open files or tabs in the editor</li>
  <li>GitHub Copilot Chat is available for both public and private repositories for individual and enterprise plans, with the necessary permissions. </li>
</ul>

<h2>Agent <a href="https://docs.github.com/en/copilot/responsible-use-of-github-copilot-features/responsible-use-of-copilot-coding-agent-on-githubcom">[1]</a></h2>

<ul>
  <li>Copilot can work like a developer: fix bugs, implement features, create PR, etc  <a href="https://docs.github.com/en/copilot/using-github-copilot/using-copilot-coding-agent-to-work-on-tasks/about-assigning-tasks-to-copilot">[1]</a></li>
</ul>

<h2>Subscription <a href="https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/getting-started-with-copilot-on-your-personal-account/getting-started-with-a-copilot-plan">[1]</a><a href="https://docs.github.com/en/copilot/about-github-copilot/plans-for-github-copilot">[2]</a></h2>

<ul>
  <li>Non-GitHub users can access GitHub Copilot through Microsoft Visual Studio and Visual Studio Code if they have an Azure subscription</li>
  <li>GitHub Copilot requires users to have a GitHub account for authentication and subscription purposes. However, it does not require users to host their repositories on GitHub</li>
  <li><a href="https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/getting-started-with-copilot-on-your-personal-account/about-individual-copilot-plans-and-benefits#github-copilot-free">Free</a>: code completion (2k line/month), chat (50/month), block suggestion, access to Claude Sonnet and ChatGPT model</li>
  <li><a href="https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/getting-started-with-copilot-on-your-personal-account/about-individual-copilot-plans-and-benefits#github-copilot-pro">Pro</a>: code completion [no limit], chat[no limit], chat in GH Mobile</li>
  <li><a href="https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/getting-started-with-copilot-on-your-personal-account/about-individual-copilot-plans-and-benefits#github-copilot-pro-1">Pro+</a>: PRO + Full access to all available models in Copilot Chat; Up to 1,500 premium requests per month; Priority access to advanced AI capabilities</li>
  <li><a href="https://docs.github.com/en/copilot/managing-copilot/managing-github-copilot-in-your-organization/managing-the-copilot-plan-for-your-organization/subscribing-to-copilot-for-your-organization">Business</a>: 
    <ul>
      <li>All previous + file exclusion, organization wide policy, audit logs, support for public and private repositories, manage policies at the enterprise or organization level</li>
      <li>Enables admin-level control, telemetry for auditing, and organization-wide enforcement of code matching filters, which scan for snippets that closely match public GitHub content—crucial for enterprise risk mitigation</li>
      <li>Allows the organization to configure the service to meet company-wide policies and exclude specific files from being evaluated</li>
      <li>Orgaization-wide policies like disable suggestions matching public code</li>
      <li>Designed for organizations that need data privacy and security features</li>
      <li>Enterprise-grade security practices, including end-to-end encryption of data in transit and at rest</li>
      <li>GitHub Copilot Business is designed with enterprise clients in mind, offering key security and compliance features such as SOC 2 Type 2 and GDPR compliance</li>
      <li>It has the ability to restrict AI-generated code suggestions based on organization policies</li>
      <li>Provides an IP (intellectual property) indemnity clause that covers claims against the generated code in certain scenarios</li>
      <li>SSO integration</li>
      <li>Private code generation</li>
      <li>Vulnerability scanning</li>
      <li>The "block matching public code" feature to support copyright or licensing risks. Copilot does not generate code suggestions that match public repositories</li>
      <li>REST API:
        <ul>
          <li>Automate the management of subscriptions using GitHub’s REST API to list, add, and remove GitHub Copilot seats for users in organization</li>
          <li>Manage users and assign Copilot seats, it is not role-based</li>
          <li>Endpoint to manage subscription for a user in an organization: POST /orgs/{org}/copilot/seats</li>
          <li>Remove a user: the administrator must call the /orgs/{org}/copilot/billing/seats/{username} endpoint with a DELETE request.</li>    
          <li>The admin can get the list of subscription by the endpoint GET /orgs/{org}/copilot/subscriptions using the API token scope as admin:org. OAuth2 token is necessary to provide the required authentication for organizational access</li>
        </ul>
      </li>
    </ul>
  </li>
  <li><a href="https://docs.github.com/en/enterprise-cloud@latest/copilot/managing-copilot/managing-copilot-for-your-enterprise/managing-the-copilot-plan-for-your-enterprise/subscribing-to-copilot-for-your-enterprise">Enterprise</a>: 
    <ul>
      <li>All the Business + Copilot Knowladge bases (improve accuracy), fine tuning a custom LLM</li>
      <li>Knowladge base:  dedicated repository that holds all the relevant documentation, code, and libraries; make the contents available for enhanced coding suggestions, ensuring that organization-specific practices are reflected in Copilot’s output. The most useful types of knowledge are stored: code snippets, standardized functions, and reusable components from internal repositories </li>
      <li>Provides the ability to <a href="https://docs.github.com/en/enterprise-cloud@latest/admin/copilot-business-only/about-enterprise-accounts-for-copilot-business">manage licenses</a> and users at scale</li>
      <li>Centralized administrative controls (license management, security policies, billing)</li>
      <li>Analyzes commit messages, file changes, and project context to generate a concise pull request summary</li>
      <li>Best option for large organizations with strict privacy and security concerns</li>
      <li>It includes advanced privacy controls, like the ability to configure context exclusions, enforce corporate policy integration, and ensure that sensitive codebases are handled securely. Also allows admins configure policies at the organization level to specify which repositories are enabled for Copilot</li>
      <li>GitHub Copilot Enterprise includes features like enhanced telemetry and more granular data retention policies. Telemetry data allows to monitor usage while complying with internal security policies</li>
    </ul>
  </li>
</ul>

<h2>Access</h2>

<ul>
  <li><a href="https://docs.github.com/en/copilot/overview-of-github-copilot/about-github-copilot-individual">GitHub Copilot Individual</a> is designed for single-user environments and does not include team management features like access control. It is  a member of an Organization with subscription.</li>
  <li><a href="https://docs.github.com/en/copilot/managing-copilot/managing-copilot-as-an-individual-subscriber/getting-started-with-copilot-on-your-personal-account/getting-free-access-to-copilot-pro-as-a-student-teacher-or-maintainer">Free Copilot Pro</a>: student, teacher or maintainer of a popular OSS project</li>
</ul>

<h2>Configuration</h2>

<ul>
  <li>'.copilot' can be used to disabled suggestions</li>
  <li>'copilot.yaml' can be used to configure content exclusion</li>
  <li>'GitHub Copilot editor config' to ensure that code suggestions from Copilot do not incorporate sensitive internal code: use the exclude directive ("exclude": true) in the Copilot editor config file for directories or files</li>
  <li>The "excludePatterns" directive in the editor config file to exclude private repositories or directories from Copilot completions ensure that specific directories, files, or repositories are excluded from GitHub Copilot’s completions, protecting proprietary or internal code from being suggested</li>
  <li>Exclude sensitive content within a repository: Enable "Copilot Exclusion Rules" in the repository's settings, specifying the files and directories containing sensitive information</li>
</ul>

<h2>Security</h2>

<ul>
  <li>Audit Logs: track Copilot usage at a high level (organizational level - user and admin activities related to GitHub Copilot) such as when users enable or disable Copilot in their settings, subscription updates, unauthorized access to GitHub Copilot</li>
  <li>Search for audit events: filters or search queries can tracking administrative actions on Copilot access, e.g, action:copilot.access_enabled to identify events where Copilot access was granted or enabled for organization members</li>
  <li>Admins can search for Copilot-related events by using the query "copilot" within the GitHub organization audit log, filtering results by actor, event type, and date range</li>
  <li>GitHub provides options to configure repository-level exclusion rules to prevent sensitive files and directories from being accessed by GitHub Copilot</li>
  <li>If a policy is applied at enterprise level, all organizations within the enterprise will inherit the policiy</li>
</ul>

<h2>Developer Responsiblity <a href="https://docs.github.com/en/copilot/responsible-use-of-github-copilot-features/responsible-use-of-github-copilot-chat-in-your-ide">[1]</a></h2>

<ul>
  <li>Developers should review AI-generated code for security vulnerabilities, licenses, and ensure compliance with internal policies before using it in production. It can mitigate copyright violations and security risks</li>
  <li>The code generated by copilot is available to be used, modified, and distribute by developers as if they had written it manually</li>
  <li>Copilot can generate code that is similar to existing public code, but it does not track or enforce license compliance. Developers must verify that</li>
  <li>Bias: the developer is respobsible for review code to avoid biased suggestions and make appropriate edits to ensure that the open-source project remains inclusive and avoids reinforcing harmful stereotypes</li>
</ul>

<br />
<h3>References</h3>
<ul>
  <li><a href="https://docs.github.com/en/get-started/showcase-your-expertise-with-github-certifications/about-github-certifications">About GitHub Certifications</a></li>
  <li><a href="https://www.udemy.com/course/github-copilot-certification-practice-exams/?srsltid=AfmBOooSF8IylHUHhqoOnPm3eRt-bHJRk4kuXroCddcMMbxJFXEtfCF9&couponCode=CP130525">Udemy: GitHub Copilot Exam Prep: Ace Your Certification [2025]</a></li>
  <li><a href="https://www.udemy.com/course/githubcopilot/?srsltid=AfmBOorfRgnrpCuFg3p3_h4HaXj0b6d7TSYoB34ZINYJSEj607_HvGFT&couponCode=LETSLEARNNOW">Udemy: [NEW] GitHub Copilot: Use GenAI to Write Terraform For You!</a></li>
  <li><a href="https://www.udemy.com/course/mastering-github-copilot-for-devops-and-devsecops-engineers/?srsltid=AfmBOopPlX998NS-0-ig9ynHkyhowuxX4ZQZ4HZcEtDPlFFbY4WP-2_r&couponCode=LETSLEARNNOW">Udemy: Mastering GitHub Copilot for DevOps and DevSecOps Engineers</a></li>
</ul>  
