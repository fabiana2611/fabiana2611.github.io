---
layout: post
title:  "Terraform Foundation"
date:   2025-02-17
categories: infra book
permalink: /:categories/terraform-foundation
---


<p style="text-align: justify;">This post is just an overview about Terraform guided by the certification content. The material used in my study were:</p>

<ul>
	<li><a href="https://developer.hashicorp.com/terraform/tutorials/certification-associate-tutorials-003">[DOC] Terraform Associate (003) Tutorials</a></li>
	<li><a href="https://developer.hashicorp.com/terraform/tutorials/certification-003/associate-review-003">[DOC] Exam Content List - Terraform Associate (003)</a></li>
	<li><a href="https://developer.hashicorp.com/certifications"></a>TF Certification</li>
	<li><a href="https://www.pluralsight.com/courses/hashicorp-certified-terraform-associate"></a>[CloudGuru] Hashicorp Cetified Terraform Associate: Foundations</li>
	<li><a href="https://www.udemy.com/course/terraform-beginner-to-advanced/?srsltid=AfmBOopbMkNKb0_VqG2dg1aFzfVFoM2N12XLFS5M9fIVLEg-Hx_cveyr">[Udemy] HashiCorp Certified: Terraform Associate 2024</a></li>
	<li><a href="https://www.amazon.es/Terraform-Running-Writing-Infrastructure-Code/dp/1098116747">Book: Terraform - Up and Running</a></li>
	
</ul>


<!-- ### ####################################### -->


<br />
<hr>
<br />
<h2 id="iacconcept">Iac</h2>


<p>Traditional infra issues:</p>
<ul>
	<li>Cannot guarantee infra config consistence</li>
	<li>Lack of standardization</li>
	<li>Slow provisioning</li>
	<li>Human error</li>
	<li>Difficulty in documentation</li>
</ul>

<p style="text-align: justify;"><em>Infrastructure as code (IaC) is a mainstream pattern for managing infrastructure with configuration files rather than through a graphical user interface or through manual command line script sequences. It allows you to build, change, and manage your infrastructure in a safe, consistent, trackable, and repeatable way by defining resource configurations that you can version (in a version control system like GitHub), reuse, and share </em><a href="https://www.hashicorp.com/resources/what-is-infrastructure-as-code">[1]</a><a href="https://developer.hashicorp.com/terraform/intro#infrastructure-as-code">[2]</a>. </p>

<p style="text-align: justify;"><em>IaC makes it easy to provision and apply infrastructure configurations, saving time. It standardizes workflows across different infrastructure providers (e.g., VMware, AWS, Azure, GCP, etc.) by using a common syntax across all of them</em> <a href="https://www.hashicorp.com/blog/infrastructure-as-code-in-a-private-or-public-cloud">[1]</a>.</p>

<p>Benefits of IaC:</p>
<ul>
	<li>Relatively simple to learn and write</li>
	<li>Makes Infrastructure more Reliable: changes become idempotent, consistent, repeatable, and predictable</li>
	<li>Idempotent: the outcome of applying the same configuration multiple times will always result in the same desired state.</li>
	<li>Makes Infrastructure more Manageable</li>
	<li>Reuse of code to deploy similar resources</li>
	<li>Easily change and update existing infrastructure</li>
	<li>Allows a user to turn a manual task into a simple, automated deployment</li>
	<li>Allows recreate an application's infrastructure for disaster recovery scenarios</li>
	<li>Allows infrastructure to be versioned</li>
	<li>Provides configuration consistency and standardization among deployments</li>
	<li>Creating a blueprint of your data center</li>
</ul>

<p>Tools:</p>
<u>
	<li>Infra provisioning tools: Terraform, AWS Cloudformation</li>
	<li>Server templating tools: AWS Cloudformation, AWS EC2 Image Builder, Hashicorp Packer</li>
	<li>Orchestration tools: Kubernetes, Docker Swarm and Apache Mesos</li>
	<li>Configuration management tools: Puppet, Chef, Ansible, SaltStack and Microsoft DSC</li>
</u>

<p><b>Other References</b></p>
<ul>
	<li><a href="https://itnext.io/infrastructure-as-code-landscape-overview-2024-a066124e5989">Infrastructure as Code Landscape Overview 2024</a></li>
	<li><a href="https://www.hashicorp.com/resources/what-is-infrastructure-as-code">Infrastructure as Code: What Is It? Why Is It Important?</a></li>	
</ul>


<!-- ### ####################################### -->


<br />
<hr>
<br />
<h2 id="iacwithterraform">Iac with Terraform</h2>

<p style="text-align: justify;"><a href="https://developer.hashicorp.com/terraform/tutorials/certification-associate-tutorials-003/infrastructure-as-code">Terraform</a> is a Iac tool used to manage infrastructure with <u>declarative</u> (desired end-state) configuration files. It manage multiple cloud platform, track resource changes using state, standardize the deployment workflow, manage dependencies between resources to create or destroy in the correct order, and prevent race conditions. Terraform create a dependency graph to ensure create the resources in the right order.</p>

<u>
	<li>The <a href="https://developer.hashicorp.com/terraform/language/v1.1.x/state/purpose">state</a> maps the resources configuration in the real world.</li>
	<li>Terraform use APIs to handle the resources enabled by <a href="https://registry.terraform.io/">providers</a> like AWS or Azure.</li>
	<li><em>Terraform configuration files are declarative, meaning that they describe the end state of your infrastructure</em></li>
	<li><a href="https://registry.terraform.io/">Core workflow</a>: <u>Write, Plan, Apply</u></li>
	<li>It standarizes the deployment workflow allowing the same Terraform configuration to <a href="https://developer.hashicorp.com/terraform/intro/use-cases#multi-cloud-deployment">different providers</a></li>
</u>

<p><b>Benefits TF with IaC:</b></p>
<ul>
	<li>Store code in a version control helping the collaraboration work <a href="https://developer.hashicorp.com/terraform/cloud-docs/vcs#supported-vcs-providers">(GitHub.com, GitLab, BitBucket, Azure)</a></li>
	<li>Easily integrate with application workflows (GitHub Actions, Azure DevOps, CI/CD tools)</li>
	<li>Provide reusable modules for easy sharing and collaboration</li>
	<li>Manage infrastructure on multiple cloud platforms (platform agnostic)</li>
	<li>Human-readable configuration language</li>. 
	<li>Terraform is written in HashiCorp Configuration Language (HCL)</li>
	<li>Tests modifications using a "dry run" before applying any actual changes</li>
</ul>


<p>Some <a href="https://developer.hashicorp.com/terraform/language/style">recomendations</a> when writing Terraform code. One of them is 2 spaces between each nesting level in Terraform code for better readability and maintainability.</p>



<!-- ### ####################################### -->    



<br />
<hr>
<br />
<h2 id="foundamentals">Terraform Foundamentals</h2>

<p style="text-align: justify;">Terraform is <a href="https://www.hashicorp.com/resources/what-is-mutable-vs-immutable-infrastructure">immutable</a> and declarative. It uses <a href="https://github.com/hashicorp/hcl/blob/main/hclsyntax/spec.md">Hashicorp Configuration Language (HCL)</a> as primary syntax, or optionally <a href="https://developer.hashicorp.com/terraform/language/syntax/json">JSON</a>, more used when importing existing infrastructure or when integrating Terraform with other tools that expect data in JSON format.</p>

<p style="text-align: justify;">Terraform is available for <a href="https://www.terraform.io/enterprise/requirements/os-specific/supported-os">macOS, FreeBSD, OpenBSD, Linux, Solaris, and Windows.</a> </p>

<p style="text-align: justify;">Terraform has some <a href="https://developer.hashicorp.com/terraform/language/syntax/style">recomendation</a> that are not mandatory but are good practices.</p>

<!-- ###  -->    

<h3><b>Install</b></h3>

<p style="text-align: justify;">The terraform might be <a href="https://developer.hashicorp.com/terraform/install">installed</a> by the download of the binary, the package manager of your system like `brew`, or using a control version tool. There are two known tool for easily switch between terraform version: tfswitch and <a href="https://spacelift.io/blog/tfenv">tfenv</a>.</p>

<!-- ###  -->    

<h3><b>Workflow</b></h3>

<p>The Terraform workflow is a <a href="https://developer.hashicorp.com/terraform/tutorials/cli/init">3 step process</a>:</p>
<ol>
	<li><a href="https://developer.hashicorp.com/terraform/cli/commands/init">Init</a> - initialise the project:
		<ul>
        	<li>Download any provider plugins</li>
        	<li>Initialise the working directory to recognise and manage the configuration files</li>
        	<li>Initialise any modules. TF downloads modules from the module registry or a version control system</li>
        	<li>It can automatically download community providers. It was <a href="https://www.hashicorp.com/blog/automatic-installation-of-third-party-providers-with-terraform-0-13">added with Terraform 0.13</a>. Before 0.13, terraform init would NOT download community providers</li>
        	<li>Set up the the backend for storing state files</li>
        	<li><a href="- https://developer.hashicorp.com/terraform/internals/debugging">Debug</a>: If you want to see details you can use variables `TF_LOG` and `TF_LOG_PATH`. It sends logs to stderr. Levels: TRACE (most verbose), DEBUG, INFO, WARN, ERROR <a href="https://developer.hashicorp.com/terraform/internals/v1.1.x/debugging">[1]</a><a href="https://developer.hashicorp.com/terraform/tutorials/configuration-language/troubleshooting-workflow#enable-terraform-logging">[2]</a></li>
    	</ul>
    </li>
    <li><a href="https://developer.hashicorp.com/terraform/cli/commands/plan">Plan</a> - show the planned infrastructure changes: 
    	<ul>
    		<li>Authentication credentials are used to connect to your infra</li>
	        <li>Read your configuration files and the current state</li>
	        <li>Compares them to determine what changes need to be made</li>
	        <li>Generates an execution plan allowing to review the changes before applying them</li>
	        <li>Terraform performs a refresh, unless explicitly disabled</li>
	        <li><a href="https://developer.hashicorp.com/terraform/cli/commands/plan#planning-modes">Refresh-only</a> mode: creates a plan whose goal is only to update the Terraform state and any root module output values to match changes made to remote objects outside of Terraform. </li>
	        <li>save the plan: use the -out flag</li>
    	</ul>
    </li>
    <li><a href="https://developer.hashicorp.com/terraform/cli/commands/apply">Apply</a> - deploy the infrastructure: 
    	<ul>
        	<li>Executes the planned changes modifying the infrastructure to match the desired state in your configuration files</li>
        	<li>Records the changes in the Terraform state file</li>
        	<li>Option for auto-approve as opposed to waiting for approval (necessary for CI/CD)</li>
        	<li>By default, uses <a href="https://developer.hashicorp.com/terraform/internals/graph#walking-the-graph">parallelism</a> (10 resources concurrently)</li>
        	<li><a href="https://developer.hashicorp.com/terraform/cli/commands/plan#replace-address">Replace</a>: Using `terraform apply -replace=aws_instance.web` allows mark a specific resource for replacement without affecting other resources.</li>
    	</ul>
    </li>
    <li><a href="https://developer.hashicorp.com/terraform/tutorials/aws-get-started/aws-destroy">Destroy</a> - remove infra: 
    	<ul>
        	<li>It needs an approval</li>
        	<li>Use the state file to destroy the resources</li>
    	</ul>
    </li>
</ol>

<!-- ###  -->    

<h3><b>Architecture</b></h3>

<ul>
	<li>Terraform is a plugin-based architechture.</li>
	<li>Terraform and plugins use Go language</li>
	<li><a href="https://developer.hashicorp.com/terraform/plugin/how-terraform-works#terraform-core">Terrform Core</a>: is the CLI. It is responsible for IaC, state management, dependency graph, plan, communication with plugins that happens via `remove procedure call` (RPC)</li>
	<li><a href="https://developer.hashicorp.com/terraform/plugin/how-terraform-works#terraform-plugins">Terraform Plugins</a>: exposes the implementation for the service, executed as a separate process, are responsible for initialization of libraries, authentication, define data and resources, define functions.</li>
</ul>


<!-- ###  -->    

<h3><b>Resources</b></h3>

<p><a href="https://developer.hashicorp.com/terraform/language/resources">Terraform resources</a> are:</p>
<ul>
	<li>Resources Blocks</li>
	<li>Resources Behaviour</li>
	<li>Meta-Arguments: depends_on, count, for_each, provider, lifecycle</li>
</ul>

<!-- ###  -->    

<h3><b>Providers</b></h3>

<ul>
	<li>The Terraform providers are responsible for allow the interaction between Terraform and cloud providers. That communication is done via APIs. Examples of providers: google, aws, azure, kubernetes, datadog, etc. <a href="https://developer.hashicorp.com/terraform/tutorials/configuration-language/provider-versioning">[1]</a><a href="https://developer.hashicorp.com/terraform/language/v1.1.x/providers/configuration">[2]</a><a href="https://developer.hashicorp.com/terraform/language/providers">[3]</a><a href="https://registry.terraform.io/browse/providers">[4]</a><a href="https://developer.hashicorp.com/terraform/language/providers/requirements#provider-installation">[5]</a><a href="https://developer.hashicorp.com/terraform/cli/commands/providers">[6]</a></li>
	<li><em>Providers are distributed separately from Terraform itself, and each provider has its own release cadence and version numbers.</em> <a href="https://developer.hashicorp.com/terraform/plugin/how-terraform-works">[1]</a></li>
	<li>The providers are plugins that are downloaded in `init` step considering the provider configuration. </li>
	<li>- The <a href="https://developer.hashicorp.com/terraform/plugin#installing-plugins">provider plugins are downloaded and stored</a> in the `.terraform/providers` directory within the current working directory.</li>
	<li>In case be necessary use <a href="https://www.terraform.io/language/providers/configuration#alias-multiple-provider-configurations">multiple providers</a>, terraform allows the use of <u>alias</u> to manage them.</li>
	<li>The <a href="https://registry.terraform.io/providers/hashicorp/vault/latest/docs">Vault Provider</a> allows you to read and write to HashiCorp Vault from Terraform. </li>
	<li>Good practice: specify the provider version inside the terraform setting block</li>
	<li><em>Each Terraform module must declare which providers it requires, so that Terraform can install and use them. Provider requirements are declared in a required_providers block</em><a href="https://developer.hashicorp.com/terraform/language/providers/requirements#requiring-providers">[1]</a></li>
	<li><a href="https://registry.terraform.io/providers/hashicorp/aws/latest/docs#authentication">Authentication</a></li>
</ul>

<p style="text-align: justify;">The provider (plugin) can exist in local work directory without any reference to it in the Terraform configuration, and may not reflect a provider dependency. That provider dependency exisist if: exist any resource instace belong to a provider in the state; exist any resource or data block in configuration; or explicit provider block in configuration.</p>

<p style="text-align: justify;">In case multiple users sharing the same Terraform configuration then they should use the same <a href="https://developer.hashicorp.com/terraform/language/expressions/version-constraints#version-constraint-syntax">version</a>. For that, there are two alternatives to manage the provider version: provide version (<a href="https://developer.hashicorp.com/terraform/language/settings#specifying-a-required-terraform-version">required_version</a>) in terraform block or dependency lock file. More details about the <u>Terraform block</u> you can see <a href="https://developer.hashicorp.com/terraform/language/terraform#specifying-provider-requirements">here</a>.</p>

<p>For <b>Dependency Lock</b> approach:</p>
<u>
	<li>The <a href="https://developer.hashicorp.com/terraform/language/files/dependency-lock">dependency lock</a> is related to provider dependencies. It stores the version to be used. </li>
	<li>The `init` step considers the version constraints in the configuration and the version selections recorded in the lock file as well. The Terraform will get the version recorded in lock file</li>
	<li>This file (`.terraform.lock.hcl`) must be in root folder and pushed to the code repository</li>
	<li>The lock file has the exact version of each provider is used (inside of required_providers block)</li>
	<li>Use `terraform init -upgrade` to update the version</li>
	<li>A checksum verification checks if the checksum for the packaged to be installed matches with the checksum related to the version in lock file</li>
</u>

<!-- ###  -->    

<h3><b>State</b></h3>

<p><a href="https://developer.hashicorp.com/terraform/language/v1.1.x/state/purpose">Concepts:</a></u></p>
<ul>
	<li>All the metadata about deploy</li>
	<li>Track what is deployed (real infrastructure) by a state file (mapping configuration to real-world resources)</li>
	<li>State file is stored in plain text</li>
	<li>Stored locally in `terrafomr.tfstate` (default) </li>
	<li>Stored remotely in AWS S3, Google Storage
		<ul>
			<li>Allows sharing state file with multiple teams</li>
			<li>Remove Storage allows loking state so parallel execution don't coincide</li>
			<li>Enables sharing output values with other Terraform configuration or code</li>
		</ul>
	</li>
	<li>State locking support remote state storage that prevents conflicts and potential corruption of the state file by multiple execution in deployment using the same state file simultaneously. <a href="https://developer.hashicorp.com/terraform/language/state/locking">[1]</a><a href="https://www.terraform.io/language/state/locking">[2]</a></li>
	<li>It helps to create new deployment plans</li>
	<li>It helps boost deployment performance by caching resource attributes for subsequent use, avoiding query the cloud provider's API repeatedly</li>
	<li>Helps to determining the correct order to destroy resources</li>
</ul>

<p><a href="https://developer.hashicorp.com/terraform/tutorials/state/state-cli">Commands:</a></p>
<ul>
	<li>State commands: list, show, output, graph <a href="https://developer.hashicorp.com/terraform/cli/v1.1.x/inspect">[1]</a></li>
	<li><a href="https://developer.hashicorp.com/terraform/tutorials/state/state-cli#replace-a-resource-with-cli">Replace</a>: rebuild a specific resources avoiding a full destroy operation. It recreates the resource even without midification in the configuration (previous versions: taint)(terraform taint RESOURCE_ADDRESS -> modifies state file (taints a resource, force to be destroyed and recreted)) </li>
	<li><a href="https://developer.hashicorp.com/terraform/tutorials/state/state-cli#move-a-resource-to-a-different-state-file">Move</a>: the `terraform state mv` moves resources from one state file to another. You can also rename resources with mv. The move command will update the resource in state, but not in your configuration file</li>
	<li><a href="https://developer.hashicorp.com/terraform/tutorials/state/state-cli#remove-a-resource-from-state">Remove</a>: Use a removed block to remove specific resources from your state. This does not destroy the infrastructure itself, instead it indicates that your Terraform configuration will no longer manage the resource.</li>
	<li><a href="https://developer.hashicorp.com/terraform/tutorials/state/state-cli#refresh-modified-infrastructure">Refresh</a>: The terraform refresh command updates the state file when physical resources change outside of the Terraform workflow.</li>
	<li>The import feature is used when a resource exists and you wish that be manage by terraform. <a href="https://www.terraform.io/cli/commands/import">[1]</a><a href="https://developer.hashicorp.com/terraform/language/state/import">[2]</a><a href="https://developer.hashicorp.com/terraform/cli/import/usage">[3]</a></li>
	<li><a href="https://developer.hashicorp.com/terraform/cli/commands/validate">Validate</a>: terraform validate check and report errors within modules, attribute names, and value types to ensure they are syntactically valid and internally consistent.</li>
	<li><a href="https://developer.hashicorp.com/terraform/cli/commands/force-unlock">terraform force-unlock</a> or "terraform state rm" command followed by the "terraform state push"</li>
</ul>


<p><u>Workspace</u></p>
<ul>
	<li>Definition: It is the state file working directory, where the `terrafomr.tfstate` file will be stored. </li>
	<li>Each Terraform <a href="https://developer.hashicorp.com/terraform/language/state/workspaces#workspace-internals">workspace</a> indeed uses its own state file to manage the infrastructure specific to that workspace</li>
	<li><a href="https://blog.gruntwork.io/how-to-manage-terraform-state-28f5697e68fa#784f">Isolate State:</a>
		<ul>
			<li>workspace: path where the state is stored. It is not the best approach for isolate environments to avoid mistakes.</li>
			<li>file layout: best solution for the full isolation between the environments: each TF configuration file must be inside a different folder; and must configure a different backend for each environment with different authentication and access controll (e.g, different S3)</li>
		</ul>
	</li>	
	<li>A workspace can only be configured to a single VCS repo, however, multiple workspaces can use the same repo.<a href="https://developer.hashicorp.com/terraform/cloud-docs/workspaces/creating">[1]</a></li>
	<li><a href="https://learn.hashicorp.com/tutorials/terraform/cloud-migrate">Migration:</a> to migrate a backend is necessary to move the state file and configuration to a nre location. The backend can be migrate even if exists managed resources whithout de-provisioning anything</li>
	<li>The default local backend stores the state file on the local filesystem of the machine where Terraform is being run. It uses system APIs to lock the state file and performs all operations locally.</li>
	<li>Alternatives available to provide the remaining values to Terraform to initialize and communicate with the remote backend: use the -backend-config=PATH flag to specify a separate config file enables users to store sensitive information in a dedicated file that can be securely managed; directly querying HashiCorp Vault for the secrets; interactively on the command line</li>
	<li>Commands: <a href="https://developer.hashicorp.com/terraform/cli/commands/workspace/select">[1]</a><a href="https://developer.hashicorp.com/terraform/cli/commands/workspace/new">[2]</a>
		{% highlight ruby %}
		terrraform workspace new NAME
		terraform workspace select NAME
		terraform workspace list
		Variable Access: ${terraform.workspace} 
		{% endhighlight %}
	</li>
</ul>

<!-- ###  -->   

<h3><b>Variables and Outputs</b></h3>

<p style="text-align: justify;">Usually the map key/value of variables are inside the file `terraform.tfvars` and the declarations whith their <a href="https://developer.hashicorp.com/terraform/language/expressions/types">data types</a>, and <a href="https://developer.hashicorp.com/terraform/language/values/variables#declaring-an-input-variable">names</a> are inside `variables.tf`. Also, the variables can be <a href="https://developer.hashicorp.com/terraform/cli/config/environment-variables">environment variables</a> that must be in the format TV_VAR_VARIABLENAME. </p>

Type Constraints:
- Primitive types: number, strong, bool
- Complex types 
- - Collection (one primitives): list, map, set
- - Structural (multiple primitives): tuple, set , object
- Dynamic Type:
- any (not decided yet)

<p>The <a href="https://developer.hashicorp.com/terraform/language/values/locals">locals</a> block is another way to declare variables but it can create variables and use expressions.</p>

<p style="text-align: justify;">The <a href="https://developer.hashicorp.com/terraform/language/values/variables">input variables</a> are the values you pass to the terraform configuration. When they are declared inside the module is necessary to take care if it is sensitive or not because even sensitive variables are store inside state file. If you don't want to store that, you can mark it as ephemeral.</p>

<p style="text-align: justify;">As of Terraform 0.9, Terraform does not persist state to the local disk when remote state is in use, and some backends can be configured to encrypt the state data at rest.<a href="https://developer.hashicorp.com/terraform/language/state/sensitive-data">[1]</a></p>

<p style="text-align: justify;">If you pass that values using <a href="https://www.terraform.io/docs/commands/environment-variables.html">environment variable</a> and it is <a href="https://developer.hashicorp.com/terraform/language/values/variables#values-for-undeclared-variables">undeclared</a>, no warning or error will be shown. In case the values are passed inside of `.tfvars` file, then a warn will be shown, what helps to identify some mistakes. In case it is passed by command line then it will return an error.</p>

<p style="text-align: justify;">The <a href="https://developer.hashicorp.com/terraform/language/values/variables#variable-definition-precedence">terraform precedence</a> to load th variables is: Environment variable, `.tfvars` or `.tfvars.json`, `.auto.tfvars` or `.auto.tfvars.json`, -var or -var-file (using the order given in command line).</p>

<p style="text-align: justify;">Consiring that risk of expose sensitive data, Terraform <a href="https://github.com/github/gitignore/blob/main/Terraform.gitignore">recommends to ignore</a>: `terraform.tfstate`, `terraform.tfvars`, .terraform directory , terraform.tfstate and terraform.tfstate.backup, .tfvars files, .tfplan files.</p>

<p style="text-align: justify;">Even using the Terraform provider for <a href="https://learn.hashicorp.com/tutorials/terraform/secrets-vault">Vault</a>, the tight integration between Terraform and Vault does not automatically mask secrets in the state file. Developers need to implement secure practices to handle secrets effectively. An alternative is to use environment variables to store sensitive information or use Terraform's data sources to retrieve the information from the environment. </p>


<h2>References</h2>
<ul>
	<li><a href="https://itnext.io/infrastructure-as-code-landscape-overview-2024-a066124e5989">Infrastructure as Code Landscape Overview 2024</a></li>
	<li><a href="https://www.hashicorp.com/resources/what-is-infrastructure-as-code">Infrastructure as Code: What Is It? Why Is It Important?</a></li>	
</ul>


<!-- ###  -->   

<h3><b>Data Sources</b></h3>

<p style="text-align: justify;"><em>In Terraform, data blocks are used to retrieve data from external sources, such as APIs or databases, and make that data available to your Terraform configuration. With data blocks, you can use information from external sources to drive your infrastructure as code, making it more dynamic and flexible.</em> <a href="https://developer.hashicorp.com/terraform/language/data-sources">[1]</a></p>

A data source in Terraform enables the configuration to fetch data from an external source, such as an API or a cloud provider, to be used elsewhere in the Terraform configuration. This allows Terraform to dynamically retrieve information needed for resource provisioning.<a href="https://developer.hashicorp.com/terraform/language/data-sources">[2]</a>


<!-- ###  -->   

<h3><b>Meta-Arguments: depends_on, count, for_each, provider, lifecycle</b></h3>

<p><u>depends_on</u></p>

<p style="text-align: justify;"> In TF we can identify two types of dependencies: <a href="https://developer.hashicorp.com/terraform/tutorials/configuration-language/dependencies">[1]</a><a href="https://developer.hashicorp.com/terraform/tutorials/certification-associate-tutorials-003/dependencies">[2]</a><a href="">[3]</a></p>
<ul>
	<li><em>The `depends_on` argument in Terraform creates an explicit dependency between resources. This means that Terraform will wait for the specified resource to be created or updated before proceeding with the dependent resource. </em></li>
	<li><em>Terraform implicit dependencies refer to the dependencies between resources in a Terraform configuration but are not explicitly defined in the configuration. Terraform uses a graph to track these implicit dependencies and ensures that resources are created, updated, and deleted in the correct order.</em></li>
</ul>

<p><u>count</u></p>

<p style="text-align: justify;"><em>The count argument replicates the given resource or module a specific number of times with an incrementing counter</em><a href="https://developer.hashicorp.com/terraform/tutorials/configuration-language/count">[1]</a></p>

<p style="text-align: justify;">It's necessary to take care of it when manipulate a list because the content can change the position (in case remove any object).</p>

<p><u>for_each</u></p>

<p style="text-align: justify;"><em>In Terraform, when you use the for_each argument in a resource block, Terraform generates multiple instances of that resource, each with a unique address. The address of each instance is determined by the keys of the for_each map, and it is used to identify and manage each instance of the resource.</em> <a href="https://developer.hashicorp.com/terraform/cli/v1.1.x/state/resource-addressing">[1]</a></p>

<p><u>Dynamic blocks</u></p>

<p style="text-align: justify;"><em>Repeatable nested blocks which typically represent separate objects that are related to (or embedded within) the containing object.</em> Supported within: resource, data, provider and provisioner <a href="https://developer.hashicorp.com/terraform/language/expressions/dynamic-blocks">[1]</a></p>


<!-- ### ####################################### -->    

<br />
<hr>
<br />
<h2 id="advanced">Advanced Concepts</h2>

<h3><b>Modules</b></h3>

<p style="text-align: justify;" ><a href="https://developer.hashicorp.com/terraform/tutorials/modules/module">Module</a> is a collection of code. The main folder of your code where you run terraform commands is called root module. The modules that you call are called <a href="https://developer.hashicorp.com/terraform/language/v1.1.x/modules/syntax">child module</a>.</p>

<p style="text-align: justify;" >It's possible pass <a href="https://learn.hashicorp.com/tutorials/terraform/module-use#set-values-for-module-input-variables">arguments</a> to the modules. In case the result of the module needs to be used by who call it, then is necessary to use the <a href="https://developer.hashicorp.com/terraform/language/v1.1.x/modules/syntax#accessing-module-output-values">output</a> to access it. That <a href="https://learn.hashicorp.com/tutorials/terraform/module-use#define-root-output-values">output</a> values are defined within the module. </p>

<p style="text-align: justify;" >A point to be carefull is the scenario where is necessary to refactor the module. The state can be impacted and they can marke destroy to create a new one. To avoid this, you can follow this <a href="https://developer.hashicorp.com/terraform/language/v1.1.x/modules/develop/refactoring">Refactoring tutorial</a> and manage the states and resources to preserve the existent resources.</p>

<p style="text-align: justify;">You can <a href="https://developer.hashicorp.com/terraform/tutorials/modules/module-create">create</a> your own module or reuse from some <a href="
https://registry.terraform.io/browse/modules">private/public registry</a>. <a href="https://developer.hashicorp.com/terraform/tutorials/modules/module-use">Here</a> is how to use these modules.</p>

<p style="text-align: justify;" >The modules can be in public or private registry. Private registry modules have source strings of the form HOSTNAME/NAMESPACE/NAME/PROVIDER. This is the same format as the public registry but with an added hostname prefix.</p>

<p>benefits</p>
	<li>support versioning</li>
	<li>automatically generated documentation</li>
	<li>allow browsing version histories</li>
	<li>show examples and READMEs</li>
</ul>

<p style="text-align: justify;" ><a href="https://developer.hashicorp.com/terraform/registry/modules/publish#requirements">Requirements</a> to publish in TF registry:</p>
<ul>
	<li>the module must live in public GH repo</li>
	<li>the module must be named terraform-PROVIDER-NAME</li>
	<li>the module mus follow a specific structure: provide readme and using convension of main, variables, outputs</li>
	<li>the repo must use Git tags semantic <a href="https://developer.hashicorp.com/terraform/language/modules/syntax#version">versioning (x.y.z)</a> for releases</li>
</ul>


<!-- ###  -->   

<h3><b>Provisioners</b></h3>

<ul>
	<li>Provisioners are used to execute scripts on a local or remote machine as part of resource creation or destruction <a href="https://www.terraform.io/docs/provisioners/index.html">[1]</a>
		<ul>
			<li>local-exec: invokes a local executable after a resource is created</li>
			<li><a href="https://www.terraform.io/docs/provisioners/remote-exec.html">remote-exec</a>: invoke scripts or run commands directly on the remote server</li>
		</ul>
	</li>	
 	<li>Terraform way of bootstrapping custom scripts, commands or actions</li>
 	<li>Creation-time and Destroy-time</li>
</ul>


<!-- ###  -->   

<h3><b>Functions</b></h3>

<ul>
	<li>Terraforms comes pre-packaged with functions<a href="https://developer.hashicorp.com/terraform/language/functions">[1]</a></li>
	<li>User-defined functions are nor allowed</li>
	<li>Built-In Functions: join</li>
	<li>Test using <a href="https://developer.hashicorp.com/terraform/cli/commands/console">console</a>:$terraform console. Command-line interface (CLI) tool that allows you to interactively evaluate expressions in Terraform. The terraform console command opens a REPL (Read-Eval-Print Loop) environment, where you can type Terraform expressions and see the results immediately. Console is used to test expressions, debugging configuration and understand TF behaviour.</li>
</ul>	


<p><b>Other References</b></p>
<ul>
	<li><a href="https://developer.hashicorp.com/terraform/language/functions/index_function">Index function</a></li>
	<li><a href="https://www.terraform.io/docs/configuration/functions/zipmap.html">zipmap function</a></li>	
	<li><a href="https://www.terraform.io/language/functions/lookup">lookup function</a></li>	
	<li><a href="https://developer.hashicorp.com/terraform/language/functions/length">Length function</a></li>	
	<li><a href="https://developer.hashicorp.com/terraform/language/functions/element">Element</a></li>	
</ul>



<!-- ### ####################################### -->    


<br />
<hr>
<br />
<h2 id="tfcloud">Terraform Cloud and Enterprise</h2>

<ul>
	<li><a href="https://developer.hashicorp.com/terraform/cloud-docs">HCP Enterprise</a></li>
	<li>HCP Terraform can be managed from the CLI but requires an <a href="https://developer.hashicorp.com/terraform/cloud-docs/users-teams-organizations/api-tokens">API token</a></li>
	<li>Terraform Community (Free)/CLI <a href="https://developer.hashicorp.com/terraform/cli/workspaces#workspace-internals">store the local state</a> for workspaces in the directory called terraform.tfstate.d/WORKSPACENAME</li>
	<li>In HCP Terraform, you can switch between <a href="https://developer.hashicorp.com/terraform/cloud-docs/workspaces">workspaces</a> directly within the HCP Terraform web interface without the need to use the CLI. In HCP Terraform, each workspace represents a separate environment.</li>
	<li>The Terraform CLI is primarily used to run Terraform commands locally on your development machine. When working with HCP Terraform, you typically interact with your workspaces through the web UI or by using HCP Terraform's API.</li>
	<li>HCP Terraform always encrypts state at rest</li>
	<li><a href="https://developer.hashicorp.com/terraform/cloud-docs/workspaces">Workspaces</a>, managed with the terraform workspace command, isn't the same thing as HCP Terraform's workspaces. HCP Terraform workspaces act more like completely separate working directories. HCP Terraform offers additional features and capabilities for managing workspaces, such as remote state management, collaboration tools, and version control integration, which are not available in the Community version. <a href="https://developer.hashicorp.com/terraform/language/state/workspaces">CLI workspaces</a> (Community) are just alternate state files.</li>
	<li>Air Gap: network security measure employed to ensure that a secure computer network is physically isolated. <a href="https://www.hashicorp.com/blog/deploying-terraform-enterprise-in-airgapped-environments">Install terraform in a place where internet is unavailable</a></li>
	<li><a href="https://developer.hashicorp.com/terraform/cloud-docs/run/remote-operations">Remote Operations</a>: <em>After approving a merge request, HCP Terraform will run a speculative plan to show the potential changes that will be applied to the managed environment. This allows users to review and validate the changes against any applicable Sentinel policies before applying them.</em></li>
	<li><a href="https://developer.hashicorp.com/terraform/tutorials/cloud/cloud-versions">Upgrade TF version in HCP</a>: <em>When you create a new workspace, HCP Terraform automatically selects the most recent version of Terraform available. If you migrate an existing project from the CLI to HCP Terraform, HCP Terraform configures the workspace to use the same version as the Terraform binary you used when migrating. HCP Terraform also provides the ability to upgrade your Terraform version in a controlled manner. This allows you to upgrade your Terraform version in a safe and predictable way, without affecting your existing infrastructure or state.</em></li>
	<li><a href="https://developer.hashicorp.com/terraform/cloud-docs/agents">HCP Terraform agents</a> <em>are lightweight programs deployed within your target infrastructure environment. Their primary function is to receive Terraform plans from HCP Terraform, execute those plans locally, and apply the desired infrastructure changes. This allows you to manage private or on-premises infrastructure with HCP Terraform without opening your network to public ingress traffic.</em></li>
	<li>
		Workspace <a href="https://developer.hashicorp.com/terraform/cloud-docs/workspaces">[1]</a><a href="https://developer.hashicorp.com/terraform/language/state/workspaces">[2]</a>: 
		<ul>
			<li>HCP Terraform manages infrastructure collections with a workspace whereas CLI manages collections of infrastructure resources with a persistent working directory. This distinction helps in organizing and separating different environments or configurations.</li>
			<li>HCP Terraform maintains the state version and run history for each workspace</li>
			<li>CLI workspaces are alternative state files in the same working directory</li>
		</ul>
	</li>
	<li>
		<a href="https://developer.hashicorp.com/terraform/cloud-docs/workspaces/variables">Scope level using variables in HCP Terraform</a>: You can create a variable set by adding variables to the variable set and then applying a variable set scope so it can be used by multiple HCP Terraform workspaces. You can also apply the variable set globally, which will apply the variable set to all existing and future workspaces
		<ul>
			<li>Multiple workspaces using a variable set</li>
			<li>All current and future workspaces in a project using a variable set</li>
			<li>A specific Terraform run in a single workspace</li>
		</ul>
	</li>	
	<li>
		<a href="https://developer.hashicorp.com/terraform/cloud-docs/policy-enforcement">Sentinel or OPA with HCP Terraform</a>
		<ul>
			 <li><em>Both tools allow you to define custom policies to evaluate and control Terraform configurations before they are applied. Both offer powerful capabilities to enforce custom policies on your Terraform configurations, providing an additional layer of security and governance. By leveraging these tools, you can prevent sensitive information or undesired strings from being present in your infrastructure code, reducing the risk of accidental misconfigurations and potential security vulnerabilities.<em> <a href="https://developer.hashicorp.com/terraform/cloud-docs/policy-enforcement/sentinel">[1]</a><a href="https://developer.hashicorp.com/terraform/cloud-docs/policy-enforcement/opa">[2]</a></li>
			<li>Sentinel Policy: policy as code framework integrated with HashiCoprp Enterprise</li>
			<li>Teal-time feedback on potential security risks in Terraform configurations during the development process</li>
			<li>Sentinel and OPA can enhance security by preventing unauthorized changes to your managed infrastructure</li>
			<li>Organizations can enforce resource naming conventions or approved machine images for improved consistency and clarity</li>
			<li>Sentinel and OPA enable automated policy checks to enforce compliance standards before applying changes to production environments</li>
		</ul>	
	</li>
</ul>

	