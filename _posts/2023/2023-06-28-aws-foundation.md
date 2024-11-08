---
layout: post
title:  "AWS Cloud Concepts"
date:   2023-06-01
categories: infra
permalink: /:categories/aws-foundational
---

<table>
  <tr>
    <td><a href="#concept">Cloud Concepts</a></td>
    <td><a href="#iam">IAM</a></td>
    <td><a href="#orgcontrolpower">AWS Organization and Control Power</a></td>
  </tr>
  <tr>
    <td><a href="#ec2">EC2</a></td>
    <td><a href="#asg">ASG</a></td>
    <td><a href="#network">AWS networking services</a></td>
  </tr>
  <tr>
    <td><a href="#storage">AWS Storage Services</a></td>
    <td><a href="#container">Docker Containers and ECS</a></td>
    <td><a href="#serverless">Serverless Applications</a></td>
  </tr>
  <tr>
    <td><a href="#database">AWS database services</a></td>
    <td><a href="#deploy">Deployment</a></td>
    <td><a href="#monitoring">Monitoring</a></td>
  </tr>
  <tr>
    <td><a href="#security">Security</a></td>
    <td><a href="#migration">Migration</a></td>
    <td><a href="#machinelearning">Machine Learning</a></td>
  </tr>

  <tr>
    <td><a href="#globalinfra">AWS Global Infrastructure</a></td>
    <td><a href="#others">Others Services</a></td>
    <td><a href="#pricing">Billing and Pricing</a></td>
  </tr>
  <tr>
    <td><a href="#architect">AWS Well-Architected Framework</a></td>
    <td><a href="#support">Support</a></td>
    <td><a href="#shots">Some Shots</a></td>
  </tr>
  <tr>
    <td colspan="3"><a href="#conclusion">Conclusion</a></td>
  </tr>
</table>


 <br />
 <hr>

<p style="text-align: justify;">AWS has a lot of certifications and a set of them together defines a Role. You can see all the journeys <a href="https://d1.awsstatic.com/training-and-certification/docs/AWS_certification_paths.pdf">here</a>. As soon as you are  prepared, you can schedule your exam <a href="https://aws.training">here</a>. Two important benefits are 30 minutes more if you are not a native  English speaker, and 50% in your next test. </p>

<p style="text-align: justify;">The first test must be the <a href="https://aws.amazon.com/certification/certified-cloud-practitioner/?ch=tile&tile=getstarted">AWS Certified Cloud Practitioner (CLF-C01)</a>, and this post is regarding that one.</p>

<p style="text-align: justify;">The first step to start your journey is <a href="https://www.tutorialspoint.com/amazon_web_services/amazon_web_services_account.htm">creating your account</a> to do your tests. AWS has a <a href="https://repost.aws/knowledge-center/create-and-activate-aws-account">HowTo</a> for it. Don't forget to not use the root to do your tasks. You have to create an AWS IAM service by <a href="https://aws.amazon.com/getting-started/hands-on/getting-started-with-aws-management-console/?ref=gsrchandson">AWS Management Console</a>. The default region available to the user is <b>North Virginia</b>.</p>

<p style="text-align: justify;">The course used fot this was:</p>
<ul>
  <li><a href="https://www.udemy.com/course/aws-certified-cloud-practitioner-training-course/">Udemy Course: AWS Certified Cloud Practitioner Exam Treining</a></li>
  <li><a href="https://www.udemy.com/course/aws-certified-cloud-practitioner-new/">Udemy Course: [NEW] Ultimate AWS Certified Cloud Practitioner - 2023</a></li>
  <li><a href="https://www.udemy.com/course/aws-certified-cloud-practitioner-practice-exams-c/">AWS Certified Cloud Practitioner Practice Exams CLF-C01 2023</a></li>
  <li><a href="https://www.udemy.com/course/practice-exams-aws-certified-cloud-practitioner/">6 Practice Exams | AWS Certified Cloud Practitioner CLF-C01</a></li>
</ul>


<p><center>
  <img src="/img/aws/aws-arch.svg" height="100%" width="100%">
</center></p>

<!-- ######################################################## -->

<br />
<hr>
<br />
<h2 id="concept">Cloud Concepts</h2>

<p style="text-align: justify;"><b>Definition</b>: <a href="https://aws.amazon.com/what-is-cloud-computing/">Cloud computing</a> is the on-demand delivery of IT resources over the Internet with pay-as-you-go pricing. </p>

<p style="text-align: justify;"><b>Cloud vs Traditional</b>:</p>
<ul>
  <li><b>Cloud:</b> On-demand, Broad network access, Resource pooling, Rapid elasticity, Measured Service.</li>
  <li><b>Traditional:</b> Requires human involvement, Internal accessibility, limited public presence, Single-tenant, can be virtualized, Limited scalability, Usage is not typically measured</li>
</ul>

<p style="text-align: justify;"><b>Problems solved:</b> Flexibility; Cost-Effectiveness, Scalability, Elasticity, Agility, High-availability and fault-tolerance</p>

<p style="text-align: justify;"><a href="https://aws.amazon.com/what-is-cloud-computing/?pg=TOCC"><b>Benefits</b></a>: Agility, Elasticity, Cost saving (trade fixed expenses for variable expenses), deploy globally in minutes</p>

<p style="text-align: justify;"><b><a href="https://docs.aws.amazon.com/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html">Advantages</a> of cloud computing</b></p>
<ul>
  <li>On-Demand: Pay only when you consume computing resources, and pay only for how much you consume</li>
  <li>Economies of scale: lower pay as-you-go prices</li>
  <li>Elasticity: Scale up and down as required with only a few minutes</li>
  <li>Increase speed and agility: the cost and time it takes to experiment and develop is significantly lower; speed to create resources; experiment quickly; scalable compute capacity</li>
  <li>Stop spending money running and maintaining data centers</li>
  <li>Go global in minutes</li>
</ul>  

<p style="text-align: justify;"><b><a href="https://aws.amazon.com/types-of-cloud-computing/">Cloud Computing Models</a></b></p>
<ul>
  <li><b>IaaS</b> (Infrastructure as a Service): not responsible by the underline hardware and hypervisor but by the operating system (OS), Data and Application. Ex: EC2, CloudFormation.</li>
  <li><b>PaaS</b> (Platform as a Service): responsible for the applications and data. The customers only need upload their code/data to create the application. Ex: AWS Elastic Beanstalk; Azure WebApps; Compute App Engine.</li>
  <li><b>SaaS</b> (Software as a Service): Not manage anything, only use the service (Facebook, Salesforce). Signup an account. </li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/types-of-cloud-computing/">Cloud Computing Deployment Models</a></p>
<ul>
  <li>Public Cloud (AWS, Azure, GCP): the resources are owned and operatad by the provider, and the services delivered by internet</li>
  <li><a href="https://aws.amazon.com/hybrid/?pg=TOCC">Hybrid Cloud</a>: keep some services on primise. It has the control of sensitive assets and flexibility of the public.</li>
  <li>Private Cloud (on-premise): not exposed; it allows automatize some process but all the management of the stack is responsability of the company. It must incluse self-service, multi-tenancy, metering, and elasticity. Benefits: Complete control, security (keep the data and application in house)</li>
  <li>Multicloud - use private/public from multiple providers</li>
</ul>

<p style="text-align: justify;"><b><a href="https://aws.amazon.com/serverless/">Serverless</a>:</b> <em>technologies for running code, managing data, and integrating applications, all without managing servers. Serverless technologies feature automatic scaling, built-in high availability, and a pay-for-use billing model to increase agility and optimize costs. It eliminates infrastructure management tasks like capacity provisioning, patching and OS maintenance.</em> It not mean no server.</p>  


<p><b>Aditional References:</b></p>
<ul>
  <li><a href="https://digitalcloud.training/aws-cloud-computing-concepts/">DigitalCloudSummary</a></li>
  <li><a href="https://aws.amazon.com/what-is-cloud-computing/?nc2=h_ql_le_int_cc">AWS - What is cloud computing?</a></li>
</ul>


<!-- ########################################### -->



<br />
<hr>

<br />
<h2 id="globalinfra">AWS Global Infrastructure</h2>

<p style="text-align: justify;"><a href="https://aws.amazon.com/about-aws/global-infrastructure/">AWS Global Infrastructure</a>: make possible a global application (decrease latency, disaster recovery, attack protection)</p>
<ul>
  <li><b>Availability Zones</b> (AZ): <em>one or more discrete data centers with redundant power, networking, and connectivity. Each AZ has independent power, cooling, and physical security and is connected via redundant, ultra-low-latency networks. AZs give customers the ability to operate production applications and databases that are more highly available, fault tolerant, and scalable than would be possible from a single data center. All traffic between AZs is encrypted. AZs are physically separated by a meaningful distance.</em>. Minimum of two AZ to achieve high availability.</li>
  <li>AWS <b>Regions</b>: <em> physical location around the world where we cluster data centers. Each AWS Region is isolated, and physically separate AZs within a geographic area.</em> Minimum of three AZs by region. Criterias to choose the region: Compliance, Proximity to the customer, available service (<a href="https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/">List of AWS Services Available by Region</a>) and pricing.</li>
  <li><a href="https://aws.amazon.com/about-aws/global-infrastructure/localzones/"><b>Local Zones</b></a>: <em>place compute, storage, database, and other select AWS services closer to end-users. Each AWS Local Zone location is an extension of an AWS Region.</em></li>
  <li><b>Edge Locations</b>: <em>Content Delivery Network (CDN) endpoints for CloudFront</em>. Delivery content closer the user.</li>
  <li>Regional <b>Edge Caches</b>: <em>between your CloudFront Origin servers and the Edge Locations</em></li>
  <li>Architecture: Single Region + SingleAZ; Single Region + Multi AZ; Multi Region + Active-Passive; Multi Region + Active-Active</li>
  <li>In Active-Passive failover is possible to apply the <a href="https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html">routing policy</a> Failover routing</li>
</ul>


<p style="text-align: justify;"><a href="https://aws.amazon.com/outposts/"><b>AWS Outsposts</b></a></p>
<ul>
  <li><em> virtually any on-premises or edge location</em></li>
  <li>It brings AWS data center close to on-premises (racks)</li>
  <li>Hybrid cloud, fully managed infra, consistency</li>
  <li>Outposts Racks: Complete Rack (42 U rack) </li>
  <li>Outposts servers: 1U or 2U</li>
  <li>Low latency, local data, data residency, easier migration, fully managed service</li>
</ul>  

<p><center>
  <img src="/img/aws/global-infra.png" height="100%" width="100%">
</center></p>

<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/aws-global-infrastructure/">DigitalCloud Summary</a></li>
<li><a href="https://digitalcloud.training/aws-application-integration/">DigitalCloud - AWS Application Integration Services</a></li>
<li><a href="https://infrastructure.aws/">Regions and Availability Zones</a></li>



<!-- ############################################################### -->



<br />
<hr>
<br />

<h2 id="architect">AWS Well-Architectured Framework</h2>

<p style="text-align: justify;">AWS Well-Architectured Framework helps to build secure, high-performing, resilient, and efficient infrastructure <a href="https://digitalcloud.training/architecting-for-the-cloud/">[1]</a><a href="https://docs.aws.amazon.com/pdfs/wellarchitected/latest/framework/wellarchitected-framework.pdf">[2]</a><a href="https://aws.amazon.com/architecture/well-architected/">[3]</a><a href="https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf">[4]</a>.</p>

<p style="text-align: justify;">AWS Best Practices</p>
<ul>
  <li>Scalability (vertical and horizontal)</li>
  <li>Disposable Resources</li>
  <li>Automation (serverless, IaaS,etc)</li>
  <li>Loose Coupling</li>
  <li>Services not Server</li>
  <li>Design for failure -> Distributing workloads across multiple Availability Zones</li>
  <li>Provision capacity for peak load</li>
</ul>

<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html">Principles</a></p>
<ul>
  <li>Stop guessing the capacity needs</li>
  <li>Test systems at production scale</li>
  <li>Automate</li>
  <li>Evolutionary architecture</li>
  <li>Drive architecture using data</li>
  <li>Simulate applications for flash sale days</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/blogs/apn/the-6-pillars-of-the-aws-well-architected-framework/">Pillars</a>:</p> 
<ul>
  <li><a href="https://wa.aws.amazon.com/wat.pillar.operationalExcellence.en.html">Operational Excellence</a>: run and monitor system 
    <ul>
      <li>Design Principles: IaaC annotate doc; frequent, small, reversible changes; refine operations; anticipate failure; learn with failures</li>
      <li>Best Practices: creates, use procedures and validate; collect metrics; continuous change</li>
    </ul> 
  </li>
  <li><a href="https://docs.aws.amazon.com/wellarchitected/latest/security-pillar/welcome.html">Security</a>: protect information, systems and assets
    <ul>
      <li>Design Principles: strong identity foundation; traceability; apply at all layers; automate; protect data in transit and at rest; keep people away from data; prepare for security events</li>
      <li>Best Practice: control who do what; identify incidents; maintain confidentiality and integrity of data</li>
    </ul> 
  </li>
  <li><a href="https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html">Reliability</a>: system recover from infra or service disruptions 
    <ul>
      <li>Design Principles: test recovery procedures; automatically recover from failure; scale horizontally; stop guessing capacity; manage change in automation</li>
      <li>Best Practices: Foundations, Change Management, Failure Management</li>
      <li>Foundation Services: Amazon VPC, AWS Service Quotas; AWS Trust Advisor</li>
      <li>Change management: CloudWatch, CloudTrail, AWS Config</li>
    </ul> 
  </li>
  <li><a href="https://docs.aws.amazon.com/wellarchitected/latest/performance-efficiency-pillar/welcome.html">Performance Efficiency</a>: use compute resources efficiently 
    <ul>
      <li>Design Principles: democratize advanced technology; go global in minutes; experiment more often; Mechanical sympathy</li>
      <li>Best practices: Data-driven approach; review the choices;make trade-offs;</li>
    </ul> 
  </li>
  <li><a href="https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html">Cost Optimization</a>: run system to delivery value at the loest price 
    <ul>
      <li>Design Principles: adopt a consumption mode, measure overall efficinecy; stop spending money on data center operations; analyze and attribute expenditure; use managed and application level services to reduce cost</li>
      <li>Best Practices: using the appropriate services, resources, and configurations for the specific workloads</li>
    </ul> 
  </li>
  <li><a href="https://docs.aws.amazon.com/wellarchitected/latest/sustainability-pillar/cloud-sustainability.html">Sustainability</a> (shared responsibility): minimizing the environmental impacts of running cloud workloads
    <ul>
      <li>Design Principles: understand impacts; establish sustainability goals; maximize utilization; anticipate and adopt new solutions; use managed services; reduce downstream impact</li>
    </ul>
  </li>
</ul>


<!-- ################################################# -->


<br />
<hr>
<br />
<h2 id="iam">IAM - AWS Identity and Access Management</h2>

<p style="text-align: justify;">Identify AWS access management (IAM) capabilities. It is the AWS service to specify how people, tools and applications will access AWS services and data <a href="https://aws.amazon.com/iam/">[1]</a><a href="https://digitalcloud.training/aws-iam/">[2]</a><a href="https://docs.aws.amazon.com/accounts/latest/reference/managing-accounts.html">[3]</a>.</p>


<ul>
  <li><b>IAM</b> is a <b>Global</b> (not apply to regions) service used to control the access to AWS resources (authentication/authorization). It can be used to manage users, groups, access policies, user credentials, user pwd policies, MFA and API keys.</li>
  <li><a href="https://docs.aws.amazon.com/general/latest/gr/root-vs-iam.html"><b>Root</b></a> has <b>full administrative permissions</b> and complete access to all AWS services and resource.  <a href="https://docs.aws.amazon.com/accounts/latest/reference/root-user-tasks.html">Actions allowed only to root</a>: change account setting, close account, restore IAM permission, change or cancel AWS support plan, register as a seller, config S3 bucket to enable <a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html">MFA</a>, edit/delete S3 bucket policies.</li>
  <li>When a Identity Federation (AD, facebook, SAML, OpenID) is configured, IAM user account is not necessary</li>
  <li>Power User has alot of permission but not to manage groups and users in IAM.</li>
  <li>IAM Security Tool: 
    <ul>
      <li>IAM Credential Report (account-level): account's users and their credential status. Access it by IAM menu Credential Report</li> 
      <li><a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_access-advisor.html">IAM Access Advisor</a> (user-level): services permissions and last access. Access it by IAM User menu. Use it to identify unnecessary permissions that have been assigned to users.</li>
    </ul>
  </li>
</ul>

<p style="text-align: justify;"><b>User</b> is an entity (person or service) created without permissions (by default) with access to an AWS Accounts. They are create with NO access to any AWS services, only login to the AWS console. The permissions must be explicitly given. They log in using <em>user name</em> and <em>password</em>. They can change some configurations or delete resources in your AWS account. Users created to represent an application are known as "servoce accounts". It's possible to have 5000 users per AWS account.</p>

<p style="text-align: justify;"><b>Groups</b> are a way to organize the users (only) and apply <b>policies</b> (permissions) to a collection of users in the same time. A user can belong to multiple groups. Only users and cannot be nested (groups with groups). It is not an identity so cannot be referenced in policies.</p>

<p style="text-align: justify;"><b>Roles</b> delegate permissions. Roles are assumed by users, applications, and services. It can provides temporary security credentials (STS - Security Token Service) for customer role session. Also, the IAM roles make possible to access cross-account resources. It is a trusted entity.</p>

<p style="text-align: justify;">The <b>policy</b> manage access and can be attached to users, groups, roles or resources. When it is associated with an identity or resource it defines their permissions. It is a document written in JSON. The policy is evaluate when a user or role makes a request, and the permission inside that determine if the request is allowed or denied. The types of policies are:  identity-based policies (user, groups, roles), resource-based policies (resource), permissions boundaries (maximum permission), AWS Organizations service control policy (SCP)(maximum permission for an oganization), access control list (ACL), and session policies (AssimeRole* API action). <a href="https://docs.aws.amazon.com/en_us/IAM/latest/UserGuide/access_policies.html">Policy main elements</a>:
<ul>
  <li>Version</li>
  <li>Effect: allow/deny</li>
  <li>Action: type of action that should be allowed or denied</li>
  <li>Resource: specifies the object or objects that the policy statement covers</li>
  <li>Condition: circumstances under which the policy grants permission</li>
  <li>Principal: account, user, role, or federated user</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/blogs/database/using-iam-authentication-to-connect-with-pgadmin-amazon-aurora-postgresql-or-amazon-rds-for-postgresql/">IAM authentication</a> is just another way to authenticate the user's credentials while accessing the database.</p>

<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys"><b>Access keys</b></a> are used to programmatic access (API/SDK). It is generated through the AWS Console</p>

<p style="text-align: justify;"><b>SSH key</b> is an IAM feature to allow developer to access AWS services through the AWS CLI.</p>

<p><center>
  <img src="/img/aws/iam.png" height="90%" width="90%">
</center></p>

<p><a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html">Best Practices</a></p>
<ul>
    <li>Use IAM user instead of root user in regular activities</li>
    <li>Add user into groups</li>
    <li>Strong password</li>
    <li>Use MFA</li>
    <li>Create roles for permissions to AWS services</li>
    <li>User Access Keys for programmatic access (CLI/SDK)</li>
    <li>Audit permissions through IAM Credential Reports and IAM Access Advisor</li>
    <li>Protectect your access key</li>
    <li>Prefer customer managed policies (managed policies cannot be edited)</li>
    <li>Use roles for applications that run EC2 and to delegate permissions</li>
    <li>Rotate credentials</li>
    <li>Give only credentials that is really needed (Least privilege)</li>
</ul>


<p><b>Good Reads:</b></p>
<li><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html">IAM roles for Amazon EC2</a></li>
<li><a href="https://aws.amazon.com/iam/">AWS Identity and Access Management</a></li>
<li><a href="https://aws.amazon.com/blogs/database/using-iam-authentication-to-connect-with-pgadmin-amazon-aurora-postgresql-or-amazon-rds-for-postgresql/">Using IAM authentication to connect with pgAdmin Amazon Aurora PostgreSQL or Amazon RDS for PostgreSQL</a></li>
<li><a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html">Policies and permissions in AWS Identity and Access Management</a></li>
<li><a href="https://repost.aws/knowledge-center/iam-restrict-calls-ip-addresses">How can I use IAM roles to restrict API calls from specific IP addresses to the AWS Management Console?</a></li>
<li><a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html?icmpid=docs_iam_console">Set an account password policy for IAM users</a></li>
<li><a href="https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-iam-roles.html">Amazon ECS task IAM role</a></li>
<li><a href="https://aws.amazon.com/iam/features/manage-roles/">Manage IAM Roles</a></li>
<li><a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html">Policy evaluation logic</a></li>


<!-- #################################################### -->


<br />
<hr>
<br />
<h2 id="orgcontrolpower">AWS Organization and Control Tower</h2>

<p style="text-align: justify;"><b>AWS Organization</b><a href="https://aws.amazon.com/organizations/">[1]</a><a href="https://digitalcloud.training/aws-organizations/">[2]</a>: it is a collection of AWS accounts where is possible manage these accounts, apply polices, delegate responsibilities, apply SSO, share resources within the organization, use CloudTrail across the accounts.</p>

<ul>
  <li>It provides volume discounts or EC2 and S3 aggregated across the member AWS account.</li>
  <li><a href="https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/consolidated-billing.html">Consolidate billing</a>: bill for multiple accounts and volume discounts as usage in all accounts is combined, easy to tracking or charges across accounts, combined usege across accounts and sharing of volume pricing discounts, reserved instance discounts and saving plans.</li>
 </ul>

<p style="text-align: justify;"><b>Service Control Policies (SCPs)</b> is in AWS Organization and can control a lot of available permissions in AWS account, but NOT grant permissions. It can be used to apply the restrictions across multiple member accounts (deny rule). It affects only UAM users and roles (not resources policies)</p>    


<p style="text-align: justify;"><b>Control Tower</b>: is over organization and give support to some adicional features, as create Landing Zone (multi-account baseline) and CT will deploy it. it set up and govern a secure and compliant multi-account AWS environment. Monitor compliance through a dashboard. Supports Preventive Guardrail using SCP (e.g, restruct regions across accounts); and Detective Gardrail using AWS Config (e.g, identity untagged resources)</p>


<p><center>
  <img src="/img/aws/iam-org-ct.png" height="100%" width="100%">
</center></p>


<!-- ############################################## -->


<br />
<hr>
<br />
<h2 id="ec2">EC2 - Elastic Compute Cloud</h2>

<p style="text-align: justify;"><b>Amazon EC2</b> (Elastic Compute Cloud)<a href="https://aws.amazon.com/ec2/">[1]</a><a href="https://digitalcloud.training/amazon-ec2/">[2]</a> is a virtual machine that is managed by AWS.</p>
<ul>
  <li>A new instance combine CPU, memory, Storage and networking. The different <a href="https://aws.amazon.com/ec2/instance-types/">types</a> were created to optimize different use case. The t2.micro is an general example of a type of instance. The first letter 't' represent the instance class, the number '2' represents the generation, and the last part is the size. Each category try to balance different characteristics:
    <ul>
      <li>compute: require high performance (batch, media transcoding, HPC, machine learning, gaming) - Ex. C8g </li>
      <li>memory: process large data sets in memory (relational/non-relational database, distributed cache, in-memory database for BI, real-time unstructured data) - Ex. R8g </li>
      <li>storage: high, sequencial read and write access to large data sets on local storage (OLTP, relational/non-relational database, cache, data wharehouse, distributed file systems) - Ex. I4g</li>
      <li>networking </li>
    </ul>
  </li>
  <li><b>IaaS</b> (Infrastructure as a service)</li>
  <li>Secure, resizable compute capacity in the cloud. Designed to make web-scale cloud computing easier for developers</li>
  <li>It can run virtual server instances in the cloud</li>
  <li>Each instance can run Windows/Linux/MacOS</li>
  <li>It can storing data (EBS/EFS), distributing load (ELB), scaling services (ASG)</li>
  <li>Volumes: EBS (persist) and Instance Store (Non-Persistent)</li>
  <li>Bootstrap scripts: script that runs when the instance first runs (EC2 User data scripts). It can install updates, softwares, etc. Those scripts run with root user.</li>
  <li>Instance metadata is information about the instance. User data and metadata are not encrypted. The metadata is available at http://169.254.169.254/latest/meta-data</li>
  <li></li>
  <li>When the instance is stopped and started again the public IP will change. The private IP not change.</li>
  <li>If you have a legacy, the EC2 instance is a good solution to migrate to cloud that is right-sized (right amount of resources for the application)</li>
  <li>Key pair to access EC2: public key (stored in AQS) + private key file (stored locally). It is used to connect to EC2 instance.</li>
  <li>Get metrics in CloudWatch, logs in CloudTrail</li>
  <li><b><a href="https://fabiana2611.github.io/infra/aws-foundational#pricing">Pricing: </a></b>On-Demand, Reservation (Standard, Convertible and Shecule), Saving Plain, Spot, <a href="https://aws.amazon.com/ec2/dedicated-hosts/">Dedicated Host</a>, <a href="https://aws.amazon.com/ec2/pricing/dedicated-instances/">Dedicated Instance</a></li>
  <li><b>Shared Responsability</b>
    <ul>
      <li>AWS: Infrastructure (global network security), Isolation on physical hosts, Replacing hoardware, Compliance Validation</li>
      <li>Customer: Security Groups rules, OS patches and updates, Software and utilities installed on the EC2 instance, IAM Roles assigned to EC2 and IAM user access management, Data security on your instance.</li>
    </ul>
  </li>
</ul>

<p><center>
  <img src="/img/aws/ec2.png" height="100%" width="100%">
</center></p>

<p style="text-align: justify;">VMWare on AWS: for hybrid cloud, cloud migration, disaster recovery, leverage AWS</p>

<p style="text-align: justify;">Amazon EC2 <a href="https://aws.amazon.com/ec2/spot/">Spot Instances</a></p>
<ul>
  <li><em>Let you take advantage of unused EC2 capacity in the AWS cloud. Spot Instances are available at up to a 90% discount compared to On-Demand prices. You can use Spot Instances for various stateless, fault-tolerant, or flexible applications such as big data, containerized workloads, CI/CD, web servers, high-performance computing (HPC), and test & development workloads.</em></li>
  <li>Useful for workloads resilient to failure (batch, data analysis, Image processing, distributed workload, CI/CD and testing). However, it is not suitable for critical jobs or persistent workload and databases.</li>
  <li>Useful when workload is not immediate and can be stopped for a moment and continue from that point after</li>
  <li>Spot fleed: collection of spot on-demand. It will try and match the target capacity with your price restraints. Strategies: capacotyOptimized, lowestPrice, diversified, InstancePoolsToUseCount</li>
</ul>

<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/imagebuilder/latest/userguide/what-is-image-builder.html"><b>EC2 Image Builder</b></a></p>
<ul>
  <li>It creates Virtual Machine or container images</li>
  <li>Automate the creation, maintain, validate and test EC2 AMIs</li>
  <li>The execution can be scheduled and after the process the AMI can be distributed (multiple regions)</li>
</ul> 


<p style="text-align: justify;">EC2 Hibernate: suspende to disk. Hibernation saves the contents from RAM to EBS root volume. When start again, RBS root volume is restored; RAM contents are reloaded. Faster to boot up. Maxmin days an instance can be in hibernation: 60 days.</p>

<p><b>Storage:</b></p>
<ul>
  <li>
    <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html"><b>EC2 Instance Store</b></a> is an alternative to EBS with a high-performance hardware disk, better I/O performance. However, it lose their storage when they stop. So, the best scenarios to be used are, e.g, buffer, cache, temporary content.</li>
  <li>
    <b>EBS</b> - Amazon Elastic Block Store <a href="https://aws.amazon.com/ebs/">[1]</a><a href="https://digitalcloud.training/amazon-ebs/">[2]</a><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html">[3]</a><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/RootDeviceStorage.html">[4]</a>
    <ul>
      <li>EBS <b>Volume</b>: attached to one instance.</li> 
      <li>Designed for mission-critical workload</li>
      <li>High Availability: Automatically replicated within a single AZ</li>
      <li>Scalable: dynamically increase capacity and change the volume type with no impact</li>
      <li>The EBS volumes not need to be attached to an instance.</li> 
      <li>The EBS volumes cannot be accessed simultaneously by multiple EC2 instance (only with constrains)</li> 
      <li><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volumes-multi.html">Attach a volume to multiple instances with Amazon EBS Multi-Attach</a>: Same AZ, only to SSD volume, allowed only in some regions, and others restrictions</li> 
      <li>It allows the instance to persist data even after termination, however, Root EBS volumes are deleted on termination by default</li>
      <li>It can be mounted to one instance at a time and can be attached and detached from EC2 instance to another quickly. However it is locked to an AZ. To move to another AZ is necessary to create a <b>snapshot</b> and it can be copy across AZ or Region. </li>
      <li>A <a href="https://docs.aws.amazon.com/ebs/latest/userguide/ebs-snapshots.html">snapshot</a> is a backup of the EBS Volume at a point in time. The snapshots are stored on Amazon S3 and they are incremental. EBS Snapshot features are <b>EBS Snapshot Archive</b> and <b>Recycle Bin for EBS Snapshot</b>. The process with snapshots (creating, deletion, updates) can be automated with <b>DLM</b> (Data Lifecycle Manager).</li> 
      <li>It has a limited performance.</li> 
      <li><b>Pricing</b>: Volumes type (performance); storage volume in GB per month provisioned; Snapshots (data storage per month); Data Transfer (OUT)</li>
      <li>EBS Volume Types: 
        <ul>
          <li>gp2/gp3 (SSD): general puerpose; balance between price and performance; 3K IOPS and 125 MB/s (up to 16K IOPS and 1K MiB/s). Use cases: high performance at a low cost (MySQL, virtual desktop, Hadoop). </li> 
          <li>io1 (SSD): high perfomance and most expensive. 64K IOPs per volume, 50 IOPS per GiB. critical low latency or high throughput]; Use cases: large database, legacy</li>
          <li>io2 (SSD): Higher durability. 500 IOPS per GiB (same price of io1). I/O intensive apps, large database</li>
          <li>st1(HDD): low cost, frequently accessed and thoughput intensive workload (big data, data warehouse); </li>
          <li>sc1 (HDD): lowest cost; less frequently accedded]. Onlys SSDs can be boot volume.</li>
        </ul>
      </li>
      <li>Encryption: use KMS; if the volume is created encrypted the data in trasit is encrypted, the snapshots are encrypted, the volumes created from snapshots are encrypted. A copy of an uncrypted volume can be encrypted.</li>
    </ul>
  </li>
  <li>
    <b>EFS</b><a href="https://aws.amazon.com/efs/">[1]</a><a href="https://docs.aws.amazon.com/efs/latest/ug/awsbackup.html">[2]</a><a href="https://digitalcloud.training/amazon-efs/">[3]</a> - Amazon Elastic File System</p>
    <ul>
      <li>Network File System (NFS) for Linux instances in multi-AZ.</li>
      <li>Shared File storage service using EC2.</li>
      <li>It is considered highly available, scalable, expensive, pay per use.</li>
      <li>Expensive</li>
      <li>EFS Infrequent Access (EFS-IA) is a storage class that is cost-optimized for files not accessed and has lower cost than EFS standard. It is based on the last access. You can use a policy to move a file from EFS Stanrd to EFS-IA.</li>
      <li>Encryption at rest using KMS</li>
      <li>Pay per use</li>
      <li>Tiers: frequent access and not frequent access</li>
      <li>For linus instance and linux-based applications</li>
    </ul>
  </li>
  <li> <a href="https://aws.amazon.com/fsx/windows/">Amazon FSx</a>
    <ul>
      <li>for Windows File Server: fully managed Microsoft Windows file servers, manage native Microsoft windows file system. Make the migration easy</li>
      <li>for Lustre: managed file system that is optimized for compute-intensive workloads (HPC, Machine Learning, Media data Processing). Fo Linux File System. It can store data in S3.</li>
    </ul>
  </li>
</ul>    


<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html">Amazon <b>AMI</b></a> (Amazon Machine Image)</p>
<ul>
  <li>Template of root volume + laung permissions + block device mapping the volumes to attach</li>
  <li>Launch EC2 one or more pre-configured instance </li>
  <li>It can be customized </li>
  <li>it is build for a specific region. The AMI must be in the same region as that of the EC2 instance to be launched; but can be copied to another one where want to create another instance.</li>
  <li>An EBS snapshot is created when an AMI is builded</li>
  <li>It can be copied to other regions by the console, command line, or the API</li>
  <li>Category:
    <ul>
      <li>Amazon EBS: created from an Amazon EBS snapshot. It can be stopped. The data is not lost if stop or reboot. By default, the root device volume will be deleted on termination</li>
      <li>Instance Store: created from a template stored in S3. If delete the instance the volume will be deleted as well. If the instance fails you lose data, if reboot the data is not lost. It cannot stop the volume.</li>
    </ul>
  </li>
</ul> 


<p><b>Network:</b></p>
<ul>
  <li>ENI (Elastic Network Interface): Virtual Network card
    <ul>
      <li>Attributes: Primary and secondary IPv4 address, Elastic IPv4, public IPv4/IPv6, security group, MAC address, source/destination check flag, description</li>
      <li>Attached to instances</li>
      <li>eth0 is ENI created when an Ec2 instance is launched</li>
      <li>Use cases: create a management network; use network and security compliances in your VPC; create dual-homed instances with workloads/roles on distinct subnets; create a low-budget, high-availability solution</li>
    </ul>
  </li>
  <li>ENL (Enhaneed Networking): uses single root I/O virtualization (SR-IOV) to provide high performance (1-Gbps - 100 Gbps)
    <ul>
      <li>ENA (Elastic Network Adapter): it enable Enhanced network which provides higher bandwidth, higher packet-per-second (PPS) performance, and consistently lower inter-instance latencies (up to 100 Gbps)</li>
      <li>VF (Intel 82599 Virtual Function Interface): For older instances (up to 10 Gbps)</li>
    </ul>  
  </li>
  <li>EFA (Elastic Fabric Adapter): ENA with more capabilities. It is a network interface for Amazon EC2 instances that enables customers to run applications requiring high levels of inter-node communications at scale on AWS. </li>
</ul>

<p><a href="https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html"><b>Security Group</b></a>:</p>
<ul>
  <li>It operates at instance level (can be attached to multiple instances) and are applied to the network security, controlling the traffic into or out of the EC2 instance, acting like a firewall (by default, inbound traffic is blocked and outbound traffic is authorised).</li>
  <li>Virtual firewall to ENI/EC2 instance</li>
  <li>Control how traffic is allowed into or out of EC2 instance (ALLOW rule -IP and other security groups)</li>
  <li>It contains only <b>rules</b> and these rules can reference by IP or by security group. They are stateful and locked down to a region/VPC combination.</li> 
  <li>Protect against low level network attack like UDP floods.</li>
  <li>They regulate access to Ports and authorised IP ranges.</li>
  <li>A good practices is to create a separate security group for SSH access.</li>
  <li>Tips: errors with time out is a security group issue; error of connection refused can be an application error.</li>
</ul>


<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html"><b>Placement groups:</b></a> It is an strategy of optimization to meet the needs of your workload which you can launch a group of interdependent EC2 instances into a placement group to influence their placement. It can be: </p>
<ul>
  <li><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-strategies.html#placement-groups-cluster">Cluster</a>: grouping of instances within a single AZ. Low latency and high throughput. It can't span multiple Azs</li>
  <li><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-strategies.html#placement-groups-partition">Partition</a>: set of racks that each rack has its own network and power source. Multiple EC2 instance</li>
  <li><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-strategies.html#placement-groups-spread">Spread</a>: group of instances that are each placed on distinct underlying hardware. Small number of critical instances that should be separate from each other. A spread placement group can span multiple Availability Zones in the same Region. You can have a maximum of seven running instances per Availability Zone per group. </li>
</ul>

<p><center>
  <img src="/img/aws/placementgroup.png" height="90%" width="90%">
</center></p>

<p style="text-align: justify;"><b>EC2 Pricing:</b> the price for it depends the instance (number, type), load balance, IP adreess, etc. You can use AWS Pricing Calculator to simulate to cost.</p>
<ul>
  <li><b>On-Demand:</b> short workload, predictable pricing, billing per second/hour, pay for what you use, no long-term commitment, highest cost, no discount. Best use to <b>short-term and un-interrupted worloads</b>.</li>
  <li><b>Reservations (1-3 years):</b> predicted workload. Various services like Ec2, DynamoDB, ElastiCache, RDS and RedShift. Pay up Front.
    <ul>
      <li><b>Reserved instances (RI)</b>: long workloads; has a big discount and has as scope Regional or Zonal. Indicated for steady-state usage application. It cannot be interrupted <a href="https://aws.amazon.com/ec2/pricing/reserved-instances/">(up to 72% off the on-demand price)</a></li> 
      <li><a href="https://docs.aws.amazon.com/whitepapers/latest/cost-optimization-reservation-models/standard-vs.-convertible-offering-classes.html"><b>Convertible Reserved Instances</b></a>: long workload with flexible instances; gives a big discount. This model change the attributes of the RI as long as the exchange results in the creation of RIs of equal or greater value (up to 54% off the on-demand price)</li>
    </ul>
  </li>
  <li><b>EC2 <a href="https://aws.amazon.com/savingsplans/pricing/">Savings Plain</a></b>: reduce compute cost based on long term (1-3y). Locked to a specific instance family and region. Lot of flexibility (EC2, Fargate, Lambda). No Upfront or Partial Upfront or All Upfront Payments</li> 
  <li><b>Spot Instance:</b> High discount (up to 90%). It is the most cost-efficient instances in AWS. Urgent Capacity; Flexible; Cost Sensitive. Use for app with flexible start and end times; app with low compute prices (Image rendering, Genomic sequence). Not use if need a guarantee of time.</li> 
  <li><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-hosts-overview.html"><b>Dedicated host</b></a> (single customer, your VPC): physical server with EC2 instance dedicated, can use your own licenses. It can be purchasing <b>On-Demand</b> or <b>Reserved</b>. It is the most expensive.</li> 
  <li><b>Dedicated Instance</b>: single customer, isolated hardware dedicated to your application, but this hardware can be shared with other instances in the same account. Compliance, Licensing, on-Demand, Reserved.</li>
  <li><a href="https://aws.amazon.com/blogs/aws/new-per-second-billing-for-ec2-instances-and-ebs-volumes/">Minimum charge</a>: one-minute for Linux based EC2 instances.</li>    
</ul>

<p><b>Aditional References:</b></p>
<ul>
  <li><a href="https://digitalcloud.training/aws-compute-services/">DigitalCloud Summary</a></li>
  <li><a href="https://aws.amazon.com/ec2/instance-types/">Instance Types</a></li>
  <li><a href="https://aws.amazon.com/aws-cost-management/aws-cost-optimization/right-sizing/">Right Sizing</a></li>
  <li><a href="https://instances.vantage.sh/">Instance Types - Vantage</a></li>
</ul>


<!-- ###################################################### -->


<br />
<hr>
<br />
<h2 id="asg">High Availability and Scaling</h2>

<p style="text-align: justify;">These are features <a href="https://digitalcloud.training/auto-scaling-and-elastic-load-balancing/">[1]</a> to be used to ensure elasticity and high availability. They can be used together.</p>

<p><b>Scalability</b></p>
<ul>
  <li>Handle greater loads by adapting</li>
  <li><b>Scale Up</b>: scale by adding more power (CPU/RAM) to existent machine/node. Operation running on only one computer.</li>
  <li><b>Scale Out</b>: scale by adding more instance to existent pool of resources.  Fault Tolerance is achieved by scale out operation.</li>
  <li><b>Scale In</b>: decrease the number of instances.</li>
  <li><b>Vertical</b>: inscrease the size of the instance. Common for non distributed system. Limited, e.g, by hardware.</li>
  <li><b>Horizontal</b> <a href="https://wa.aws.amazon.com/wat.concept.horizontal-scaling.en.html">[1]</a>: increase the number of instances. Distributed system. Common for web applications. Auto Scaling Group and Load Balancer <a href="https://digitalcloud.training/auto-scaling-and-elastic-load-balancing/">[1]</a>. Instances that are launched by your Auto Scaling group are automatically registered with the load balance<a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-load-balancer.html">[2]</a>.</li>
  <li><b>High Availability</b>: Direct relatioship with horizontal scalability. No interruption even with failover. Run across <a href="https://aws.amazon.com/rds/features/multi-az/">multi AZ</a>, at least in 2 AZ</li>
</ul>

<p>Set Up</p>
<ul>
  <li><a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/LaunchTemplates.html">Launch Template</a> -> all the settings needed to build an EC2 instance; for all EC2 auto scaling features; supports versioning; more granularity; recommended. The specification of a network interface has considerations and limitations that need to be taken into account in order to avoid errors. <a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-launch-template.html#change-network-interface">[1]</a></li>
  <li>Launch Configuration: only certain EC2 Auto Scaling feature; immutable; limited configuration options; specific use cases</li>
</ul>


<p style="text-align: justify;">Auto Scaling: create and remove instance when is necessary. It can use a launch configuration (an instance configuration template) that an Auto Scaling group uses to launch Amazon EC2 instances. <a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html">[1]</a><a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/launch-configurations.html">[2]</a><a href="https://aws.amazon.com/autoscaling/">[3]</a> </p>

<ul>
  <li>ASG contains a collection of EC2 instance (logical group)</li>
  <li>Replace unhealthy instances. </li> 
  <li>Only run at an optimal capacity.</li>
  <li>AWS EC2 Auto Scaling provides elasticity and scalability.</li>
  <li>High availability can wi achieve with Auto Scaling balancing your EC2 count across the AZs <a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html">[1]</a>
  <li>Scaling Policies: minumum, maximum and <a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/asg-capacity-limits.html).">desired capacity</a> 
    <ul>
      <li>Step scaling policy: launch resources in response to demand. It's not a guarantee the resources are ready when necessary</li>
      <li>Simple Scaling Policy: Relies on metrics for scaling needs, e.g., add 1 instance when CPU utilization metric > 70%.</li>
      <li>Target Tracking Policy: Use scaling metrics and value that ASG should maintain at all times, e.g, Maitain ASGAverageCPUUtilization equal 50%</li>
    </ul>
  </li>
  <li><b>Instance Warm-Up</b>: stops instances behind load balancer, failing the helath check and being terminated prematuraly</li>
  <li><b>Cooldown</b>: pause AS for a set amount of time to not launch or terminate instances; </li>
  <li><b>Avoid Thrashing</b>: create instance very fast</li>
  <li>Scaling types: 
    <ul>
      <li>Reactive scaling: Monitors and automatically adjusts the capacity; predictable performance at the lowest possible cost. It, e.g, add/remove (Scale out/in) EC2 instances when the load is increased/decreased. </li>
      <li>Scheduled Scaling (predictable workflow) <a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/schedule_time.html">[1]</a> can be configured for known increase in app traffic.</li> 
      <li>Predictive Scaling: uses daily and weekly trends to determine when scale</li>
    </ul>
  </li>
  <li><b>Strategy</b>: Manual or Dynamic (1. SimpleStep Scaling (CloudWatch); 2.Target Tracking Scaling; 3. Scheduled Scaling</li>
</ul> 

<p style="text-align: justify;">Scaling Relational Database</p>
<ul>
  <li>Vertical Scaling: resize the database</li>
  <li>Scaling Storage: resize storage to go up, but is not able scale back down (RDS, Autora)</li>
  <li>Read Replicas: realy only copies to spread out the workload. Use multiple zones.</li>
  <li>Aurora Serverless: offload scaling to AWS. Unpredictable workloads. Aurora is the only engine that offers a serverless scaling option. <a href="https://aws.amazon.com/rds/aurora/serverless/">[1]</a></li>
</ul>

<p style="text-align: justify;">Scaling Non-Relational Database</p>
<ul>
  <li>AWS do this</li>
  <li><a href="https://aws.amazon.com/dynamodb/pricing/provisioned/">Provisioned</a>: predictable workflow; need tp review past usage to set upper and lower scaling bounds; most cost-effective model</li>
  <li><a href="https://aws.amazon.com/dynamodb/pricing/on-demand/">On-Demand</a>: sporadic workflow; less cost effective;</li>
  <li>Read Capacity Unit (RCU): DynamoDB unit of measure for reads per second for an item up to 4KB in size. As an example: if you have objects that are 7KB in size, then will be necessary 2 RCU for 1 strongly consistent read per second (1 RCU = 4KB/1 Strongly Consistent Read -> 2 RCU = 8KB)</li>
  <li>Write Capacity Unit (WCU): DynamoDB unit of measure for writes per second for an item up to 1KB in size. As an example: if you have an object that are 3KB in size, then will be necessary 3 WCU (1 WCU = 1KB * Write per Second -> 3 KB * 1 WCU = 3 WCUs ) </li>
</ul>

<p><center>
  <img src="/img/aws/asg.png" height="100%" width="100%">
</center></p>


<p style="text-align: justify;">Disaster Recovery</p>
<ul>
  <li>RPO - Recovery Point Objective: point in time to recover (24h, 5 minutes, etc)</li>
  <li>RTO - Recovery Time Objective: how fast to recover; how long the business support</li>
  <li>Strategies
    <ul>
      <li>Backup and Restore: Restore from a snapshot (Chepest but slowest)</li>
      <li>Pilot Light -  not consume the same level; provision 100% of the services to keep the applications up (faster than backup and restore but some downtime)</li>
      <li>Warm Standby - provision the services neceaary to keep the applications up (quicker recovery time than Pilot Light but more expensive)</li>
      <li>Strategy: Active/Active Failover: is necessary to have a complete duplicated services (the most expensive but no downtime but lowest RTO and RPO)</li>    
    </ul>
  </li>
  
</ul>


<!-- ##################################################### -->


<br />
<hr>
<br />

<h2 id="network">AWS networking services</h2>


<p id="vpc" style="text-align: justify;"><b><u>VPC</u></b> (Virtual Private Cloud): isolated network in AWS cloud that can ne fully customizid<a href="https://aws.amazon.com/vpc">[1]</a><a href="https://digitalcloud.training/amazon-vpc/">[2]</a><a href="https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html">[3]</a>. It is a virtual data center. A range of IP<a href="https://cidr.xyz/">[4]</a><a href="https://www.ipaddressguide.com/cidr.aspx">[5]</a> is defined when the VPC is created</p>
<ul>
  <li><b>Subnet</b>: partition the network inside the VPC and AZ. The public is accessible from the internet.  Instances are launch into subnets. Two subnets configured in one AZ (High avalilability)</li>
  <li><b>Elastic IP</b>: static IP to a public IP to EC2 instance</li>
  <li><b>Route Tables</b> make possible the access of the internet and between subnets.</li>
  <li><b>Internet Gateways</b>: helps VPC to connect to internet. The public subnet has a route to the internet gateway, but private subnet does NOT have a route to Internet Gateway.</li>
  <li><b>NAT Gateway</b><a href="https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html">[1]</a> (AWS-managed) and <b>NAT instance</b><a href="https://docs.aws.amazon.com/vpc/latest/userguide/VPC_NAT_Instance.html">[2]</a> (self-managed): allows the instance inside the private Subnets to access the internet or other services. But denying inbound traffic from internet. It is Reduntand inside AZ; no need to patch; automatically assigned a public IP; and it's not associated with security groups. NAT instance supports port forwarding</li>
  <li><b>VPC Endpoint</b><a href="https://docs.aws.amazon.com/vpc/latest/userguide/vpce-gateway.html">[1]</a>: connect to AWS services using private Network. It can be combined with PrivateLink and is not necessary NAT, gateways,etc. It is not leavinf AWS environment. They are horizontaly scaled, redundant, and highly available. Types: Interface endpoints (elastic network interface with private IP - supports many services) and Gateway Endpoints (virtual device you provision, similar to NAT GW - supports connection to S3 and DynamoDB)</li>
</ul>

<p><b><u>VPC Security</u></b></p>
<ul>
  <li><b>Network ACL</b> (Access Control List): it is the first line of defense. It is subnet level: firewall to subnets (only IP), controlling traffic in and out of one or ore subnets. <u>Stateless</u>: have to allow inbound and outbound traffic (checks for an allow rule for both connections). Supports allow and deny rules. Customer is responsible for configure it. The default ACLs allows all outbound and inbound traffic. The custom ACL denies inbound and outbound traffic by default. A subnet will be associated with the default ACL. A subnet is associated with only one ACL but ACL can be associated with multiple subnets. Rules are evaluating in order starting with the lowest number rule (first match wins).</li>
  <li><b>Security Group</b> (SG): Virtual firewall for EC2 instance. <u>Stateful</u>: if there is an inbount rule that allow the traffic, the outbound automatically allowed without rules; if the outgoing request is done by instance and the rule allow the outbound traffic then the inbound return is automatically allowed. Supports only allow rules. Security Groups can be associated with a NAT instance. The rules are evaluated before deciding whether to allow traffic.</li>  
</ul>

<p><b><u>VPCs Connections</u></b></p>
<ul>
  <li><b>VPC Peering</b> <a href="https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html">[1]</a> - connect two VPC via direct network route using private IP; cross account and region, no transitive peering, must not have overlapping CIDRS. It can use Security Group cross account but not cross region. </li> 
  <li><b>PrivateLink</b> provides private connectivity between VPCs, AWS services, and your on-premises networks, without exposing your traffic to the public internet. It is the best option to expose a service to many of customer VPC. It does not need VPC peering, or route tables or Gateways. It needs a Network Load Balancer (NLB) on the service VPC and an ENI on the customer VPC.</li>
  <li><b><u>Security</u></b>: VPM CloudHub: Multiple sites with its own VPN connection. The traffic os encrypted.</li>
  <li><b>VPN</b> - Virtual Private Network<a href="https://aws.amazon.com/vpn/">[1]</a>:
    <ul>
      <li>Establish secure connections between your on-premises networks, remote offices, client devices, and the AWS global network</li>
      <li><b><a href="https://docs.aws.amazon.com/vpn/latest/s2svpn/how_it_works.html">Site to Site VPN</a></b>: connect (encrypted) on premises VPN to AWS. Over the public internet</li>
      <li><b>AWS Managed VPN</b>: Tunnels from VPC to on premises</li>
      <li><b>VPN Gateway</b>: connect one VPC to customer network</li>
      <li><b>Customer Gateway</b>: installed in customer network</li>
      <li><b>Client VPN</b>: connect to your computer using OpenVPN. Connect to EC2 instance over a private IP.</li>
    </ul>
  </li>
  <li><b>Direct Connect (DX)</b><a href="https://aws.amazon.com/directconnect/">[3]</a><a href="https://digitalcloud.training/aws-direct-connect/">[4]</a>: physical connection (private) between on premises and AWS. Types: dedicated network connection (physical ethernet connection associated with a single customer) or hosted connection (provisioned by a partner). No public internet. The company should use AWS Transit Gateway. Using only DX data in transit is not encrypted but is private; DX + VPN privides an IPSec-encrypted private connection. Resuliency: Use two Direct Connection locations each one with two independent connections.</li>
  <li><b>AWS Transit Gateway</b> <a href="https://aws.amazon.com/transit-gateway/">[1]</a>: connect VPC and on-premise netowrk using a central hub working as a router. It allows a transitive peering; works on a hub-and-spoke model; works on a regional basis (cannot have it across multiple regions but can use it across multiple accounts.)</li>
  <li><b>Site-To-Site VPN</b>: it connects two VPCs via VPN. It needs Virtual Private Gateway (VGW), a VPN concentrator on the AWS side of VPN connection; and a customer Gateway (CGW) in the customer side of the VPN. It can be used as a backup connection in case DX fail.</li>
</ul>

<p style="text-align: justify;">5G Networking with <a href="https://aws.amazon.com/wavelength/"><b>AWS WaveLength</b></a>: Infrastructure embedded within the telecommunication provides datacenters at 5G network</p>

<p><a href="https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html">VPC Flow Logs</a>: capture information about the IP traffic going to and from network interfaces in your VPC. For this is necessary to configure the Bastion Host security Group to allows inound from internet on port 22.</p>

<p><b>Bastion Host</b> is a instance in public subnet that handle the communication between internet and one or more EC2 instance in a private subnet via ssh.</p>

<p style="text-align: justify;"><b>VPC sharing</b> <em> allows multiple AWS accounts to create their application resources into shared and centrally-managed Amazon VPCs. To set this up, the account that owns the VPC (owner) shares one or more subnets with other accounts (participants) that belong to the same organization from AWS Organizations. After a subnet is shared, the participants can view, create, modify, and delete their application resources in the subnets shared with them. Participants cannot view, modify, or delete resources that belong to other participants or the VPC owner. You can share Amazon VPCs to leverage the implicit routing within a VPC for applications that require a high degree of interconnectivity and are within the same trust boundaries. </em><a href="https://docs.aws.amazon.com/vpc/latest/userguide/vpc-sharing.html">[1]</a></p>


<p style="text-align: justify;"><b>Route 53</b><a href="https://digitalcloud.training/amazon-route-53/">[1]</a><a href="https://medium.com/@kinnarisutaria9/getting-started-with-amazon-route-53-e10f93165a6a">[2]</a>: Global Managed DNS. Helth check. Reliability and cost-effective way to route end users.</p>
<ul> 
  <li>It is a DNS supported by AWS:
    <ul>
      <li>DNS: Convert name to IP</li>
      <li>TTL: time to live</li>
      <li>CNAME (canonical name): map a domain name to another domain name. CAnnot be used for naked domain names</li>
      <li>Alias: Map a host name to an AWS resource. You can't set TTL and cannot set an ALIAS record for an EC2 DNS name.</li>
      <li>Record/alias can be used to naked domain names.</li>
      <li>DNS: Port 53</li>
      <li>DNS does not route any traffic but responds to the DNS queries</li>
    </ul>
  </li>
  <li>It is a hybrid architecture.</li>
  <li>It's not possible to extend Route 53 to on-premises instances.</li>
  <li>Paied for hosted zone, queries, traffic flow, helth checks, domain name. </li>
  <li>Policies:
    <ul>
      <li><b>Weighted routing policy</b><a href="https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html">[1]</a> is used to route traffic to multiple resources (associated with a single domain/subdomain) and to choose how much traffic is routed to each resource (split traffic based on different weights assigned). It can be used, e.g, for load balancing purpose. Assigning 0 to a record will stop the traffic to that resource. Assigning 0 to all records then all records returns equally.</li>
      <li><b>Simple Routing Policy</b> route the traffic to a single resource. It allows one record with multiple IP; if the record is multiple value the Route 53 returns all values to the user in a random order. Failover Routing Policy: used when you want to create an active/passive set up. It cannot be associated with Health Checks.</li>
      <li><b>Geolocation Routing Policy</b>: choose where the traffic will be sent based on the geographic location of the <u>users</u> (which DNS queries originate). Also, can restrict distribution of content. </li>
      <li><b>Geoproximity Routing</b>: based on geographic location of the <u>resources</u>, and can choose to route more traffic to a given resource. </li>
      <li><b>Latency Routing Policy</b>: based on the lowest network latency for the end user (which regions will give them the fastest response time)</li>    
      <li>Failover routing policy: use primary and standby configuration that sends all traffic to the primary until it fails a health check and sends traffic to the secondary. This solution does not good enough for lowest latency</li>
    </ul>
  </li>
  <li><em>An AWS DNS alias record is a type of record that points a domain name to an AWS resource, such as an Elastic Beanstalk environment, an Amazon CloudFront distribution, or an Amazon S3 bucket. It is used to create subdomains or point a domain name to a different AWS service. Reference: Values for Alias Records </em> <a href="https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-values-alias.html">[1]</a></li>
  <li>Health Checks: Only for public resources</li>
</ul>

<p><center>
  <img src="/img/aws/network.png" height="100%" width="100%">
</center></p>

<p style="text-align: justify;"><b>ELB</b> (Elastic Load Balancer): distribute the traffic across healthy instances with targets. <a href="https://aws.amazon.com/elasticloadbalancing/">[1]<a href="https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-update-security-groups.html">[2]</a></p>
<ul>
  <li>It can be across multiple AZs but Single Region</li>
  <li>Internal (private) or external (public)</li>
  <li>Servers that handle the traffic and distribute it across, e.g., EC2 instance, containers and IP address.</li>
  <li>It has only one point of access (DNS). </li>
  <li>It do the health check<a href="https://docs.aws.amazon.com/elasticloadbalancing/latest/application/target-group-health-checks.html">[2]</a></li>
  <li>Benefits: High availability across zones, automatic scaling and Fault Tolerance.</li>
  <li>AWS responsibilities: guarantees it will work, upgrade, maintenance, high availability</li>
  <li>Types:
    <ul> 
      <li><b>ALB</b> (Application Load Babancer / Inteligent LB): HTTP/S; Static DNS (URL); Layer 7; It is a single point of contact for client. ALBs allow you to route traffic based on the contents of the requests. Distributes incoming application traffic across multiple targets in multiple AZ. Good for microservices and container-based application</li>
      <li><b>NLB</b> (Network Load Balancer / Performance LB): high performance/low latency (TCP/UDP); static IP throught Elastic IP; layer 4 (connection level). It distributes traffic. When the NLB has only unhealthy registered targets, the Network Load Balancer routes requests to all the registered targets, known as fail-open mode.</li> 
      <li><b>GLB</b> (Gateway Load Balancer / Inline Virtual Appliance LB): route traffic to firewalls managing in EC2 instance (Layer 3); Classic Load Balancer (Layer 4 and 7)</li>
      <li><b>Classic</b>: layer 4/7; more used to test or dev. 504 error means gateways has time out</li>
    </ul>
  </li>
  <li>Sticky Session: redirect to the same instance. Use cookies (LB or Application). <em>Stickiness allows the load balancer to bind a user's session to a specific target within the target group. The stickiness type differs based on the type of cookie used. Can't be turned on if Cross-zone load balancing is off.</em></li>
  <li><b>Shared responsibility</b>: AWS is responsable to keep it working, upgrade, maintain, and provide only few configurations.</li>
</ul>

<p><center>
  <img src="/img/aws/lb.png" height="100%" width="100%">
</center></p>


<p><b><u>Performance</u></b></p>

<p style="text-align: justify;"><b>AWS Global Accelerator</b><a href="https://aws.amazon.com/global-accelerator/">[1]</a><a href="https://digitalcloud.training/aws-global-accelerator/">[2]</a></p>
<ul>
  <li>Improve global application availability and performance</li>
  <li>Optimize the rote</li>
  <li>Use Edge Locations to the traffic</li>
  <li>Global Network</li>
  <li>Integration with Shield for DDoS protection</li>
  <li>No caching and has proxy packets at the edge</li>
  <li>Improve performance over TCP/UDP</li>
  <li>Good when use static IP and need determinist and fast regional failover.</li>
  <li>Target: EC2 instances or ALB</li>
</ul>

<p style="text-align: justify;"><b>Amazon CloudFront</b><a href="https://aws.amazon.com/cloudfront/">[1]</a><a href="https://digitalcloud.training/amazon-cloudfront/">[2]</a>: Global Content Delivery Network (CDN)</p>
<ul>
  <li>Replicate part of your application to AWS Edge Locations (content is served at the edge). </li>
  <li>Edge location: location to cache the content</li>
  <li>It can use cache at the edge to reduce latency. Improves read performance. </li>
  <li>DDoS protection, integration with Shield, Firewall</li>
  <li>S3 bucket: distribute files and caching at the edge, security with OAC (Origing Access Control)</li>
  <li>Customer origin: ALB, EC2 instance, S3 website</li>
  <li>It's a global service</li>
  <li>Can be integrated with CloudTrail</li>
  <li>Great for static content that must be available everywhere; in oposite of S3 Cross Region Replication that is great for dynamic content that needs to be available at low latency in few regions</li>
  <li><b>Pricing</b>: Traffic distribution; Requests; Data transfer out. Price is different for region</li>
</ul>


<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/aws-networking-services/">DigitalCloud Summary</li>
<li><a href="https://digitalcloud.training/aws-content-delivery-and-dns-services/">(DigitalCloud) AWS Content Delivery and DNS Services</a></li>
<li><a href="https://docs.aws.amazon.com/vpc/latest/userguide/security.html">VPC Security</a></li>


<!-- ############################################# -->


<br />
<hr>
<br />

<h2 id="storage">AWS Storage Services</h2>

<p style="text-align: justify;">There are three categories to storage services:</p>
<ul>
  <li>File storage: storage files in a hierarchy</li>
  <li>block storage: storage in a fixed sze blocks. Any change only a block is changed</li>
  <li>object storage: storage as a object. Any change then all the opject is changed</li>
</ul>

<h3>S3</h3>

<p style="text-align: justify;"><b>S3</b><a href="https://digitalcloud.training/amazon-s3-and-glacier/">[1]</a><a href="https://aws.amazon.com/s3/">[2]</a> is an AWS Storage service</a> for object. It allows store and retrieve data from anywhere at a low cost. Basically for static files. The files are storage in bukets and is highly available and highly durable. Data is stored redundantly across multiple AZs. The name must be global unique name even the bucket is regional level. S3 is design for Frequent Access.</p>

<p style="text-align: justify;">As characteristics, S3 offer different storage classes for different use cases (Tiered Storage); it has a lifecycle Management automatically to move the objects between different storage tiers or delete them through rules to be more cost effective; and use versions to retrieve old objecs. Also, it has a Strong Read-After-Write Consistency.</p>

<ul>
  <li>Object store and global file system.</li>
  <li>Used to store any files until 5TB without limits in buckets (directories/containers)</li>
  <li>These objects have a key.</li>
  <li>You can have version of the objects (bucket level)</li>
  <li>Virtually unlimited amount of online highly durable object storage. </li>
  <li>Each <b>bucket</b> is inside of a region</li>
  <li><a href="https://aws.amazon.com/s3/storage-classes/">Classes</a>: 
    <ul>
      <li><b>Standard</b>: frequently accessed</li> 
      <li><b>Standard-IA</b>: infrequently accessed but require rapid access. Low per GB storage price and per GB retrieval fee</li>
      <li><b>Intelligent-Tiering</b>: optimize costs by automatically moving data to the most cost-effective access tier, without performance impact or operational overhead. One tier that is optimized for frequent access and another lower-cost tier that is optimized for infrequent access. More expensive than Standard-IA.</li>
      <li><b>One Zone-IA</b>: lower cost</li> 
      <li><b>Glacier</b>: archived data; <b>pay for what you need</b>. Read and write</li>
      <li><b>Glacier Deep Archive</b>: lower cost for <b>long term retention</b>. Also can be used to backup and disaster recovery. Retrieval time of 12-48 hours. Financial Service, Health care and Public sectors.</li>
    </ul>
  </li> 
  <li><b>Features</b>: Transfer acceleration (CloudFront), Requester payes, Events (SNS, SQS, Lambda), Static website hosting, Encryptation, <a href="https://aws.amazon.com/s3/features/replication/">Replication (Cross-Region Replication - CRR; Same-Region Replication - SRR)</a></li>
  <li><b>Write-once-read-many</b> (WORM) - prevention of deletion or overwritten</li>
  <li>Use cases: backup, disaster recovery, archive, application hosting, media hosting, Software delivery, static website</li>
  <li><b>Security</b>: User-Based (IAM Policies), Resource-Based (<a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-iam-policies.html">Bucket Polices)</a>, Object/Bucket Access Control List (ACL), Encryptation</li>
  <li><a href="https://docs.aws.amazon.com/AmazonS3/latest/dev/Versioning.html">Versioning:</a> stores all versions of an object </li>
  <li>Performance: <a href="https://docs.aws.amazon.com/AmazonS3/latest/dev/transfer-acceleration.html">S3 Transfer Acceleration:</a> Accelerate global uploads & downloads into Amazon S3; and Increase transfer speed to Edge Location (enables fast, easy, and secure transfers of files over long distances between your client and your Amazon S3 bucket) </li>
  <li><a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/replication.html">Replication:</a> CRR and SRR</li>
  <li><a href="https://aws.amazon.com/premiumsupport/knowledge-center/move-objects-s3-bucket/">Move Objects</a></li>
  <li><b>Shared Responsibility</b>
    <ul>
      <li>AWS: Infrastructure (global security, durability, availability), Configuration and vulnerability analysis, Compliance validation, AWS employees can't not access the customer data, separation between customers</li>
      <li>Customer: version, bucket policies, replication, logging and monitoring, storage class, data encryptation, IAM user and roles</li>
    </ul>
  </li>
  <li><b>Pricing</b>: Depends the storage class; storage quantity; number of request; transition request; data transfer.</li>
</ul>

<p><u>Secure</u></p>

<p>Securing the data:</p>
<ul>
  <li>Server-side Encryption: default encryption on a bucket will encrypt all new objects stored in the bucket</li>
  <li>Access Control Lists (ACLs): It is account level control. It defines which account/groups can access and type of access. It can be attach by object or bucket.</li>
  <li>Bucket Policies: It is account level and user level control. It defines who and what is allowed or denied. - allows across account</li>
  <li>IAM Policy: It is user level contro. A policy attached to a user can give permission to access S3 bucket</li>
  <li>IAM Role for EC2 instance can allow EC2 instance access S3 bucket</li>
  <li>Access Point</li>
</ul>

<p style="text-align: justify;">Buckets are private by default. For securing a bucket with public access is necessary to allow public access to bucket and objects. It involves Object ACL (Individual Object level) and Bucket Policies (entire bucket level).</p>

<p style="text-align: justify;">S3 is a good option to hosting a static website. It will scales automatically. For that, the bucket access should be public and you can add a policy to allow read permission for the objects. Other use cases can be: backup and storage, disaster recovery, archive, hybrid cloud storage, data lakes and big data analytics.</p>

<p>Encrypting S3 Object:</p>
<ul>
  <li>Types: 
    <ul>
      <li>in transit: SSL/TLS; HTTPS (Buket policy can force encryption)</li>
      <li>at Rest: server-side: SSE-S3 (AES 256-bit -> default -> all objects); SSE-KMS (advantages: user control + audit key usage using CloudTrail); SSE-C: customer-provider keys (S3 does NOT store the encryption key you provide; must use HTTPS; key must be provided in header)</li>
      <li>at rest: client-side: encrypt before upload file</li>
    </ul>
  </li>
  <li>Enforcing Server-side Encryption adding a parameter in PUT Request Header:
    <ul>
      <li>x-amz-server-side-encryption: AES256</li>
      <li>x-amz-server-side-encryption: aws:kms</li>
      <li>PS: You can create bucket policy to denies any S3 PUT request without this parameter</li>
    </ul>
  </li>
  <li>CORS: needs to be anabled</li>
  <li>MFA delete: for delete object or suspend version. Only the owner can enbled it.</li>
</ul>

<p><u>Lock</u></p>
<ul>
  <li>S3 Object Lock: WriteOnce, ReadMany (WORM)
    <ul>
      <li>Governance Mode: overwrite or delete an object version only with special permissions</li>
      <li>Compliance Mode: even root cannot overwrite or delete protected object version for the duration of the retention period.</li>
      <li>Legal hold can be placed and removed by user with s3:PutObjectLegalHold permission</li>
    </ul>
  </li>
  <li>Glacier Vault Lock: WORM. Deploy and enforce compliance controls for individual S3 Glacier valts with vault lock policy. Objects can be deleted.</li>
</ul>

<p><u>Optimizing S3 Performance:</u></p>

<ul>
  <li>Use Preifx (folders inside the bucket) to increase performance</li>
  <li>Use KMS impact in performance because is necessary to call GenerateDataKey when upload a file and call Decrypt in KMS API to download a file</li>
  <li>Mulpart Uploads can increate performance. It is recomended for files over 100MB and required for files over 5GB. The performance can be improved parallelizing uploads.</li>
  <li>S3 Byte-Range Fetches: Parallelize downloads by specifying bytes ranges</li>
  <li>Tranfer speed can be increate transfering the data to an edge location</li>
</ul>

<p><u>Backup</u></p>

<ul>
  <li>Versioning: all versions are stored; good for backup; once enable it cannot be disabled (only suspended); it can be integrated with lifecycle rules and supports MFA. For the static webpage, the last version will be available, not the previous. It can use Lifecycle Management rules to transit versions throgh tiers.</li>
  <li>Replication:
    <ul>
      <li>Replicate the object from one bucket to another and the version must be enables in both sides</li>
      <li>The object uploaded after turn it on will be replicated. The others that exist will do automatically</li>
      <li>Deleted objects are not replicated by default</li>
      <li>Cross-Region Replication (CRR): compliance, lower latency access</li>
      <li>Same-Region Replication (SRR): log aggregation, live replication</li>
      <li>Copying is asynchronous</li>
      <li>Only new objects are replicated</li>
    </ul>
  </li>
  <li>S3 sync command can be used to copy objects between S# buckets and lists the source and target buckets.</li>
  <li>Amazon S3 Batch Replication provides you a way to replicate objects that existed before a replication configuration was in place, objects that have previously been replicated, and objects that have failed replication. This is done through the use of a Batch Operations job.</li>
</ul>

<p><u>Classes</u></p>

<ul>
  <li>Standard: High Availability and durability; Designed for Frequent Access; Suitable for Most workflows; low latency and high throughput. Ex: Big Data analytics, mobile, gaming, content distribution.</li>
  <li>Standard-Infrequent Access: Rapid Access; Pay to access the data; better to long-term storage, backups and disaster recover. Ex: disaster recover, backup.</li>
  <li>One Zone-Infrequent Access: data stored redundantly inside a single AZ; Costs 20% less than Standard-IA; Better to long-lived, IA, non-critical data. Ex: secondary backup copies of on-premises data.</li>
  <li>Intelligent-Tiering: Good to optimize cost. It is used to move the data into classes in a cost-efficient way if you don't know what is frequent or not.</li>
  <li>Gacier: archive data; pay by access; cheap storage. You can use Server-side filter and retrieve less data with SQL
    <ul>
      <li>Gacier Instant Retrieval (minimum duration - 90 days)</li>
      <li>Glacier Flexible Retrieval -> not need immediate access, retrieve large sets of data at no cost (backup, disaster recover)(minimum duration - 90 days)</li>
      <li>Glacier Deep Archive -> Cheapest -> data sets for 7 -10 years (12h). (minimum duration - 180 days)</li>
    </ul>
  </li>
</ul>

<p style="text-align: justify;">Cost</p>
<ul>
  <li>Owner pay for storage and data transfer</li>
  <li>If other requester, then they will pay for it</li>
</ul>

<p style="text-align: justify;">Last notes</p>
<ul>
  <li>S3 Event Notification: S3 event can be trigger to SNS, SQS, Lambda, EventBridge (archive, replay events, reliable delivery)</li>
  <li>S3 Storage Lens: Tools to analyse S3</li>
  <li>S3 Access Log: A nre buket will store the logs. They must be in the same region.</li>
  <li>Pre-Signed URL: can be created by Cosole or CLI.</li>
</ul>


<p><center>
  <img src="/img/aws/s3.png" height="100%" width="100%">
</center></p>


<h3>Storage Gateway</h3>

<p style="text-align: justify;"><b>Storage Gateway</b><a href="https://docs.aws.amazon.com/storagegateway/latest/userguide/WhatIsStorageGateway.html">[1]</a><a href="https://aws.amazon.com/storagegateway/">[2]</a></p>
<ul>
  <li>It is a hybrid cloud storage service: a bridge between on-premise data and cloud data in S3.</li>
  <li>Simplify storage management and reduce costs for key hybrid cloud storage use cases</li>
  <li>Virtually unlimited cloud storage</li>
  <li>Cannot be used to data archival</li>
  <li>Types: File Gateway, Volume Gateway and Tape Gateway</li>
  <li>Ex: moving backups to the cloud, low latency access, disaster recovery</li>
</ul>


<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/aws-storage-services/">DigitalCloud Summary</a></li>
<li><a href="https://docs.aws.amazon.com/opsworks/latest/userguide/best-practices-storage.html">Best Practices: Root Device Storage for Instances</a></li>
<li><a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-iam-policies.html">Bucket policies and user policies</a></li>


<!-- ################################################################## -->


<br />
<hr>
<br />

<h2 id="container">Docker Containers and ECS</h2>

<p style="text-align: justify;"><b>Docker</b> </p>
<ul>
  <li>Amazon <b>ECS</b> (Elastic Container Service)
    <ul>
      <li>Launch Docker containers on AWS (inside the EC2 instance)</li>
      <li>It has integration with <b>ALB</b> (Application Load Balancer)</li>
      <li>A <b>ECS cluster</b> can have ECS Container instances in different AZ</li>
      <li>It is not fully managed service and the customer can manage the underlying servers.</li>
      <li><b>Shared responsibility</b>
        <ul>
          <li>AWS start and stop the containers</li>
          <li>Customer has to provision and maintain the infrastructure (EC2 instance). </li>
        </ul>
      </li>
    </ul>    
  </li>
  <li><b><a href="https://aws.amazon.com/fargate/">Fargate</a></b>
    <ul>
      <li>Launch Docker container on AWS.</li> 
      <li>Serverless</li>
      <li>Works with ECS and EKS</li>
      <li>Charged for running tasks</li>
      <li>No EFS and EBS integrations</li>
      <li><b>Shared responsibility</b>
        <ul>
          <li>AWS: Automatically provision resources. AWS runs the containers for the customer.</li>
          <li>The customer don't need provision the infrastructure. </li>
        </ul>
      </li>
      <li><b>Pricing</b>: pay for vCPU and memory allocated</li>
    </ul>
  </li>
  <li><b>ECR</b> - Elastic Container Registry
    <ul>
      <li>Private Docker Registry</li> 
      <li>Store customer docker images to be runned by ECS or Fargate</li>
    </ul>
  </li>    
</ul>  


<p><center>
  <img src="/img/aws/ecs.png" height="90%" width="90%">
</center></p>

<p style="text-align: justify;">Amazon Elastic Container Service for Kubernetes (<a href="https://aws.amazon.com/eks/">EKS</a>): Manage Kubernetes clusters on AWS</p>


<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/amazon-ecs-and-eks/">ECS and EKS</a></li>
<li><a href="https://aws.amazon.com/ecs/pricing/">ECS Pricing</a></li>
<li><a href="https://aws.amazon.com/ecs/">ECS</a></li>


<!-- ###################################################### -->

<br />
<hr>
<br />

<h2 id="serverless">Serverless Applications</h2>

<p><u>Loosly Decouple</u></p>

<p style="text-align: justify;">The AWS recommendation for architecture is <b>Loosly Coupling</b>. It can be achieve by ELB and multiple instances. However, in some scenarios ELB may not be available. For this, other resources can be used to achive that. Here are some services that go on this direction</p>

<p><b>SQS</b> (cloud native service) <a href="https://digitalcloud.training/aws-application-integration/#amazon-simple-queue-service-amazon-sqs">[1]</a><a href="https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues.html">[2]</a>:</p>
<ul>
  <li>Fully managed message that use queue for decouple and scale microservices, distributed system and serverless application.</li>
  <li>Retention of message: default is 4 days, maximum 14 days, the minimun can be customized (e.g.,1 minutes).</li>
  <li>Deletion: after the retention period or to be read.</li>
  <li>Pay-as-you-go pricing.</li>
  <li>Asynchronous process.</li>
  <li>Settings: Delivery delay (0 up to 15 minutes)</li>
  <li>Message size: up to 256KB of text)</li>
  <li>Require Message Group ID and Message Deduplication ID</li>
  <li>AWS recommend using separate queues when you need to provide prioritization of work</li>
  <li>Security
    <ul>
      <li>Encryption: message are encrypted in trasit (HTTPS) by defaul but not at rest (can do using KMS)</li>
      <li>Access Control with IAM policy - SQS API</li>
      <li>SQS Access policy with resource policy - useful for cross-account or other services</li>
    </ul>
  </li>
  <li>Strategy:
    <ul>
      <li>FIFO: Guaranteed ordering, no message duplication, 300 trasanction per second (can achieve 3000 with baching). FIFO High throughput process up to 9000 transaction per second, per API without batching; and up to 90000 messages using batching APIs. </li>
      <li>Standard: better performance; the order message can be implemented; message can be duplicated; can use message group ID to process the message in order based on the group; unlimited throughput; unlimited throughput</li>
    </ul>
  </li>
</ul>

<p style="text-align: justify;"><b>DLQ</b> (Dead-Letter Queues):</p>
<ul>
  <li>Target for messages that cannot be processed sussessfully.</li>
  <li>It works with SQS and SNS.</li>
  <li>Useful for debugging applications and messaging systems.</li>
  <li>Redrive capability allows moving the message back into the source queue.</li>
  <li>It is a SQS queue and use FIFO.</li>
  <li>Benfits: can use alarms</li>
  <li>Publicly accessible by default</li>
</ul>

<p><b>SNS</b> (cloud native service) <a href="https://digitalcloud.training/aws-application-integration/#amazon-simple-notification-service">[1]</a><a href="https://aws.amazon.com/sns/">[2]</a> :</p>
<ul>
  <li>Push-based messaging service.</li>
  <li>Delivery messages to the endpoints that are subscribed.</li>
  <li>Fully managed message for application-to-application (A2A) and application-to-person (A2P).</li> 
  <li>Cycle: Publisher -> SNS topic / Subscriber -> get all messages from the topic</li>
  <li>Subscribers: Kinesis, SQS, Lambda, emails, SMS and endpoints</li>
  <li>Size: 256KB of text</li>
  <li>Extended Library allows sending messages up to 2GB. The payload is stored in S3 and then SNS publishes a reference to the object.</li>
  <li>DLQ Support</li>
  <li>FIFO or Standard</li>
  <li>Security
    <ul>
      <li>Encryption in transit by default (HTTPS) and can add at rest via KMS</li>
      <li>Access Policies: can be attached a resource policy, useful across-account access</li>
    </ul>
  </li>
  <li>FanOut (SNS+SQS) : messages published to SNS topic are replicated to multiple endpoint subscription (1:N)</li>
  <li>Message Filtering: send to specific subscriber</li>
  <li>Publicly accessible by default</li>
</ul>

<p><b>Amazon MQ</b> <a href="https://digitalcloud.training/aws-application-integration/#amazon-mq">[1]</a>:</p>
<ul>
  <li>Message broker</li>
  <li>Good when migrating to the cloud</li>
  <li>Supports ActiveMQ or RabbitMQ</li>
  <li>Topics and queues</li>
  <li>1:1 and 1:N message design</li>
  <li>AmazonMQ requires private network (VPC, Direct Connect or VPN)</li>
  <li>Not scale as SNS or SQS</li>
  <li>Runs on servers and can run in multiple AZs with failover</li>
</ul>


<p><b>API Gateway</b> <a href="https://digitalcloud.training/amazon-api-gateway/">[1]</a><a href="https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-request-throttling.html">[2]</a><a href="https://aws.amazon.com/blogs/aws/new-for-aws-lambda-container-image-support/">[3]</a>:
<ul>
  <li>Fully managed service for developers; easy for developers create, publish, maintain, monitor, and secure APIs at any scale</li>
  <li>Restful and WeSocket</li>
  <li>Front door of the application.</li>
  <li>Integrate with lambda, HTTP, endpoints, etc</li>
  <li>Features: 
    <ul>
      <li>Security - protect endpoints by attaching a WAF (Web Application Firewall);</li>
      <li>Stop abuse - users can easily implements DDoS protection and rate limiting to curb abuse of their endpoints;</li>
      <li>Ease of Use</li>
    </ul>
  </li>
  <li>Enpoint Types:
    <ul>
      <li>Edge-optimized - (default option): API requests get sent through a CloudFront edge location (best for global users);</li>
      <li>Regional - ability to also leverage with CloudFront; reduce latency; can be protected with WAF</li>
      <li>Private - only accessible via VPCs using interface VPC endpoint or Direct Connect</li>
    </ul>
  </li>
  <li>Securing APIs: user authentication (IAM, roles, Cognito, custom authorizer); ACM certs for edge-optimized endpoints and regional endpoints; WAF</li>
</ul>
  

<p><b>AWS Batch:</b></p>
<ul>
  <li>Run batch computing workloads within AWS (EC2 or ECS/Fargate): Fargate is more recomended because require fast start times (<30 sec), 16 VCPU or less, no GPU, 120 GiB of memory; EC2 needs more control, require GPU and custom AMIs, high levels of cuncurrency, require access to Linux Parameters</li>
  <li>Simple: Automatically provision and scale, no intallation is required</li>
  <li>Components: Jobs; Jobs definition (how jobs will run); Jobs Queues; Compute Environment</li>
  <li>Batch vs Lambda
    <ul>
      <li>Time Limits: lambda has 15 minutes execution time limit; batch does not have this</li>
      <li>Disk space: lambda has limited disk space, and EFS requires functions live within a VPC</li>
      <li>Runtime limitations: lambda is fully serverless, but limited runtimes; and Batch can use any runtime because uses docker</li>
    </ul>
  </li>
</ul>


<p><b>Step Function</b> <a href="https://digitalcloud.training/aws-application-integration/#aws-step-functions">[1]</a></p>
<ul>
  <li>Coordenate distributed apps</li>
  <li>Orchestration service; graphical console;</li>
  <li>Main componenets: state machine (workflow with different event-driven steps) and tasks (specific states within a workflow (state machine) representing a single unit of work). State is every single step within a workflow</li>
  <li>Execution: instances where you run your workflows in order to perform your task</li>
  <li>Types:
    <ul>
      <li>Standard: one execution, can run upto one year, useful for long-running workflow - auditable history; up to 2000 executions per second; pricing based per state transition</li>
      <li>express: at least one execution, can run for up to five minutes, useful for high-event-rate workflows, e.g IoT data streaming; pricing based on number of execution, durations and memory</li>
    </ul>
  </li>
</ul>

<p><b>AppFlow</b>:</p>
<ul>
  <li>Integration service for exchanging data between SaaS apps and AWS services; </li>
  <li>Pulls data records from third party SaaS vendors and stores them in S3;</li>
  <li>Bi-directional data transfer</li>
  <li>Flow (transfer data between sources and destinations);</li>
  <li>Data mapping (how sources data is stored);</li>
  <li>Filter (controls which data is transferred);</li>
  <li>Trigger (how the flow is started)</li>
  <li>Use case: salesforce records to Redshift; analyzing conversations in S3; migration to Snowflake</li>
</ul>


<p><center>
  <img src="/img/aws/serverless.png" height="100%" width="100%">
</center></p>

<p><u>Other Serverless Service</u></p>

<ul>
<li>Cognito<a href="https://digitalcloud.training/amazon-cognito/">[1]</a></li>
  <li>Lambda@Edge</li>
  <li>Amazon Kinesis Data Streams (KDS) <a href="https://digitalcloud.training/amazon-kinesis/">[1]</a> - For real-time instead of SQS</li>
  <li>
    Lambda<a href="https://digitalcloud.training/aws-lambda/">[1]</a><a href="https://aws.amazon.com/blogs/architecture/best-practices-for-developing-on-aws-lambda/">[2]</a>:
    <ul>
      <li>FaaS</li>
      <li>Example of integration: API Gateway, Kinesis, DynamoDB, S3, CloudFront, CloudWatch, SNS, SQS, Cognito</li>
      <li>Virtual functions</li>
      <li>Serverless</li>
      <li>Run on-demand</li>
      <li>Scaling automatically</li>
      <li>Event-driven</li>
      <li>Can be monitoring through <b>CloudWatch</b></li>
      <li>Integrated with Load balancer (<b>ELB</b>)</li>
      <li>Pricing: Pay per call (request) and duration (time of execution)</li>
    </ul>
  </li>
  <li>EventBridge <a href="https://aws.amazon.com/eventbridge/">[1]</a></li>
  <li>SWF <a href="https://digitalcloud.training/aws-application-integration/#amazon-simple-workflow-service-amazon-swf">[1]</a></li>
</ul>



<!-- ############################################################# -->

<br />
<hr>
<br />

<h2 id="database">AWS database services</h2>

<p style="text-align: justify;">It's possible to install database in EC2 instance. It can be necessary when is needed full control over instance and database; and using a third-party database engine <a href="https://digitalcloud.training/aws-database-services/">[1]</a><a href="https://aws.amazon.com/backup/">[2]</a>.</p>

<p style="text-align: justify;">RDS - Amazon Relational Database Service<a href="https://aws.amazon.com/rds/">[1]</a><a href="https://digitalcloud.training/amazon-rds/">[2]</a><a href="https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_CommonTasks.BackupRestore.html">[3]</a>.</p>
<ul>
  <li>Use EC2 instance</li>
  <li>Benefits to deploy database on RDS instead EC2: hardware provision, database setup, Automated backup and software patching. It reduce the database administration tasks. There is no need to manage OS. You can only create read replicas of databases running on RDS.</li>
  <li>RDS types for it: SQL Server, Oracle, MySQL, PostgreSQL, MariaDB</li>
  <li>It's possible encrypt the RDS instances using AWS Key Management Service (KMS) and snapshot</li>
  <li>Sales up by increaing instance size (compute and storage)</li>
  <li>Replicas is only to ready. It improves database scalability.</li>
  <li>Read Replica: read-only copy of the primary database. It can be cross-AZ and cross-region. Not used for recovery disaster, only for performance. It requeres Automatic backup.</li>
  <li>Multi-AZ: RDS creates an copy of production database in another AZ. RDS will automatically fail over to the standby copy.</li>
  <li>It can use Auto scaling to add replicas</li>
  <li>Serveless</li>
  <li>You can't use SSH to access instances.</li>
  <li>It is suited for OLTP workloads (real-time)</li>
  <li>Security through IAM, Security Groups, KMS, SSL in transit</li>
  <li>Support for IAM Authentication (IAM roles)</li>
  <li>RDS Proxy: Allows app to pool and share DB connections improving db efficience, as well reduce the failover</li>
  <li>Shared Responsibility
    <ul>
      <li>AWS: Manage the underlyning EC2 instance, disable ssh access; Automated DB and OS patching, guarantee the hardware</li>
      <li>Consutmer: Check ports, IP, Security groups inbound rules; users and permissions for database; create database (public/private access); config DB to only allow SSL connection; database encryptation setting; createing schema (table, indexes,etc), Schema Optimization.</li>
    </ul>
  </li>
  <li>Pricing: Depends the Clock hours of server uptime; Database characteristics (size, mem); Database purchase type (on demand, reserved instance); Number of database instances; Provisioned storage; Additional storage; Requests; Deployment type; Data transfer (OUT); Reserved Instances.</li>
</ul>

<p><center>
  <img src="/img/aws/rds.png" height="100%" width="100%">
</center></p>


<p style="text-align: justify;"><b>Aurora</b><a href="https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-multi-master.html">[1]</a><a href="https://aws.amazon.com/rds/aurora/">[2]</a><a href="https://digitalcloud.training/amazon-aurora/">[3]</a><a href="https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/USER_CreateSnapshotCluster.html">[4]</a></p>
<ul>
  <li>Relational DB from AWS fully managed.</li>
  <li>Compatible with <a href="https://aws.amazon.com/rds/aurora/mysql-features/">MySQL</a>, PostgreSQL, Oracle, Microsoft SQL Server</li>
  <li>Storage: data is stored in 6 replicas across 3 AZ</li>
  <li>Compute: cluster of DB instance across multiple AZ, auto scaling (up 128 TB) of Read Replicas. automatic backup enabled</li>
  <li>User case: unpredictable and intermittent workloads, no capacity planning</li>
  <li>Autora Global: up to 16DB read instances in each region</li>
  <li>Perform Machine Learning</li>
</ul>

<p><center>
  <img src="/img/aws/aurora.png" height="100%" width="100%">
</center></p>

<p style="text-align: justify;">Amazon <b>ElastiCache</b><a href="https://aws.amazon.com/elasticache">[1]</a><a href="https://digitalcloud.training/amazon-elasticache/">[2]</a></p>
<ul>
  <li>Manage Mem cached</li>
  <li>Managed Redis</li>
  <li>Service that adds caching layers on top of your databases</li>
  <li>In-Memory databases with high performance and low latency (under a millisecond)</li>
  <li>Support for clustering (Redis) and Multi AZ</li>
  <li>Securitu through IAM, Security Groups, KMS, Redis Auth</li>
  <li>Shared Responsibility: AWS takes care of OS maintenance / patching, optimizations, setup, configuration, monitoring, failure recovery and backups</li>
</ul>

<p><center>
  <img src="/img/aws/elasticache.png" height="100%" width="100%">
</center></p>

<p style="text-align: justify;"><b>Amazon DynamoDB</b><a href="https://aws.amazon.com/dynamodb/features/">[1]</a><a href="https://digitalcloud.training/amazon-dynamodb/">[2]</a><a href="https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html">[3]</a></p>

<ul>
  <li><a href="https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/SQLtoNoSQL.WhyDynamoDB.html">NoSQL</a> database</li>
  <li>Key/value store and document store (Tables, Items [maximum size 400KB] and Attributes)</li>
  <li>Highly available with replication across 3 AZ.</li>
  <li>Stored on SSD storage</li>
  <li>Hight performance</li>
  <li>Low latency retrieval</li>
  <li>Eventually consistent reads (default - better performance) or Strongly consistent reads</li>
  <li>Multi-Region replication. Ative-Active with cross region support. The global tables replicate data automatically across the customer choise of regions</li>
  <li>Distributed serverless database</li>
  <li>Integrated with IAM for security, authorization and administration</li>
  <li>Low cost and auto scaling</li>
  <li>Horizontal Scaling</li>
  <li>Standard and IA (Infrequent Access) Table class</li>
  <li><a href="https://aws.amazon.com/dynamodb/dax/">DynamoDB <b>Accelarator</b> (DAX)</a> is fully managed in memory cache, the performance is improved, highly scalable and available. Only used with DynamoDB</li>
  <li>Considering a <a href="https://aws.amazon.com/blogs/aws/new-amazon-dynamodb-continuous-backups-and-point-in-time-recovery-pitr/"><b>point-in-time recovery</b></a> (PITR)(continuous backup) for DynamoDB, the customer is responsible to configure (turn on) and AWS is responsible for the backup. Amazon RDS database instance can be restored to a specific point in time with a granularity of 5 minutes</li>
  <li>Pricing: throughput; Indexed data storage; Data tranfer; Global tables; reserved capacity; On-demand capacity mode; Provisioned capacity mode</li>
  <li>Security: Encryption at rest using KMS; Site-to-Site VPN, Direct Connect (DX), IAM policies and roles; Integrate with CloudWatch and CloudTrail; VPC endpoints to communicate directly with DynamoDB</li>
  <li>ACID with DynamoDB -> Dynamo transaction across 1 or more tables within a single AWS account and region. Used when the application needs coordenation. This feature needs to be enable.</li>
  <li>Backup: On-Demand: full backups at any time; no performance impact, same region of source table</li>
  <li>Recovery: Point-in-Time Recovery (PITR): protect agains accidental writes or deletes; restore to any point in the last 35 days; incremental; not default; latesst restorable in the past 5 minutes</li>
  <li>Streams: time-oerdered sequence of titem-level changes in a table. Stored for 24 hours</li>  
  <li>Global Table: managed multi-master, multi-region replication: globally distributed applications; based on DynamoDB streams; replication latency under 1 second</li>  
  <li>Time to Live (TTL): define when an item expire abd can be automatically deleted</li>
</ul>

<p><center>
  <img src="/img/aws/dynamoDB.png" height="100%" width="100%">
</center></p>

<p style="text-align: justify;"><b>DocumentDB</b><a href="https://aws.amazon.com/documentdb">[1]</a><a href="https://docs.aws.amazon.com/documentdb/latest/developerguide/backup_restore.html">[2]</a>: Implementation of MongoDB. It is fully managed service; storage scales sutomatically up tp 64TB, high avai;ability and replicates six copies of the data across 3 AZs. Used to migrate MongoDB to cloud. Backup to S3. Ex: User profile.</p>

<p style="text-align: justify;">Amazon <b>Redshift</b><a href="https://aws.amazon.com/redshift">[1]</a><a href="https://docs.aws.amazon.com/redshift/latest/mgmt/working-with-snapshots.html">[2]</a></p>
<ul>
  <li>Based on PostgreSQL (but not OLTP)</li>
  <li>Relational database for a analytic purpose</li>
  <li>OLAP - online analytical processing (analytics and data warehouseing)</li>
  <li>Parallel Query</li>
  <li>Run SQL against data warehouse</li>
  <li>Redshift Spectrum run queries against Amazon S3 without loading the data from Amazon S3 into data warehousing solution</li>
  <li>Pricing: Pay as you go</li>
  <li>BI tools: AWS Quicksight or Tableau</li>
</ul>

<p style="text-align: justify;">Amazon <b>Glue</b><a href="https://aws.amazon.com/glue/">[1]</a><a href="https://digitalcloud.training/aws-glue/">[2]</a></p>
<ul>
  <li>extract, transform, and load (ETL) service</li>
  <li>serverless service</li>
  <li>prepare and load their data for analytics</li>
  <li>The AWS Glue Data Catalog is a central repository to store structural and operational metadata for all your data assets. </li>
</ul>

<p style="text-align: justify;">Amazon EMR (Elastic MapReduce)<a href="https://aws.amazon.com/emr/features/">[1]</a><a href="https://digitalcloud.training/amazon-emr/">[2]</a></p>
<ul>
  <li>Helps to create Hadoop clusters (Big Data)</li>
  <li>Take care of all the provisioning and configuration</li>
  <li>Auto Scaling</li>
  <li>Ex: machine learn and big data</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/qldb"><b>QLDB</b></a>(Quantum Ledger Database): Fully managed graph database; no decentralization component; immutable ledger database. Ex: review a complete history of all the changes. NoSQL. Use cryptography. Immutable database.</p>

<p style="text-align: justify;"><b>Managed Blockchain</b>: create and manage blockchain networks with open-source frameworks</p>

<p style="text-align: justify;"><b>Amazon Keyspaces</b>: run Apache Cassandra workloads. Distributed database that uses NoSQL. Main application is big data but can be used for backend. Fully manage database. Pay for resource is used.</p>

<p><b>Neptune</b><a href="https://aws.amazon.com/neptune">[1]</a<a href="https://docs.aws.amazon.com/neptune/latest/userguide/intro.html">[2]</a>: Fully managed graph database. Good to app with highly connected datasets, as fraud detection and knowledge grapns. Used for analysis, build connections between identities, build knowledge, detect fraud patterns, security.</p>

<p style="text-align: justify;">Analyses</p>
<ul> 
  <li><a href="https://aws.amazon.com/quicksight/"><b>QuickSight</b></a>:  scalable, serverless, embeddable, machine learning-powered business intelligence (BI) service</li>
  <li><b>Athena</b><a href="https://digitalcloud.training/amazon-athena/">[1]</a><a href="https://aws.amazon.com/athena/features/">[2]</a>: Analyze data in S3 using SQL; it is serverless (no infrastructure to manage); Pricing: you pay only for the queries that you run. Ex: BI, analytics, reporting</li>
  <li>Timestream: time series database service for IoT and operational application</li>
</ul>



<!-- ###################################################### -->


<br />
<hr>
<br />

<h2 id="deploy">Deployment</h2>


<p style="text-align: justify;">Amazon <b>CloudFormation</b><a href="https://aws.amazon.com/cloudformation/">[1]</a><a href="https://digitalcloud.training/aws-cloudformation/">[2]</a></p>
<ul>
  <li>declarative way of outlining your AWS Infrastructure, for any resources</li>
  <li>It uses <b>template</b> to create the stack (security group, EC2 instancesm S3 bucket, ELB, etc)</li>
  <li>Infrastructure as a Code (IaaC)</li>
  <li>Productivity: fast to destroy and re-create an infrastructure</li>
  <li>Automated generation of diagrams</li>
  <li>Declarative programming</li>
  <li>Free to use</li>
  <li>JSON/YAML</li>
</ul>

<p style="text-align: justify;">AWS <a href="https://aws.amazon.com/cdk/"><b>Cloud Development Kit (CDK)</b></a></p>
<ul>
  <li>Open-source software development framework.</li>
  <li>Define your cloud infrastructure using a familiar language.</li>
  <li>The code is compiled into a CloudFormation template</li>
  <li>Provisions the resources using CloudFormation</li>
</ul>

<p style="text-align: justify;">AWS Elastic <b>Beantalk</b><a href="https://aws.amazon.com/elasticbeanstalk/">[1]</a><a href="https://digitalcloud.training/aws-elastic-beanstalk/">[2]</a></p>
<ul>
  <li>Integrate with VPC and IAM</li>
  <li>ZIP, WAR, Git</li>
  <li>Plataform as a Service (PaaS)</li>
  <li>Wasy-to-use service for deploying (on EC2) and scaling web applications and services developed with Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker on familiar servers such as Apache, Nginx, Passenger, and IIS.</li>
  <li>Shared Responsibility
    <ul>
      <li>Aws: performe the deployment strategy, OS, capacity, load balancing, auto-scaling, health-monitoring and responsiveness</li>
      <li>Customer: deployment strategy configuration, application code</li>
    </ul>
  </li>    
  <li>Pricing: Free but you pay for the underlying instances</li>
</ul>


<p style="text-align: justify;">AWS <b>Systems Manager </b> (SSM) Session Manager<a href="https://aws.amazon.com/systems-manager/faq/">[1]</a><a href="https://digitalcloud.training/aws-systems-manager/">[2]</a></p>
<ul>
  <li>Provides an operations console and APIs for centralized application and resource management in hybrid environments</li>
  <li>A hybrid service that manage EC2 and OnPremises system at scale</li>
  <li>Operations insights about state of infrastructe. </li>
  <li>Provides interactive browser-based shell and CLI experience</li>
  <li>Run commands and apply patches on EC2 instance</li>
  <li>Manage the OS and Database patches</li>
  <li>Provide secure and auditable instance management without the need to open inbound ports, maintain bastion hosts, and manage SSH keys</li>
  <li>Centralize operational data from multiple AWS services, automate tasks, create logical groups of resources</li>
  <li>Track and resolve operational issues across your AWS applications and resources from a central place</li>
</ul>

<p style="text-align: justify;">AWS <b>OpsWorks</b><a href="https://digitalcloud.training/aws-opsworks/">[1]</a></p>
<ul>
  <li>Like Chef and Puppet - perform server configuration automatically.</li>
  <li>Alternative to SSM</li>
</ul>


<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/aws-resource-access-manager/">AWS Resource Access Manager</a></li>



<!-- ##################################################### -->

<br />
<hr>
<br />
<h2 id="monitoring">Cloud Monitoring, Audit</h2>

<p style="text-align: justify;"><b>CloudWatch</b> (Metrics, Logs, Alarms, Events) <a href="https://aws.amazon.com/cloudwatch/">[1]</a><a href="https://digitalcloud.training/amazon-cloudwatch/">[2]</a></p>
<ul>
  <li>Performance <b>Monitoring</b></li>
  <li>It is a  monitoring and observability service which provides metrics and insights; interactively search and analyze log data. </li>
  <li>Regional source</li>
  <li>Features: System Metrics, Application Metrics, Alarms</li>
  <li>The alarms trigger notifications for metric.</li>
  <li>Types of metrics: default (CPU utilization, Network throughput), custom (EC2 Memory utilization, EBS Storage Capacity)</li>
  <li>The <a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html">CloudWatch Logs</a> enable real-time monitoring, can store and access customers log file from EC2 instance, CloudTrail, etc. Centralize logs, quering logs, audit, etc. It's possible to query logs to look for potential issues. For custom logs, use CloudWatch Agent, including on-premise. Features: Filter Patterns; CloudWatch Logs Insights (query using SQL); Alarms. It cannot provide the <b>status</b> of the customer resources. Adjustable retention. </li>
  <li>Monitoring with Managed Service (Grafana, for Prometheus)</li>
</ul>

<p><b>CloudTrail</b><a href="https://aws.amazon.com/cloudtrail/"></a><a href="https://digitalcloud.training/aws-cloudtrail/">[2]</a>: <b>Record API calls</b>. It tracks events (history events/API calls). Log, monitoring and retain account activity (Who, What, When)(track user activities and API requests and filter logs to assist with operational analysis and troubleshooting). <b>Governance, compliance, audit for AWS account</b>. It can be applied to all regions or one. It has encryptation enabled as default. Enabling the <b>insights</b> allows CloudTrail detect automatically <b>unusual API activities</b> in the customer account. </p>

<p><a href="https://digitalcloud.training/aws-config/">AWS Config</a>: <b>Record configuration changes</b>Helps with auditing and recording compliance of the AWS resources, and record configurations and changes. Per Region but can be aggreated across region and account. It can send alerts for changes and the configuration can be store inside S3.</p>

<p><a href="https://aws.amazon.com/eventbridge/"><b>EventBridge</b></a> (CloudWatch Events): Serverless, build event-driven applications at scale, schedule (cron jobs), event pattern, trigger lambda functions,send SQS/SNS message, etc. Schema Registry, Archive events, replay archive events</p>

<p><b><a href="https://aws.amazon.com/xray/">AWS X-Ray</a></b>: Debugging in Production. Benefits: performance, uderstand dependencies, review request, find errors, identify users, trace request across microservice/AWS Service.</p>

<p><b>CodeGuru</b>: automated code review and application performance recommendations</p>

<p><b><a href="https://status.aws.amazon.com/">AWS Helth Dashboard</a></b>: service history (Service health Dashboard) for all regions or by your account (Account Helth Dashboard). It shows general status.</p>

<p><b><a href="https://aws.amazon.com/premiumsupport/technology/personal-health-dashboard/">AWS Personal Health Dashboard</a></b>: personalized view of the status of the AWS services that are part of customer Cloud architecture. Alerts are triggered by changes in the health of your AWS resources, giving event visibility, and guidance to help quickly diagnose and resolve issues and. Customer can quickly assess the impact on your business when AWS service(s) are experiencing issues. It gives a personalized view of performance and availability of the services used by customer.</p>


<p><center>
  <img src="/img/aws/monitor.png" height="100%" width="100%">
</center></p>

<!-- ####################################################### -->



<br />
<hr>
<br />

<h2 id="security">Security</h2>

<p style="text-align: justify;"><a href="https://aws.amazon.com/compliance/shared-responsibility-model/"><b>Shared Responsibility</b></a> has the customer responsible for security IN the cloud (data, access, authentication, configuration, encryptation, network traffic protection). AWS is responsible for the security OF the cloud, protecting/mnaging all AWS Global infrastructure (Software [compute, storage, database, networking], and hardware [regions, AZ, Edge Locations])</p>
<ul>
  <li>EC2 Storage:
    <ul>
      <li>AWS: Infrastructure, Replication for data for EBS volumes and EFS drives, replacing faulty hardware, Ensuring their emploees cannot access your data.</li>
      <li>Customer: backups and snapshot procesures, data encryptation, data on the drives, analysis the risk</li>
    </ul>
  </li>
  <li>Databases
    <ul>
      <li>Customer: resiliency, backup, patching, high availability, fault tolerance, scaling, etc.</li>
    </ul>
  </li> 
  <li>Shared Controls
    <ul>
      <li>Patch Management, Configuration Management, Awareness and Training</li>
    </ul>
  </li>
</ul>

<p style="text-align: justify;">DDos: Distributed Denial-of-Service</p>
<ul>
  <li>AWS Shield Standard: free for every customer, protect websites and applications (SYN/UDP fllds, reflection attacks). </li>
  <li>AWS Shield Advanced: protection 24/7, optional DDoS migration services; protection on EC2, ELB, CloudFront, GLobal Acceleator, Route 53. Detection and mitigation for network layer (layer 3), transport layer (layer 4) and application layer (layer 7) attacks</li>
  <li>AWS WAF<a href="https://docs.aws.amazon.com/waf/latest/developerguide/how-aws-waf-works.html">[1]</a><a href="https://digitalcloud.training/aws-waf-shield/">[2]</a> (Web Application Firewall): filter specific requests based on rules, protection on layer 7 (HTTP), ALB, API Gateway, CloudFront, Define Web ACL (Web Access Control List - protect SQL Injection and Cross-Site Scripting(XSS), rate-based rules). Protecting a website that is hosted outside of AWS (the on-premise IP is added to a target group).</li>
  <li>Configuring a firewall in front of resources is a <a href="https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/mitigation-techniques.html">good practice</a> to protect against DDoS</li>
  <li><a href="https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/mitigation-techniques.html">Mitigate</a></li>
</ul>

<p style="text-align: justify;"><b><a href="https://aws.amazon.com/security/penetration-testing/">Penetration Testing</a></b></p>
<ul>
  <li>Against customer AWS infrastructure without prior approval, e.g. EC2 instances, NAT Gateway, ELB, RDS, CloudFront, Aurora, API Gateway, Lambda, Beanstalk environment and LightSail resources</li>
  <li>It cannot: Dos, Port flooding, etc</li>
</ul>

<p style="text-align: justify;"><b>Encryptation</b></p>
<ul>
  <li>AWS <b>KMS</b><a href="https://digitalcloud.training/aws-kms/">[1]</a> - Key Management Service
    <ul>
      <li>Encryptation for Software</li>
      <li>AWS manage the encryptation keys</li>
      <li>Sometimes is necessary to encrypt the <b>data in rest</b>(data stored or archived on device) or <b>in transit</b>(being moved from an origin to a destiny throgh network)</li>
      <li>Encryptation is possible in all storage and database: EBS Volume, S3 bucket, Redshift, RDS, EFS</li>
      <li>Encryptation is automatically enabled to: CloudTrail Logs, <a href="https://docs.aws.amazon.com/amazonglacier/latest/dev/DataEncryption.html">S3 Glacier</a>, Storage Gateway</li>
    </ul>
  </li>
  <li>The <b>AWS encryption SDK</b> is a <a href="https://docs.aws.amazon.com/en_us/AmazonS3/latest/userguide/UsingClientSideEncryption.html">client-side encryption</a> library that is separate from the language–specific SDKs</li>
  <li>Amazon <b>S3 Managed Keys</b> (SSE-S3) is a <a href="https://docs.aws.amazon.com/en_us/AmazonS3/latest/userguide/serv-side-encryption.html">server-side encryption</a> where each object is encrypted with a unique key. As an additional safeguard, it encrypts the key itself with a root key that it regularly rotates.</li>
  <li>Server-side encryption with AWS Key Management Service (AWS KMS) keys <b>(SSE-KMS)</b> is similar to SSE-S3, but using this service. It provides audit trail.</li>
  <li><b>CloudHSM</b><a href="https://aws.amazon.com/cloudhsm/">[1]</a><a href="https://digitalcloud.training/aws-cloudhsm/">[2]</a>: Hardware Security Module. Encryptation for Hardware; The customer manages the encryptation keys; use HSM device (level 3 compliance)</li>
</ul>

<p style="text-align: justify;"><b>CMK</b> - Customer Master Keys</p>
<ul>
  <li>AWS managed CMK: create, managed and used on the customers behalf by AWS; used by AWS services</li>
  <li>Customer Managed CMK: create, manage, use, enable or disable; rotation policy</li>
  <li>AWS owned CMK: collections of CMKs owned by AWS to use in multiple accounts. The customer cannot see those keys.</li>
  <li>CloudHSM Keys: created by the device</li>
</ul>

<p style="text-align: justify;"><b>ACM</b> - AWS Certificate Manager</p>
<ul>
  <li>Customer can provise, manage and deploy SSL/TSL certiticates</li>
  <li>Provide encryptation for websites (HTTPS)</li>
  <li>Free charge for TLS certificate</li>
  <li>Integration with ELB, CloudFront, APIs</li>
</ul>

<p style="text-align: justify;">AWS <b>Secrets Manager</b></p>
<ul>
  <li>Storing secrets</li>
  <li>Rotation of secrets</li>
  <li>Integration with RDS</li>
  <li>Secrets encrypted using KMS</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/artifact/"><b>AWS Artifact</b></a>: Artifact reports (AWS security and compliance document) and Artifact Agreements (AWS agreements). Ex: Service Organization Control (SOC) reports, Payment Card Industry (PCI)</p>

<p style="text-align: justify;">Amazon <a href="https://aws.amazon.com/guardduty"><b>GuardDuty</b></a>: it is an intelligent Threat discovery to protect AWS account. Monitor suspicious activity It uses Machine Learning and check Logs. Identify potential security issues. Analyse CloudTrail events, VPC Flow Logs, etc.</p>

<p style="text-align: justify;"><a href="https://aws.amazon.com/inspector/">Amazon <b>Inspector</b></a>: </p>
<ul>
  <li>Automated security assessment service that helps improve the security and compliance of applications deployed on AWS. </li>
  <li>Inspect running operating systems (OS) against known vulnerabilities</li>
  <li>Analyze against unintended network accessibility</li>
  <li>Exposure, vulnerabilities, and deviations from best practices</li>
  <li>Automated Security Assessments for EC2 instances, Container images, Lambda Functions.</li>
  <li>Reports and Integration with AWS security Hub</li>
  <li>Send findings to Amazon Event Bridge.</li>
  <li>Continous scanning of the infrastructure when it is needed</li>
  <li>Can use an agent to monitoring</li>
  <li>Cannot be used to prevent Distributed Denial-of-Service (DDoS) attack</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/config/">AWS <b>Config</b></a>:</p>
<ul>
  <li>Enables customer to assess, audit, and evaluate the configurations of their AWS resources.</li>
  <li>Continuous monitoring.</li>
  <li>Track all changes in the resources</li>
  <li>Auditing and recording compliance, configurations</li>
  <li>Allows automating the evaluation of recorded configurations</li>
  <li>Per region service; can be aggregated across regions and accounts</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/macie/"><b>AWS Macie</b></a>: fully managed data security and data privacy service. It uses machine learning and pattern matching to discover and protect customers sensitive data in AWS. Identify potential security issues.</p>

<p style="text-align: justify;"><b>AWS Security Hub</b>: Central Security Hub. For AWS Account. Automate security Checks. Create a dashboard. Identify potential security issues.</p>

<p style="text-align: justify;"><b>AWS Detective</b>: deep analyses to isolate the root cause of the security issues or suspicious activities (ML/graphs)</p>

<p style="text-align: justify;"><a href="https://aws.amazon.com/premiumsupport/knowledge-center/report-aws-abuse/"><b>AWS Abuse</b></a>: Report suspected AWS resources used for abusive or illegal purposes (spam, port scanning, DoS, DDoS, etc)</p>

<p style="text-align: justify;">AWS <b>STS</b> - Security Token Service: temporary (short-term credentials), limited privileges credentials</p>

<p style="text-align: justify;">AWS <a href="https://aws.amazon.com/cognito/"><b>Cognito</b></a> - Alternative to IAM. Identity for your Web and Mobile applications users (sign-up/sign-in; social identity like Facebook)</p>

<p style="text-align: justify;">AWS <b>Directory Service</b><a href="https://digitalcloud.training/aws-directory-services/">[1]</a>: AWS Managed Microsoft Active Directory (Database of objects (user, accounts, computers, etc). Centralized security management)</p>

<p style="text-align: justify;">AWS <b>IAM Identify Center</b>: One loging like <a href="https://aws.amazon.com/single-sign-on/">SSO</a>.</p>

<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html"><b>AWS IAM Access Analyzer</b></a>: identify the resources in your organization and accounts, such as Amazon S3 buckets or IAM roles, shared with an external entity. This lets you identify unintended access to your resources and data, which is a security risk.</p>

<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/aws-security-services/">(DigitalCloud) Summary</a></li>
<li><a href="https://digitalcloud.training/aws-cloud-management-services/">(DigitalCloud) AWS Cloud Management Services</a></li>
<li><a href="https://aws.amazon.com/security/">AWS Cloud Security</a></li>
<li><a href="https://aws.amazon.com/waf/features/">AWS WAF features</a></li>



<!-- #################################################### -->


<br />
<hr>
<br />

<h2 id="migration">Migration</h2>

<p style="text-align: justify;"><a href="https://aws.amazon.com/cloud-adoption-framework/">AWS Cloud Adoption Framework (AWS CAF)</a> AWS experience and best practices to help migrate your business outcomes through innovative use of AWS. Perspective: Business, People, Governance, Platform, Security and Operations.</p>

<p><a href="https://aws.amazon.com/blogs/enterprise-strategy/6-strategies-for-migrating-applications-to-the-cloud/">Strategy</a>:</p>
<ul>
  <li><b>Rehosting</b>: moving applications without changes (lift-and-shift)</li>
  <li><b>Replatforming</b>: few cloud optimizations to realize a tangible benefit(lift, tinker, and shift)</li>
  <li><b>Refactoring/re-architecting</b>: reimagining how an application is architected and developed by using cloud-native features</li>
  <li><b>Repurchasing</b>: moving from a traditional license to a software-as-a-service model</li>
  <li><b>Retaining</b>:  keeping applications that are critical for the business in the source environment</li>
  <li><b>Retiring</b>: removing applications that are no longer needed</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/dms/"><b>DMS</b></a> (Database Migration Service): Migrate to AWS. With this is possible do continuous replication (ex: send to data warehouse)</p>

<p style="text-align: justify;"><b><a href="https://aws.amazon.com/migration-hub/features/">AWS Migration Hub</a></b>: single location to track the progress of application migrations</p>

<p style="text-align: justify;"><b>AWS Server Migration Service (SMS)</b> is a fast agentless service easy to migrate thousands of on-premises workloads to AWS</p>

<p style="text-align: justify;">AWS Application Migration Service<a href="https://aws.amazon.com/application-migration-service/">[1]</a><a href="https://digitalcloud.training/aws-migration-services/">[2]</a> <b>(MGN)</b>: Migrating to native AWS</p>

<p style="text-align: justify;"><a href="https://aws.amazon.com/snow"><b>Snow Family</b></a></p>
<ul>
  <li>Highly-secure, portable devices to collect and process data at the edge, and migrate data into and out of AWS</li>
  <li>Data migration: 
    <ul>
      <li>Snowcone: less size of storage, it is a small device, send data to AWS offline or using AWS DataSync</li>
      <li>Snowball Edge (Storage Optimized (80TB) /Compute Optimized (42TB)): data transfer throught the network, pay per data transfer job (Ex: disaster revovery), can have Storage Clustering (up to 15 nodes.) EC2 does this natively support. EC2 compute instance can be hosted on a Snowball.</li>
      <li>Snowmobile: More capacity (100PB - exabytes), high security</li>
    </ul>  
  </li>
  <li>Edge computing: Snowcone, Snowball Edge. Process data while it's being create on an edge location (Ex: process data, machine learning, transcoding media streams)</li>
  <li>OpsHub manage Snow Family device.</li>
  <li>Snowball Pricing: per data transfer job</li>
</ul>

<p style="text-align: justify;">AWS <a href="https://docs.aws.amazon.com/application-discovery/latest/userguide/what-is-appdiscovery.html">Application Discovery Service</a> helps you plan your migration to the AWS cloud by collecting usage and configuration data about your on-premises servers.</p>




<!-- #################################################### -->



<br />
<hr>
<br />

<h2 id="machinelearning">Machine Learning</h2>

<p>Amazon <b>Rekognition</b>: find objects, people, text in images and videos. Create "familiar faces" database or compare against celebrities.</p>

<p><a href="ttps://aws.amazon.com/transcribe/">Amazon <b>Transcribe</b></a>: Convert speech to text.(deep learning process. Automatically remove Personal Identifiable Information (PII)</p>

<p><a href="https://aws.amazon.com/polly/">Amazon <b>Polly</b></a>: Turn text into lifelike speech. Deep learning.</p>
<p>Amazon <b>Translate</b>: Natural and accurate language translation</p>
<p>Amazon <b>Lex</b>: Automatic Speech Recognition (ASR) - speech to text (chatbots, call center bots)</p>
<p>Amazon <b>Connect</b>: receive calls, create contact flows</p>
<p>Amazon <b>Comprehend</b>: Natural Language Processing (NLP), serverless service; analyses and organize text; identify positive/negative experience </p>
<p>Amazon <b>SageMaker</b>: service for build, train and deploy machine models.</p>
<p>Amazon <b>Forecast</b>: predict future sales, reduce forecasting time. Ex. Financial planning.</p>
<p>Amazon <b>Kendra</b>: document search service. Extract answers from docs. Natural Language search.</p>
<p>Amazon <b>Personalize</b>: build apps with real-time personalized recommendation</p>
<p>Amazon <b>Texttract</b>: automatically extract text, handwriting and data from documents using AI and ML.</p>








<!-- ###################################################### -->


<br />
<hr>
<br />

<h2 id="others">Others Services</h2>

<p style="text-align: justify;">Amazon <a href="https://aws.amazon.com/batch/"><b>Batch</b></a></p>
<ul>
  <li>Fully managed batch process</li>
  <li>Batch will dynamically launch EC2 instances or Spot instances</li>
  <li>AWS provisions the compute and memory. Customer only need submit or schedule the batch job.</li>
  <li>Batch jobs are defines as Docker images and run on ECS</li>
</ul>



<p style="text-align: justify;">AWS <a href="https://aws.amazon.com/codedeploy/"><b>CodeDeploy</b></a></p>
<ul>
  <li>Deploy automatically</li>
  <li>Works with EC2 instanes, On-Premises servers</li>
  <li>CodeDeploy Agent is responsable to provision and configure Servers and Instances</li>
</ul>

<p style="text-align: justify;">AWS <a href="https://aws.amazon.com/codecommit/"><b>CodeCommit</b></a>: Same of Git technology</p>
<p style="text-align: justify;">AWS <a href="https://aws.amazon.com/codepipeline/"><b>CodePipeline</b></a>: Orchestrate the steps until production</p>
<p style="text-align: justify;">AWS <a href="https://aws.amazon.com/codestar/features/"><b>CodeStar</b></a>: UI to manage Software Development activities.</p>
<p style="text-align: justify;">AWS <b>Cloud9</b>: Cloud IDE</p>

<p style="text-align: justify;">AWS <a href="https://aws.amazon.com/codebuild/features/"><b>CodeBuild</b></a></p>
<ul>
  <li>Compile code, run tests and packaged to be deployed by CodeDeploy</li>
  <li>Pay-as-you-go pricing. Pay for build time</li>
  <li>Like Jenkins</li>
</ul>

<p style="text-align: justify;">AWS <b>CodeArtifact</b></p>
<ul>
  <li>Artifacts: dependencies</li>
  <li>It is an artifact management</li>
  <li>Like maven, gradle, npm, yarn</li>
  <li>Developers and CodeBuild retrieve the dependencies using it.</li>
</ul>


<p style="text-align: justify;">Amazon <b>LightSail</b>: Low cost, easy, preconfigured virtual servers, good to beginners. However, it not possible to deploy a scalable node.js application into a VPC</p>
<p style="text-align: justify;">Amazon <b>WorkSpaces</b>: Managed Desktop as a Service (DaaS). Integrated with KMS. Pay-as-you-go.</p>
<p style="text-align: justify;">Amazon <b>AppStream</b>: Desktop Application Streaming Service (web browser)</p>
<p style="text-align: justify;">AWS <b>IoT</b>: connect devices to the cloud</p>
<p style="text-align: justify;">Amazon <b>Elastic Transcoder</b>: convert media files in S3 into different formats of media files</p>
<p style="text-align: justify;">AWS <b>AppSync</b>: store and sync data between mobile and web app</p>
<p style="text-align: justify;">AWS <b>Amplify</b>: develop and deploy scalable full stack web and mobile application</p>
<p style="text-align: justify;">AWS <b>Devise Farm</b>: service to test web application and mobile</p>
<p style="text-align: justify;">AWS <b>Backup</b>: set on demand and scheduled backups. Cross-Region/Cros-Account backups</p>
<p style="text-align: justify;">AWS <b>Elastic Disaster Recovery(DRS)</b>: recover physical, virtual and cloud-based servers into AWS</p>
<p style="text-align: justify;">AWS <b>DataSync</b>: Move large amount of data from on-premises to AWS</p>
<p style="text-align: justify;">AWS <b>Application Discovery Service</b>: Move large amount of data from on-premises to AWS</p>
<p style="text-align: justify;">AWS <b>Fault Inject Simulator (FIS)</b>: based on chaos engineering. stressing test.</p>
<p style="text-align: justify;">AWS <b>Ground Station</b>: control satellite communication</p>
<p style="text-align: justify;">AWS <b><a href="https://aws.amazon.com/pinpoint/">Pinpoint</a></b>: marketing communication service (email, sms, voice)</p>


<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/additional-aws-services/">DigitalCloud Summary</a></li>
<li><a href="https://aws.amazon.com/developer/tools/">Tools to Build on AWS</a></li>  
<li><a href="https://aws.amazon.com/datapipeline/">AWS Data Pipeline</a></li>
<li><a href="https://aws.amazon.com/elasticsearch-service/features/">Amazon OpenSearch Service Features</a></li>



<!-- ############################################################### -->


<br />
<hr>
<br />

<h2 id="pricing">Billing and <a href="https://aws.amazon.com/ec2/pricing/">Pricing</a></h2>

<p>Notes:</p>
<ul>
  <li>AWS: Operational expenses (OpEx): Pay as you go, tax deductible in same year</li>
  <li>Traditional: capital expenses (CapEx): Purchase server, tax deductible over depreciation lifetime</li>
  <li>Cloud: Trade CapEx for OpEx</li>
  <li>AWS Total Cost of Ownership (<a href="https://docs.aws.amazon.com/whitepapers/latest/how-aws-pricing-works/aws-pricingtco-tools.html">TCO</a>) comparing with in-premises TCO: include labor costs for activities that will be reduced or eliminated.</li>
  <li>Free services: IAM, VPC, <a href="https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/consolidated-billing.html">Consolidated Billing</a> (one bill, easy tracking, combined usege, no extra fee). Elastic Beantalk, CloudFormation and Auto Scaling Group are payed for created resources</li>
  <li><a href="https://aws.amazon.com/free/">Free Tiers</a>:
    <ul>
    <li>Always free: DynamoDB, Lambda, SNS, SQS, <a href="https://aws.amazon.com/cloudwatch/pricing/">ClaudWatch</a>, CloudFront, Cognito, CodeXXX, Glue, Storage Gateway, X-Ray, CloudTrail, Service Catalog, CloudFormation, Control Tower, AWS Organization</li>
    <li> 12 months free: EC2, S3, RDS, API Gateway, EFS, EBS, ELB, ElastiCache, Lex, Polly, Rekognition, Transcribe, Translate,  Amazon MQ, IoT, OpsWork, AppSync</li>
    <li>Trials: ECS, SageMaker, Redshift, AppStram, Lightsail, Comprehend Medical, Inspector, QuickSight, Macie, GuardDuty, Detective, Secrets Manager, DocumentDB, Neptune</li>
   </ul>
 </li>
</ul>

<p style="text-align: justify;">Pricing Models</p>
<ul>
  <li>Pay-as-you-go pricing: Pay for compute time; for data stored in cloud; for data transfer OUT of the cloud (<b>Massive economies of scale</b>)</li>
  <li>Save when you reserve: up to 75%. The more you pay upfront the greater the discount</li>
  <li>Pay less by using more: valume-based discount</li>
  <li>Pay less as AWS grows</li>
</ul>  


<p style="text-align: justify;">Costing Tools:</p>
<ul>
  <li><a href="https://calculator.aws/#/">Pricing calculator</a>: Estimating costs</li>
  <li>Tools for Tracking cost:
    <ul>
      <li>Billing dashboard </li> 
      <li>Cost Allocation <a href="https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html">Tags</a>: Tracking cost. Tags are used to organized resources.</li>
      <li>Cost and Usage Reports: set of cost and usage data available - can publish the reports to S3. Tracking cost</li>
      <li><a href="https://aws.amazon.com/aws-cost-management/aws-cost-explorer/">Cost Explorer</a>: Tracking costs. Visualize data as graph, understand, and manage your AWS costs and usage over time. Future cost projection. Filter by Region, AZ, tags etc.</li>
    </ul>
  </li>
  <li><a href="https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-what-is.html">Billing Alarms</a> and <a href="https://aws.amazon.com/aws-cost-management/aws-budgets">Budgets</a>: Monitoring against cost plans. The AWS Budget allows companies to track and categorize spending on a detailed level.</li>
  <li>AWS <b>Cost Anomaly Detection</b>: Continuously monitor your cost and usage using ML to detect unusual spends</li>
  <li>AWS <b>Service Quotas</b>: Notify when a service is close of the quota (maximum value for the resources, actions and item in account) value is achieved</li>
  <li><a href="https://aws.amazon.com/premiumsupport/technology/trusted-advisor/">AWS <b>Trust Advisor</b></a>: Analyse account and provide real-time <a href="https://aws.amazon.com/premiumsupport/technology/trusted-advisor/best-practice-checklist/">best practices</a> recommentation (Cost, performance, Security, Falt tolerance and Service limits). Ex: Checks security groups for rules that allow unrestrictec access to specific port.</li>
  <li>AWS <a href=" https://aws.amazon.com/compute-optimizer/"><b>Compute Optimizer</b></a>: Reduce costs and improve performance. Use ML. Helps the customer to choose optimal configuration and right size workload, including the CPU utilization and memory utilization. It delivers recommentations to EC2 instance, EC2 Scaling groups, EBS volumes and AWS lambda functions.</li>
</ul>  

<p style="text-align: justify;">AWS <b>Service Catalog</b>: stacks of authorized products</p>

<p><b>Aditional References</b></p>
<li><a href="https://digitalcloud.training/aws-billing-and-pricing/">DigitalCloud Summary</a></li>
<li><a href="https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html">Using AWS cost allocation tags</a></li>
<li><a href="https://aws.amazon.com/aws-cost-management/">Cloud Financial Management with AWS</a></li>



<!-- ################################################# -->


<br />
<hr>
<br />

<h2 id="support">Supports</h2>

<p style="text-align: justify;">Security-related actions are available at no cost:</p>
<ul>
  <li><a href="https://aws.amazon.com/blogs/aws/">AWS Blogs</a></li>
  <li><a href="https://forums.aws.amazon.com/index.jspa">AWS Forums</a></li>
  <li><a href="https://aws.amazon.com/whitepapers">AWS Whitepapers</a></li>
  <li><b>AWS Partner Solutions</b> (formerly <a href="https://aws.amazon.com/quickstart/">Quick Starts</a>): Partner Solutions are built by Amazon Web Services (AWS) solutions architects and partners to help you deploy popular technologies on AWS, based on AWS best practices for security and high availability</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/partners/">APN Consulting Partner</a>: The AWS Partner Network (APN) is the global partner program for technology and consulting businesses that leverage Amazon Web Services to build solutions and services for customers. So, if a company does not have expertise in-house and need to design and build a new workload on AWS Cloud, this program can be the ideal.</p>

<p style="text-align: justify;"><b>APN Technology Partner</b> provide hardware, connectivity services, or software solutions that are either hosted on or integrated with, the AWS Cloud. It does not help a migration process.</p>

<p style="text-align: justify;"><a href="https://aws.amazon.com/professional-services/"><b>AWS Professional Services</b></a> assistis customers with accelerating cloud adoption through paid engagements in any speciality area. It can help on migration.</p>

<p style="text-align: justify;"><a href="https://aws.amazon.com/managed-services/"><b>AWS Managed Services</b></a> (AMS): Provides infrastructure and application support on AWS; AMS business hours are 24/365; it takes care of underlyning instance or compute and therefore patching and hardening. It helps you adopt AWS at scale and operate more efficiently and securely. We leverage standard AWS services and offer guidance and execution of operational best practices with specialized automations, skills, and experience that are contextual to your environment and applications. You can easily leave a lot of the heavy lifting to AWS when you are using managed services</p>


<p style="text-align: justify;"><a href="https://aws.amazon.com/partners/aws-marketplace/">AWS Marketplace</a> is a digital catalog list of software that runs on AWS. It can be sell as Image (AMI) or SaaS.</p>

<p style="text-align: justify;"><a href="https://aws.amazon.com/premiumsupport/plans/">AWS Support Plans</a></p>
<ul><u><b>AWS Basic Support</b></u>
  <li>Customer Service & Communities - 24x7</li>
  <li>Documentation, Whitepapers, Support Forums</li>
  <li>Core checks from the AWS Trusted Advisor Best Practice Checks</li>
  <li>AWS Personal Health Dashboard</li>
</ul>
<ul><u><b>AWS Developer Support</b></u>
  <li>The same of the Basic</li>
  <li>Email access to customer Support: 24 hour response time on any question and 12 hours if the customer system is impaired</li>
  <li>When: testing or doing early development on AWS</li>
  <li>Best practices guidance</li>
  <li>Building-block architecture support</li>
  <li>Client side diagnotic tool</li>
</ul>
<ul><u><b>AWS Business Support</b></u>
  <li>The same of the Basic and Developer</li>
  <li>When: you have production workloads on AWS</li>
  <li>24x7 phone, email, and chat access to Cloud Support Engineers</li>
  <li>Production system impaired: < 4 hours</li>
  <li>Production system down: < 1 hour</li>
  <li>Full access to AWS Trusted Advisor Best Practice Checks.</li>
  <li><a href="https://docs.aws.amazon.com/health/latest/ug/health-api.html">AWS Health API</a></li>
  <li>Guidance, configuration and troubleshooting of AWS interoperability with third-party software</li>
</ul>
<ul><u><b>AWS <a href=" https://aws.amazon.com/premiumsupport/plans/enterprise/">Enterprise</a> Support</b></u>
  <li>The same of Basic, Developer and Business</li>
  <li>Technical Account Manager (TAM)</li>
  <li>Concierge Support Team for billing and account best practices. Experts that specialize in working with enterprise accounts. Focus on help customer achieve their outcomes.</li>
  <li>Business-critical system down: < 15 minutes (15 minutes SLA for business critical workload)</li>
  <li>Online training with self-paced labs</li>
  <li>24/7 technical support</li>
  <li>Consultative Architectural guidance</li>
</ul>
<ul><u><b>AWS Enterprise On-Ramp Support</b></u>
  <li>When: you have production/business critical workloads in AWS</li>
  <li>Business-critical system down: < 30 minutes</li>
  <li>Expert guidance to grow and optimize in the Cloud.</li>
  <li>Workshop to cost optimization</li>
</ul>


<!-- ########################################################## -->


<br />
<hr>
<br />

<h2 id="shots">Some Shots</h2>

<p style="text-align: justify;"><b>Computing Service</b>: Batch, EC2, EC2 Image Builder, Elastic Beanstalk, Lambda, Lightsail, AWS Outsposts, Serverless Application Repository, AWS SimSpace Weaver, AWS App Runner</p>

<p><b>Serverless</b>:</p>
<ul>
 <li>Compute: Lambda (Infra), Fargate</li>
 <li>Application Integration: EventBridge, Step Function (orchestration), SQS, SNS, API Gateway (Infra), AppSync</li>
 <li>Data Store: S3, EFS, DynamoDB, RDS, Aurora, Redshift, Neptune, OpenSearch</li>
</ul>

<p>Aditionally types there are:</p>
<ul>
  <li><b>FaaS</b> (Function as a Service): Lambda. </li>
  <li><b>DaaS</b> (Desktop as a Service): Amazon WorkSpace. </li>
</ul>

<p><b>Hybrid</b>: Storage Gateway, Outsposts, SSM, Route 53, Virtual Private Gateway</p>

<p><b>Audit</b>: CloudWatch, CloudTrail, SSE-KMS, AWS Config</p>

<p><b>Encryptation</b>: AZ traffic (Default), CloudTrail (default), Site-To-Site VPN (default), all storage (RDS, S3, EBS, Redshift, EFS)</p>


<!-- ########################################################## -->


<br />
<hr>
<br />

<h2 id="conclusion">Conclusion</h2>

<p style="text-align: justify;">The exam is not a big deal; however, there are a lot of services to remember what they mean. Generally, the exam will test you not so deeply but to see if you know what the services are and have a basic idea of where to use them.</p>

<p style="text-align: justify;">The courses I added here I consider complementary, so I recommend doing both. After that, do a lot of simulations. The simulation will help you understand what the exam is really trying to test you on.</p>

<p style="text-align: justify;">Good luck!</p>

<p><center>
  <img src="/img/infra/AWSPractioner.png" />
</center></p>