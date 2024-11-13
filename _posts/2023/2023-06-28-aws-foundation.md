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
    <td><a href="#globalinfra">AWS Global Infrastructure</a></td>
    <td><a href="#architect">AWS Well-Architected Framework</a></td>
  </tr>
  <tr>
    <td><a href="#iam">IAM</a></td>
    <td><a href="#orgcontrolpower">AWS Organization and Control Power</a></td>
    <td><a href="#ec2">EC2</a></td>
  </tr>

  <tr>
    <td><a href="#asg">High Availability and Scaling</a></td>
    <td><a href="#network">AWS networking services</a></td>
    <td><a href="#storage">AWS Storage Services</a></td>
  </tr>
  <tr>
    <td><a href="#decouple">Loosly Decouple</a></td>
    <td><a href="#serverless">Serverless Applications</a></td>
    <td><a href="#container">Containers</a></td>
  </tr>
  <tr>
    <td><a href="#database">AWS database services</a></td>
    <td><a href="#bigdata">Big Data</a></td>
    <td><a href="#deploy">Deployment</a></td>
  </tr>
  <tr>
    <td><a href="#monitoring">Monitoring</a></td>
    <td><a href="#security">Security</a></td>
    <td><a href="#migration">Migration</a></td>
  </tr>

  <tr>
    <td><a href="#machinelearning">Machine Learning</a></td>
    <td><a href="#others">Others Services</a></td>
    <td><a href="#pricing">Billing and Pricing</a></td>
  </tr>
  <tr>
    <td><a href="#support">Support</a></td>
    <td><a href="#shots">Some Shots</a></td>
    <td colspan="1"><a href="#conclusion">Conclusion</a></td>
  </tr>
</table>


<hr>
<br />

<p style="text-align: justify;">AWS has a lot of certifications and a few of them together defines a Role. You can see all the journeys <a href="https://d1.awsstatic.com/training-and-certification/docs/AWS_certification_paths.pdf">here</a>. As soon as you are  prepared, you can schedule your exam <a href="https://aws.training">here</a>. Two important benefits are 30 minutes more if you are not a native  English speaker, and 50% in your next test. </p>

<p style="text-align: justify;">A optional test is <a href="https://aws.amazon.com/certification/certified-cloud-practitioner/?ch=tile&tile=getstarted">AWS Certified Cloud Practitioner (CLF-C01)</a>, and the first mandatory is <a href="https://aws.amazon.com/certification/certified-solutions-architect-associate/?ch=sec&sec=rmg&d=1">AWS Certified Solutions Architect Associate (SAA-C03)</a>.</p>

<p style="text-align: justify;">The first step to start your journey is <a href="https://www.tutorialspoint.com/amazon_web_services/amazon_web_services_account.htm">creating your account</a> to do your tests. AWS has a <a href="https://repost.aws/knowledge-center/create-and-activate-aws-account">HowTo</a> for it. Don't forget to not use the root to do your tasks. You have to create user in AWS IAM service by <a href="https://aws.amazon.com/getting-started/hands-on/getting-started-with-aws-management-console/?ref=gsrchandson">AWS Management Console</a>. The default region available to the user is <b>North Virginia</b>.</p>

<p style="text-align: justify;">Some courses:</p>
<ul>
  <li><a href="https://www.udemy.com/course/aws-certified-cloud-practitioner-training-course/">Udemy Course: AWS Certified Cloud Practitioner Exam Treining</a></li>
  <li><a href="https://www.udemy.com/course/aws-certified-cloud-practitioner-new/">Udemy Course: [NEW] Ultimate AWS Certified Cloud Practitioner - 2023</a></li>
  <li><a href="https://www.udemy.com/course/aws-certified-cloud-practitioner-practice-exams-c/">AWS Certified Cloud Practitioner Practice Exams CLF-C01 2023</a></li>
  <li><a href="https://www.udemy.com/course/practice-exams-aws-certified-cloud-practitioner/">6 Practice Exams | AWS Certified Cloud Practitioner CLF-C01</a></li>

  <li><a href="https://www.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/?srsltid=AfmBOorzNJorKXzTS3Em5hppo_mNN1sFL3mJMRo4frUF-nD0hVNo5rql&couponCode=ST20MT111124A">Ultimate AWS Certified Solutions Architect Associate SAA-C03</a></li>
  <li><a href="https://www.udemy.com/course/aws-certified-solutions-architect-associate-hands-on/?srsltid=AfmBOorhqC5fI0UB9elZPwHObF9FAdz3SCIJCtdd8csSGV3DFcTed2fi&couponCode=ST20MT111124A">AWS Certified Solutions Architect Associate (SAA-C03) Course</a></li>
  
  <li><a href="https://www.pluralsight.com/cloud-guru/courses/aws-certified-solutions-architect-associate-saa-c03">[Cloud Guru] AWS Certified Solutions Architect - Associate (SAA-C03) </a></li>
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
  <li><a href="https://digitalcloud.training/aws-cloud-computing-concepts/">[DigitalCloudS] Concepts</a></li>
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
  <li><em>Virtually any on-premises or edge location</em></li>
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
<ul>
  <li><a href="https://digitalcloud.training/aws-global-infrastructure/">[DigitalCloud] Global Infrastructure</a></li>
  <li><a href="https://digitalcloud.training/aws-application-integration/">[DigitalCloud] AWS Application Integration Services</a></li>
  <li><a href="https://infrastructure.aws/">Regions and Availability Zones</a></li>
</ul>


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
  <li><a href="https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html">Cost Optimization</a>: run system to delivery value at the lowest price 
    <ul>
      <li>Design Principles: adopt a consumption mode, measure overall efficiency; stop spending money on data center operations; analyze and attribute expenditure; use managed and application level services to reduce cost</li>
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
  <li><a href="https://docs.aws.amazon.com/general/latest/gr/root-vs-iam.html"><b>Root</b></a> has <b>full administrative permissions</b> and complete access to all AWS services and resource.  <a href="https://docs.aws.amazon.com/accounts/latest/reference/root-user-tasks.html">Actions allowed only to root</a>: change account setting, close account, restore IAM permission, change or cancel AWS support plan, register as a seller, config S3 bucket to enable <a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html">MFA</a>, edit/delete S3 bucket policies. SCPs can limit the root account.</li>
  <li>When a Identity Federation (AD, facebook, SAML, OpenID) is configured, IAM user account is not necessary</li>
  <li>Power User has a lot of permission but not to manage groups and users in IAM.</li>
  <li>IAM Security Tool: 
    <ul>
      <li>IAM Credential Report (account-level): account's users and their credential status. Access it by IAM menu Credential Report</li> 
      <li><a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_access-advisor.html">IAM Access Advisor</a> (user-level): services permissions and last access. Access it by IAM User menu. Use it to identify unnecessary permissions that have been assigned to users.</li>
    </ul>
  </li>
</ul>

<p style="text-align: justify;"><b>User</b> is an entity (person or service) created without permissions (by default) with access to an AWS Accounts. They are create with NO access to any AWS services, only login to the AWS console. The permissions must be explicitly given. They log in using <em>user name</em> and <em>password</em>. They can change some configurations or delete resources in your AWS account. Users created to represent an application are known as "service accounts". It's possible to have 5000 users per AWS account.</p>

<p style="text-align: justify;"><b>Groups</b> are a way to organize the users (only) and apply <b>policies</b> (permissions) to a collection of users in the same time. A user can belong to multiple groups. Only users and cannot be nested (groups with groups). It is not an identity so cannot be referenced in policies.</p>

<p style="text-align: justify;"><b>Roles</b> delegate permissions. Roles are assumed by users, applications, and services. It can provides temporary security credentials (STS - Security Token Service) for customer role session. Also, the IAM roles make possible to access cross-account resources. It is a trusted entity.</p>

<p style="text-align: justify;">The <b>policy</b> manage access and can be attached to users, groups, roles or resources. When it is associated with an identity or resource it defines their permissions. It is a document written in JSON. The policy is evaluate when a user or role makes a request, and the permission inside that determine if the request is allowed or denied. The types of policies are:  identity-based policies (user, groups, roles), resource-based policies (resource), permissions boundaries (maximum permission), AWS Organizations service control policy (SCP)(maximum permission for an oganization), access control list (ACL), and session policies (AssumeRole* API action). <a href="https://docs.aws.amazon.com/en_us/IAM/latest/UserGuide/access_policies.html">Policy main elements</a>:
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
    <li>Use roles for applications that run EC2 and delegate permissions</li>
    <li>Rotate credentials</li>
    <li>Give only credentials that is really needed (Least privilege)</li>
</ul>


<p><b>Good Reads:</b></p>
<ul>
  <li><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html">IAM roles for Amazon EC2</a></li>
  <li><a href="https://aws.amazon.com/iam/">AWS Identity and Access Management</a></li>
  <li><a href="https://aws.amazon.com/blogs/database/using-iam-authentication-to-connect-with-pgadmin-amazon-aurora-postgresql-or-amazon-rds-for-postgresql/">Using IAM authentication to connect with pgAdmin Amazon Aurora PostgreSQL or Amazon RDS for PostgreSQL</a></li>
  <li><a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html">Policies and permissions in AWS Identity and Access Management</a></li>
  <li><a href="https://repost.aws/knowledge-center/iam-restrict-calls-ip-addresses">How can I use IAM roles to restrict API calls from specific IP addresses to the AWS Management Console?</a></li>
  <li><a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html?icmpid=docs_iam_console">Set an account password policy for IAM users</a></li>
  <li><a href="https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-iam-roles.html">Amazon ECS task IAM role</a></li>
  <li><a href="https://aws.amazon.com/iam/features/manage-roles/">Manage IAM Roles</a></li>
  <li><a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html">Policy evaluation logic</a></li>
</ul>


<!-- #################################################### -->


<br />
<hr>
<br />
<h2 id="orgcontrolpower">AWS Organization and Control Tower</h2>

<p style="text-align: justify;"><b>AWS Organization</b><a href="https://aws.amazon.com/organizations/">[1]</a><a href="https://digitalcloud.training/aws-organizations/">[2]</a>: </p>
<ul>
  <li>it is a collection of AWS accounts where is possible manage these accounts, apply polices, delegate responsibilities, apply SSO, share resources within the organization, use CloudTrail across the accounts.</li>
  <li>RAM easily share resources across AWS accounts. Free to use, pay by shared resources. Participants cannot modify shared resources.</li>
  <li>OU: Organization unit has a logical group of account</li>
  <li>For across-account access is better to create a role instead create a new IAM user. It gives temporary credentials.</li>
  <li>It provides volume discounts or EC2 and S3 aggregated across the member AWS account.</li>
  <li><a href="https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/consolidated-billing.html">Consolidate billing</a>: bill for multiple accounts and volume discounts as usage in all accounts is combined, easy to tracking or charges across accounts, combined usege across accounts and sharing of volume pricing discounts, reserved instance discounts and saving plans.</li>
  <li><b>Service Control Policies (SCPs)</b> is in AWS Organization and can control a lot of available permissions in AWS account, but NOT grant permissions. It can be used to apply the restrictions across multiple member accounts (deny rule). It affects only IAM users and roles (not resources policies)</li>
 </ul>


<p><b>Control Tower</b>:</p>
<ul>
  <li>It is over organization and give support to some adicional features, as create Landing Zone (multi-account baseline) and CT will deploy it.</li>
  <li>it set up and govern a secure and compliant multi-account AWS environment.</li>
  <li>Monitor compliance through a dashboard. Supports Preventive Guardrail using SCP (e.g, restrict regions across accounts); and Detective Gardrail using AWS Config (e.g, identity untagged resources). </li>
  <li>Features:
    <ul>
      <li>Landing Zone: well-architected, multi-account environment based on compliance and security best practices.</li>
      <li>Guardrails: high-level rules providing continuous governance -> preventive (ensures accounts maintain governance by disallowing violation actions; leverages service control policies; status of enforced or not enabled; supported in all Regions) and Detective (detects and alerts whithin all accounts; leverages AWS config rules; status of clear, in violation, or not enabled; apply to some regions)</li>
      <li>Account Factory: configurable account template</li>
      <li>CloudFormation StackSet: automated deployment of templates</li>
      <li>Shared accounts: three accounts used by Control Tower created during landing zone creation</li>
    </ul>
  </li>
</ul>


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
  <li><b>IaaS</b> (Infrastructure as a service)</li>
  <li>A new instance combine CPU, memory, Storage and networking. The different <a href="https://aws.amazon.com/ec2/instance-types/">types</a> were created to optimize different use case. The `t2.micro` is a general example of a type of instance. The first letter 't' represent the instance class, the number '2' represents the generation, and the last part is the size. Each category try to balance different characteristics:
    <ul>
      <li>compute: require high performance (batch, media transcoding, HPC, machine learning, gaming) - Ex. C8g </li>
      <li>memory: process large data sets in memory (relational/non-relational database, distributed cache, in-memory database for BI, real-time unstructured data) - Ex. R8g </li>
      <li>storage: high, sequencial read and write access to large data sets on local storage (OLTP, relational/non-relational database, cache, data wharehouse, distributed file systems) - Ex. I4g</li>
      <li>networking </li>
    </ul>
  </li>
  <li>Secure, resizable compute capacity in the cloud. Designed to make web-scale cloud computing easier for developers</li>
  <li>It can run virtual server instances in the cloud</li>
  <li>Each instance can run Windows/Linux/MacOS</li>
  <li>It can storing data (EBS/EFS), distributing load (ELB), scaling services (ASG)</li>
  <li>Volumes: <b>EBS</b> (persist) and <b>Instance Store</b> (Non-Persistent)</li>
  <li><b>Bootstrap scripts</b>: script that runs when the instance first runs (EC2 User data scripts). It can install updates, softwares, etc. Those scripts run with root user.</li>
  <li><b>Instance metadata</b> is information about the instance. User data and metadata are not encrypted. The metadata is available at <b>http://169.254.169.254/latest/meta-data</b></li>
  <li>When the instance is stopped and started again the public IP will change. The private IP not change.</li>
  <li>If you have a legacy, the EC2 instance is a good solution to migrate to cloud that is right-sized (right amount of resources for the application)</li>
  <li>Key pair to access EC2: public key (stored in AQS) + private key file (stored locally). It is used to connect to EC2 instance.</li>
  <li>Get metrics in CloudWatch, logs in CloudTrail</li>
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

<p style="text-align: justify;"><b>VMWare</b> on AWS: for hybrid cloud, cloud migration, disaster recovery, leverage AWS.</p>

<p style="text-align: justify;">Amazon EC2 <a href="https://aws.amazon.com/ec2/spot/">Spot Instances</a></p>
<ul>
  <li><em>Let you take advantage of unused EC2 capacity in the AWS cloud. Spot Instances are available at up to a 90% discount compared to On-Demand prices. You can use Spot Instances for various stateless, fault-tolerant, or flexible applications such as big data, containerized workloads, CI/CD, web servers, high-performance computing (HPC), and test & development workloads.</em></li>
  <li>Useful for workloads resilient to failure (batch, data analysis, Image processing, distributed workload, CI/CD and testing). However, it is not suitable for critical jobs or persistent workload and databases.</li>
  <li>Useful when workload is not immediate and can be stopped for a moment and continue from that point after</li>
  <li>Spot fleed: collection of spot on-demand. It will try and match the target capacity with your price restraints. Strategies: capacityOptimized, lowestPrice, diversified, InstancePoolsToUseCount</li>
</ul>

<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/imagebuilder/latest/userguide/what-is-image-builder.html"><b>EC2 Image Builder</b></a></p>
<ul>
  <li>It creates Virtual Machine or container images</li>
  <li>Automate the creation, maintain, validate and test EC2 AMIs</li>
  <li>The execution can be scheduled and after the process the AMI can be distributed (multiple regions)</li>
</ul> 

<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html">Amazon <b>AMI</b></a> (Amazon Machine Image)</p>
<ul>
  <li>Template of root volume + launch permissions + block device mapping the volumes to attach</li>
  <li>Launch EC2 - one or more pre-configured instance </li>
  <li>It can be customized </li>
  <li>it is build for a specific region. The AMI must be in the same region as that of the EC2 instance to be launched; but can be copied to another one where want to create another instance.</li>
  <li>It can be copied to other regions by the console, command line, or the API</li>
  <li>An EBS snapshot is created when an AMI is builded</li>
  <li>Category:
    <ul>
      <li>Amazon EBS: created from an Amazon EBS snapshot. It can be stopped. The data is not lost if stop or reboot. By default, the root device volume will be deleted on termination</li>
      <li>Instance Store: created from a template stored in S3. If delete the instance the volume will be deleted as well. If the instance fails you lose data, if reboot the data is not lost. It cannot stop the volume.</li>
    </ul>
  </li>
</ul> 

<p style="text-align: justify;"><b>EC2 Hibernate</b>: suspende to disk. Hibernation saves the contents from RAM to EBS root volume. When start again, EBS root volume is restored; RAM contents are reloaded. Faster to boot up. Maxmin days an instance can be in hibernation: 60 days.</p>

<p><b>Storage:</b></p>
<ul>
  <li>
    <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html"><b>EC2 Instance Store</b></a> is an alternative to EBS with a high-performance hardware disk, better I/O performance. However, it lose their storage when they stop. So, the best scenarios to be used are, e.g, buffer, cache, temporary content.
    <ul>
      <li>AWS: Infrastructure, Replication for data to EBS volumes and EFS drives, replacing faulty hardware, Ensuring their employees cannot access your data.</li>
      <li>Customer: backups and snapshot procesures, data encryptation, analysis the risk</li>
    </ul>
  </li>
  <li>
    <b>EBS</b> - Amazon Elastic Block Store <a href="https://aws.amazon.com/ebs/">[1]</a><a href="https://digitalcloud.training/amazon-ebs/">[2]</a><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html">[3]</a><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/RootDeviceStorage.html">[4]</a>
    <ul>
      <li>EBS <b>Volume</b>: attached to one instance.</li> 
      <li>Designed for mission-critical workload</li>
      <li>High Availability: Automatically replicated within a single AZ</li>
      <li>Scalable: dynamically increase capacity and change the volume type with no impact</li>
      <li>The EBS volumes not need to be attached to an instance. There is the root volume. Good practice create your own volume.</li> 
      <li>It allows the instance to persist data even after termination, however, Root EBS volumes are deleted on termination by default</li>
      <li>The EBS volumes cannot be accessed simultaneously by multiple EC2 instance (only with constrains): <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volumes-multi.html">Attach a volume to multiple instances with Amazon EBS Multi-Attach</a> Same AZ, only to SSD volume, allowed only in some regions, and others restrictions)</li> 
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
    <b>EFS</b> - Amazon Elastic File System <a href="https://aws.amazon.com/efs/">[1]</a><a href="https://docs.aws.amazon.com/efs/latest/ug/awsbackup.html">[2]</a><a href="https://digitalcloud.training/amazon-efs/">[3]</a> 
    <ul>
      <li>Network File System (NFS) for Linux instances and linux-based applications in multi-AZ.</li>
      <li>Shared File storage service using EC2.</li>
      <li>It is considered highly available, scalable, expensive, pay per use (Expensive).</li>
      <li>Tiers: frequent access (Standard) and not frequent access (IA)</li>
      <li>EFS Infrequent Access (EFS-IA) is a storage class that is cost-optimized for files not accessed and has lower cost than EFS standard. It is based on the last access. You can use a policy to move a file from EFS Standard to EFS-IA.</li>
      <li>Encryption at rest using KMS</li>
    </ul>
  </li>
  <li> <a href="https://aws.amazon.com/fsx/windows/">Amazon FSx</a>
    <ul>
      <li>for Windows File Server: fully managed Microsoft Windows file servers, manage native Microsoft windows file system. Make the migration easy</li>
      <li>for Lustre: managed file system that is optimized for compute-intensive workloads (HPC, Machine Learning, Media data Processing). Fo Linux File System. It can store data in S3.</li>
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

<p style="text-align: justify;">These are <a href="https://digitalcloud.training/auto-scaling-and-elastic-load-balancing/">features</a> to be used to ensure elasticity and high availability. They can be used together.</p>

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
  <li><a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/LaunchTemplates.html">Launch Template</a>: all the settings needed to build an EC2 instance; for all EC2 auto scaling features; supports versioning; more granularity; recommended. The specification of a network interface has considerations and limitations that need to be taken into account in order to avoid errors. <a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-launch-template.html#change-network-interface">[1]</a></li>
  <li>Launch Configuration: only certain EC2 Auto Scaling feature; immutable; limited configuration options; specific use cases</li>
</ul>


<p style="text-align: justify;"><b>Auto Scaling</b>: create and remove instance when is necessary. It can use a launch configuration (an instance configuration template) that an Auto Scaling Group uses to launch Amazon EC2 instances. <a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html">[1]</a><a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/launch-configurations.html">[2]</a><a href="https://aws.amazon.com/autoscaling/">[3]</a> </p>

<ul>
  <li>ASG contains a collection of EC2 instance (logical group)</li>
  <li>Replace unhealthy instances. </li> 
  <li>Only run at an optimal capacity.</li>
  <li>AWS EC2 Auto Scaling provides elasticity and scalability.</li>
  <li>High availability can be achieved with Auto Scaling balancing your EC2 count across the AZs <a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html">[1]</a></li>
  <li>Scaling Policies: minimum, maximum and <a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/asg-capacity-limits.html).">desired capacity</a> 
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
      <li><a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/schedule_time.html">Scheduled Scaling</a> (predictable workflow) can be configured for known increase in app traffic.</li> 
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
  <li><a href="https://aws.amazon.com/rds/aurora/serverless/">Aurora Serverless</a>: offload scaling to AWS. Unpredictable workloads. Aurora is the only engine that offers a serverless scaling option.</li>
</ul>

<p style="text-align: justify;">Scaling Non-Relational Database</p>
<ul>
  <li>AWS do this</li>
  <li>Types:
    <ul>
      <li><a href="https://aws.amazon.com/dynamodb/pricing/provisioned/">Provisioned</a>: predictable workflow; need to review past usage to set upper and lower scaling bounds; most cost-effective model</li>
      <li><a href="https://aws.amazon.com/dynamodb/pricing/on-demand/">On-Demand</a>: sporadic workflow; less cost effective;</li>
    </ul>
  </li>
  <li>Concepts:
    <ul>
      <li>Read Capacity Unit (<b>RCU</b>): DynamoDB unit of measure for reads per second for an item up to 4KB in size. As an example: if you have objects that are 7KB in size, then will be necessary 2 RCU for 1 strongly consistent read per second (1 RCU = 4KB/1 Strongly Consistent Read -> 2 RCU = 8KB)</li>
      <li>Write Capacity Unit (<b>WCU</b>): DynamoDB unit of measure for writes per second for an item up to 1KB in size. As an example: if you have an object that are 3KB in size, then will be necessary 3 WCU (1 WCU = 1KB * Write per Second -> 3 KB * 1 WCU = 3 WCUs ) </li>
    </ul>
  </li>
</ul>

<p><center>
  <img src="/img/aws/asg.png" height="100%" width="100%">
</center></p>


<p><b>Disaster Recovery</b></p>
<ul>
  <li><b>RPO</b> - Recovery Point Objective: point in time to recover (24h, 5 minutes, etc) (How often you run backups - back in time to get the data to recover)</li>
  <li><b>RTO</b> - Recovery Time Objective: how fast to recover; how long the business support (when recover after disaster)</li>
  <li>Strategies
    <ul>
      <li>Backup and Restore: Restore from a snapshot (Chepest but slowest)</li>
      <li>Pilot Light -  not consume the same level; provision 100% of the services to keep the applications up (faster than backup and restore but some downtime)</li>
      <li>Warm Standby - provision the services necessary to keep the applications up (quicker recovery time than Pilot Light but more expensive)</li>
      <li>Multi Site / Hot Site Approach: low RTO (expensive); full production scale is running AWS and on-premise</li>
      <li>All AWS Multi Region - the best approach for Data replication is use Aurora Global</li>
      <li>Active/Active Failover: is necessary to have a complete duplicated services (the most expensive but no downtime but lowest RTO and RPO)</li>    
    </ul>
  </li>
  <li>AWS <b>Elastic Disaster Recovery(DRS)</b>: recover physical, virtual and cloud-based servers into AWS</li>
</ul>

<p style="text-align: justify;">AWS <b>Backup</b>:</p>
<ul>
  <li>Supports PITR for supported services</li>
  <li>It can be done on-demand or schedule</li>
  <li>Cross-Region/Cros-Account backups</li>
  <li>Tag-based backup policies</li>
  <li>Backup Plans - frequency, retention</li>
  <li>Backup Vault Lock: enforce WARM (WriteOnceReadMany) for backups</li>
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

<p><b>AWS Global Accelerator</b><a href="https://aws.amazon.com/global-accelerator/">[1]</a><a href="https://digitalcloud.training/aws-global-accelerator/">[2]</a></p>
<ul>
  <li>Network service that send users' traffic through AWS's global network infrastructure via accelerators.</li>
  <li>Increase performance with IP cache</li>
  <li>By default, GA provides two static Anycast IP address</li>
  <li>For TCP and UDP (Major difference from CloudFront)</li>
  <li>Improve global application availability and performance</li>
  <li>Optimize the route to endpoints</li>
  <li>Use Edge Locations to the traffic</li>
  <li>Global Network</li>
  <li>Integration with Shield for DDoS protection</li>
  <li>No caching and has proxy packets at the edge</li>
  <li>Improve performance over TCP/UDP</li>
  <li>Global Accelerator can help deal with IP caching issues by providing static IPs</li>
  <li>Good when use static IP and need determinist and fast regional failover.</li>
  <li>Target: EC2 instances or ALB</li>
  <li>Both Route 53 and Global Accelerator can create weights for application endpoints</li>
</ul>

<p><b>Amazon CloudFront</b><a href="https://aws.amazon.com/cloudfront/">[1]</a><a href="https://digitalcloud.training/amazon-cloudfront/">[2]</a>:</p>
<ul>
  <li>Global (and fast) Content Delivery Network (CDN)</li>
  <li>It works with AWS and on-site architecture</li>
  <li>It can block countries, but the best place to do to it is WAF</li>
  <li>
    <ul>
      <li>Replicate part of your application to AWS Edge Locations (content is served at the edge)</li>
      <li>Edge location: location to cache the content</li>
      <li>It can use cache at the edge to reduce latency. Improves read performance</li>
      <li>It's possible to force the expiration of content or use TTL</li><li>
    </ul>
  </li>
  <li>Security: defauls to HTTPS connections and can add custom SSL certificate</li>
  <li>DDoS protection, integration with Shield, Firewall</li>
  <li>CloudFront commonly fronts S3 buckets</li>
  <li>S3 bucket: distribute files and caching at the edge, security with OAC (Origing Access Control)</li>
  <li>Customer origin: ALB, EC2 instance, S3 website</li>
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


<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/aws-storage-services/">DigitalCloud Summary</a></li>
<li><a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-iam-policies.html">Bucket policies and user policies</a></li>


<!-- ###################################################### -->

<br />
<hr>
<br />

<h2 id="decouple">Loosly Decouple</u></h2>

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
  <li>In scenarios of real-time should use Kinesis instead of SQS</li>
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
  <li>FanOut (SNS+SQS) <a href="https://aws.amazon.com/blogs/aws/kds-enhanced-fanout/">[1]</a> : messages published to SNS topic are replicated to multiple endpoint subscription (1:N)</li>
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
  <img src="/img/aws/decouple.png" height="100%" width="100%">
</center></p>


<!-- ############################################################# -->

<br />
<hr>
<br />
<h2 id="serverless">Serverless Applications</h2>


<p><b>Lambda</b> <a href="https://digitalcloud.training/aws-lambda/">[1]</a><a href="https://aws.amazon.com/blogs/architecture/best-practices-for-developing-on-aws-lambda/">[2]</a>: </p>
<ul>
  <li>FaaS</li>
  <li>Example of integration: ELB, API Gateway, Kinesis, DynamoDB, S3, CloudFront, CloudWatch, SNS, SQS, Cognito</li>
  <li>Virtual functions</li>
  <li>By default, Lambda function is launched outside of VPC, but it can be done in VPC</li>
  <li>Synchronous: CLI,SDK, API Gateway</li>
  <li>Asynchronous: S3, SNS, CloudWatch, etc</li>
  <li>Serverless</li>
  <li>Run on-demand</li>
  <li>Scaling automatically</li>
  <li>Event-driven</li>
  Security: Lambda bees IAM role to access AWS APIs <a href="https://docs.aws.amazon.com/lambda/latest/dg/lambda-intro-execution-role.html">[3]</a>
  <li>Can be monitoring through <b>CloudWatch</b></li>
  <li>Pricing: Pay per call (request) and duration (time of execution). Free tier of 1.000.000 requests and 400.000 GB of compute per month. After that, pay per request.</li>
  <li>Compute: 
    <ul>
      <li>1K councurrent execution</li>
      <li>Short-term execution (900 seconfs - 15minutes). If is necessary more time, use RC2, Batch, EC2</li>
    </ul>
  </li>
  <li>Storage: 
    <ul>
      <li>512MB-10GB disk storage (integration with EFS);</li>
      <li>4KB for all environment variables;</li>
      <li>128MB-10GB memory allocation</li>
      <li>Easily set memory - up to 10.240MB, and CPU scales proportionaly with memory</li>
    </ul>
  </li>
  <li>Deployment and configuration
    <ul>
      <li>Compressed deployment package <= 50MB</li>
      <li>Uncompressed package <= 250MB</li>
      <li>Request and response payload size up to 6BM</li>  
      <li>Streamed responses up to 20MB</li>
    </ul>
  </li>
  <li>Lambda@Edge: function attached to CloudFront to run close the user and minimize latency</li>
</ul>


<p><b>Serverless Application Repository</b></p>
<ul>
  <li>It allows users find, deploy, publish their own serverless application</li>
  <li>Privately share applications</li>
  <li>Deeply integrated with Lambda service</li>
  <li>Options:
    <ul>
      <li>Publish: makes apps available for others to find and deploy;SAM templates helps to define apps; private by default</li>
      <li>Deploy: Find and deploy published apps; Browse public apps wihtout an AWS account; Browse withoin Lambda Console</li>
    </ul>
  </li>
</ul>

<p><b>Aurora Serverless</b></p>
<ul>
  <li>On-Demand and Auto Scaling for Aurora database</li>
  <li>Automation of monitoring workloads and adjusting capacity for database</li>
  <li>Pricing: charged for resources consumed by DB cluster</li>
  <li>Concepts: Aurora Capacity Units (ACU - how the custer scale); allocated by AWS-managed warm pools; 2GiB of memory, matching CPU and networking capability; resiliency (six copies of data across three AZs)</li>
  <li>Use case: variable workfloes; multi-tentant apps (service manage capacity for each app); new apps; dev and test new features; mixed use apps; capacity planning</li>
</ul>

<p><b>GraphQL</b>: (AWS AppSync): robust, scalable GraphQL Interface for application developers; combines data from multiple sources; enable integration for developers via GraphQL (data language used by apps to fetch data from servers)</p>

<p>Other serverless service</p>
<ul>
  
  <li>SWF <a href="https://digitalcloud.training/aws-application-integration/#amazon-simple-workflow-service-amazon-swf">[1]</a></li>
</ul>


<!-- ############################################################# -->

<br />
<hr>
<br />
<h2 id="container">Containers</h2>


<p>Here are serverless services for containers <a href="https://digitalcloud.training/amazon-ecs-and-eks/">[1]</a>.</p>

<ul><u>Orchestration</u> 
  <li><b>ECS</b> (Elastic Container Service) <a href="https://aws.amazon.com/ecs/">[2]</a> 
    <ul>
      <li>ECS Launch Types: EC2 and Fargate</li>
      <li>Components:
        <ul>
          <li>Cluster: logical grouping of tasks or services. It can have ECS Container instances in different AZ</li>
          <li>Task: a running Docker container</li>
          <li>Container instance: EC2 instance running the ECS agent</li>
          <li>Service: Defines long running tasks. It can control number of tasks with Auto Scaling, and attach an ELB for distrubute traffic across containers</li>  
        </ul>
      </li>
      <li>Why: ECS manages anywhere many containers; ECS will place the containers and keep them online; containers are registered with LB; containers can have roles attached to them; easy to set up and scale</li>
      <li>Best used when all in on AWS</li>
      <li><a href="https://aws.amazon.com/ecs/pricing/">ECS Pricing</a></li>
      <li><b>Shared responsibility</b>
        <ul>
          <li>AWS start and stop the containers</li>
          <li>Customer has to provision and maintain the infrastructure (EC2 instance). </li>
        </ul>
      </li>
      <li>ECS anywhere:
        <ul> 
          <li>on-Premise, no orchestration, completely managed, Inboud traffic has to be managed separately (no ELB support)</li>
          <li>Requirement: SSM Agent, ECS Agent, Doker; register external instances; installation script within ECS console; execute scripts on on-premises VMs; deploy containers using EXTERNAl launch type</li>
        </ul>
      </li>  
    </ul>  
  </li>
  <li><b>EKS</b> (Amazon Elastic Container Service for Kubernetes) <a href="https://aws.amazon.com/eks/">[3]</a>:
    <ul>
      <li>Manage Kubernetes clusters on AWS</li>
      <li>Can be used on-premise and the cloud</li>
      <li>Best used when is not all in on AWS</li>
      <li>More work to configure and integrate with AWS</li>
      <li>EKS-D: managed bu developer. Self-managed Kubernetes deployment (EKS anywhere)</li>
      <li>EKS anywhere:
        <ul> 
          <li>on-Premise EKS, EKS Distro (deployment, usege and management for cluster), full lifecycle management</li>
          <li>Concepts: control plane, location, updates (manual CLI), Curated Packages, Enterprise Subscription</li>
        </ul>
      </li>
    </ul>
  </li>
</ul>  

<p><center>
  <img src="/img/aws/ecs.png" height="100%" width="100%">
</center></p>

<p><b>Fargate</b> <a href="https://aws.amazon.com/fargate/">[1]</a></p>
<ul>
  <li>Serverless compute engine for Docker container</li> 
  <li>AWS manage the infrastructure</li>
  <li>Works with ECS and EKS</li>
  <li>Benefits: no OS access, pay based on resources allocated and time ran (pay for vCPU and memory allocated - pricing model); short-running task; isolated environment ber container; capable of mounting EFS file system for persistent, shared storage. In some use cases it can be advantage comparing with <u>EC2</u>.</li>
  <li>Comparing with <u>Lambda</u>, select Fargate when the workload is more consistent (predictable). Also, Fargate allows docler use across the organization and some control by developer. By other hand, lambda is better to unpredictable or inconsistent workload; good for a single funcion.</li>
  <li>It is for containers and applications that need to run longer</li>
  <li><b>Shared responsibility</b>
    <ul>
      <li>AWS: Automatically provision resources. AWS runs the containers for the customer.</li>
      <li>The customer don't need provision the infrastructure. </li>
    </ul>
  </li>
</ul>

<p><b>ECR</b> - Elastic Container Registry</p>
<ul>
  <li>Managed container image registry</li>
  <li>Secure, scalable, reilable infrastructure</li>
  <li>Private conteiner image repository</li> 
  <li>Components: Registry (private); Authorization token (to push and pull images to and from retristries); Repository; Images</li>
  <li>Secure: permission via IAM; repository policy</li>
  <li>Cross-Region; Cross-account; configured per repository and per region</li>
  <li>Store customer images to be runned by ECS or Fargate</li>
  <li>Integration with customized container infrastructure, ECS, EKS, locally (linux - for development purpose)</li>
  <li>Use rules to expire and remove unsused images</li>
  <li>Scan on push repository can identify vulnerabilities</li>
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

<p>Amazon <b>ElastiCache</b><a href="https://aws.amazon.com/elasticache">[1]</a><a href="https://digitalcloud.training/amazon-elasticache/">[2]</a></p>
<ul>
  <li>Manage Mem cached</li>
  <li>Managed Redis</li>
  <li>Can be used in fron of any database but betther for RDS</li>
  <li>Service that adds caching layers on top of your databases</li>
  <li>In-Memory databases with high performance and low latency (under a millisecond)</li>
  <li>Support for clustering (Redis) and Multi AZ</li>
  <li>Security through IAM, Security Groups, KMS, Redis Auth</li>
  <li>Shared Responsibility: AWS takes care of OS maintenance / patching, optimizations, setup, configuration, monitoring, failure recovery and backups</li>
</ul>

<p><center>
  <img src="/img/aws/elasticache.png" height="100%" width="100%">
</center></p>

<p><b>Amazon DynamoDB</b><a href="https://aws.amazon.com/dynamodb/features/">[1]</a><a href="https://digitalcloud.training/amazon-dynamodb/">[2]</a><a href="https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html">[3]</a></p>

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
  <li>Cache: <a href="https://aws.amazon.com/dynamodb/dax/">DAX</a> (DynamoDB Accelarator)
    <ul>
      <li>It is fully managed in memory cache, the performance is improved, highly scalable and available. Only used with DynamoDB</li>
      <li>Lives inside the VPC
    </ul>
  </li>
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

<p style="text-align: justify;"><a href="https://aws.amazon.com/qldb"><b>QLDB</b></a>(Quantum Ledger Database): Fully managed graph database; no decentralization component; immutable ledger database. Ex: review a complete history of all the changes. NoSQL. Use cryptography. Immutable database.</p>

<p style="text-align: justify;"><b>Managed Blockchain</b>: create and manage blockchain networks with open-source frameworks</p>

<p style="text-align: justify;"><b>Amazon Keyspaces</b>: run Apache Cassandra workloads. Distributed database that uses NoSQL. Main application is big data but can be used for backend. Fully manage database. Pay for resource is used.</p>

<p><b>Neptune</b><a href="https://aws.amazon.com/neptune">[1]</a<a href="https://docs.aws.amazon.com/neptune/latest/userguide/intro.html">[2]</a>: Fully managed graph database. Good to app with highly connected datasets, as fraud detection and knowledge grapns. Used for analysis, build connections between identities, build knowledge, detect fraud patterns, security.</p>

<p style="text-align: justify;">Analyses</p>
<ul> 

  <li>Timestream: time series database service for IoT and operational application</li>
</ul>



<!-- ###################################################### -->



<br />
<hr>
<br />

<h2 id="bigdata">Big Data</h2>

<p>Characteristics of <a href="https://aws.amazon.com/blogs/big-data/">big data</a></p>
<ul>
  <li>Volume: Ranges from terabytes to petabytes of data.</li>
  <li>Variety: different sources and formats</li>
  <li>Velocity: needs short period of time</li>
</ul>

<p style="text-align: justify;"><b>Amazon Redshift</b><a href="https://aws.amazon.com/redshift">[1]</a><a href="https://docs.aws.amazon.com/redshift/latest/mgmt/working-with-snapshots.html">[2]</a><a href="https://digitalcloud.training/amazon-redshift/">[3]</a><a href="https://docs.aws.amazon.com/redshift/latest/dg/c-using-spectrum.html#c-spectrum-overview">[4]</a><a href="https://aws.amazon.com/blogs/big-data/amazon-redshift-spectrum-extends-data-warehousing-out-to-exabytes-no-loading-required/">[4]</a></p>

<ul>
  <li>Based on PostgreSQL (but not OLTP)</li>
  <li>Relational database for a analytic purpose</li>
  <li>OLAP - online analytical processing (analytics and data warehouseing)</li>
  <li>Parallel Query</li>
  <li>Run SQL against data warehouse</li>
  <li>Redshift Spectrum run queries against Amazon S3 without loading the data from Amazon S3 into data warehousing solution. Massive parallelism</li>
  <li>Size: up to 16PB of data</li>
  <li>Pricing: Pay as you go</li>
  <li>BI tools: AWS Quicksight or Tableau</li>
  <li>High Availability: supports Multi-AZ deployments</li>
  <li>Snapshots: are incremental and point-in-time. Always contained in S3</li>
  <li>Performance: always facor large batches inserts</li>
</ul>

<p style="text-align: justify;">Amazon EMR (Elastic MapReduce)<a href="https://aws.amazon.com/emr/features/">[1]</a><a href="https://digitalcloud.training/amazon-emr/">[2]</a></p>
<ul>
  <li>Help with ETL processing</li>
  <li>EMER is made up of EC2 instances</li>
  <li>Managed big data platform</li>
  <li>Storage:
    <ul>
      <li>Hadoop Distributed File System (HDFS) - distributes stored data across instance. Used for caching results</li>
      <li>EMR File System (EMRFS) - extends hadoop to access data in S3 which store input and output data.</li>
      <li>Localfile system - locally connected disck created with each EC2 instance (instance store volume)</li>
    </ul>
  </li>
  <li>EMR has cluster and Nodes</li>
  <li>Helps to create Hadoop clusters (Big Data)</li>
  <li>Take care of all the provisioning and configuration</li>
  <li>Auto Scaling</li>
  <li>Purchasing Options and Cluster types: OnDemand, reserved (min 1 year), Spot (cheapest option), long-running or transient</li>
  <li>Ex: machine learn and big data</li>
</ul>


<p><b>Kinesis</b> <a href="https://digitalcloud.training/amazon-kinesis/">[1]</a><a href="https://aws.amazon.com/blogs/big-data/streaming-data-from-amazon-s3-to-amazon-kinesis-data-streams-using-aws-dms/">[2]</a><a href="https://aws.amazon.com/kinesis/data-streams/">[3]</a><a href="https://aws.amazon.com/kinesis/data-streams/faqs/">[4]</a>: it is a message broker for real-time. it is a kind of big data pathway connected to a AWS account. It ingest, process and anlyze rel-time streaming data. </p>
<ul>
  <li>Amazon Kinesis Data Streams (KDS) <a href="https://digitalcloud.training/amazon-kinesis/">[1]</a> - For real-time for ingestinf data. The developer is responsible for creating the consumer and scaling the stream. It does not automatically scale</li>
  <li>Data Firehose: data transfer tool to get information to S3, Redshift, Elasticsearh, or Splunk. Near real time (60s). It is plug and play with AWS architecture. It scale automatically</li>
  <li>Kinesis Data Analytics and SQL: Easy, no servers, cost (pay for resources consumed). Easiest way to process data going through Kinesis using SQL</li>
  <li>It is more use to Big Data, but in scenarios quere is necessary real data, tt is better than SQS.</li>
</ul>

<p><b>Athena</b> <a href="https://digitalcloud.training/amazon-athena/">[1]</a><a href="https://aws.amazon.com/athena/features/">[2]</a>: </p>
<ul>
  <li>Analyze data in S3 using SQL;</li>
  <li>it is serverless (no infrastructure to manage);</li>
  <li>Pricing: you pay only for the queries that you run. Ex: BI, analytics, reporting</li>
  <li>Use case: Query logs -> Serverless solution - the only service that allow you to directly query data that's stored in S3</li>
</ul>

<p style="text-align: justify;"><b>Amazon Glue</b><a href="https://aws.amazon.com/glue/">[1]</a><a href="https://digitalcloud.training/aws-glue/">[2]</a></p>
<ul>
  <li>Serverless data integration</li>
  <li>Discover, prepare, and combine data for analytics</li>
  <li>ETL: extract, transform, and load service</li>
  <li>The AWS Glue Data Catalog is a central repository to store structural and operational metadata for all your data assets. </li>
  <li>Good working together with Athena: Athena can work by itself and Glue can design schema for the data</li>
  <li>It's possible to specify the number of DPUs (data processing unit) for an ETL job. A Glue ETL job must have a minimum of 2 DPUs. AWS Glue allocates 10 DPUs to each ETL job by default</li>
</ul>

<p><b>QuickSight</b><a href="https://aws.amazon.com/quicksight/">[1]</a>:  </p>
<ul>
  <li>Primarily used for analyzing log files and docs, specially within an ETL process</li>
  <li>scalable, serverless, embeddable, machine learning-powered business intelligence (BI) service</li>
  <li>Data visualization service -  dashboards</li>
  <li>Features: visualization, ad-hoc data analytics; integrates with RDS, Aurora, Athena, S3...</li>
  <li>Robust in-memory engine</li>
  <li>Colum-level security (CLS)</li>
  <li>Pricing per-session and use-based</li>
</ul>


<p><b>AWS Data Pipeline</b></p>

<Ul>
  <li>It is a managed ETL (Extract, Transform, Load ) service within AWS</li>
  <li>Implement automated workflows for movement and transformation of data between different compute and storage services</li>
  <li>Data source can be on-premise</li>
  <li>Define data-driven workflows</li>
  <li>Define parameters for data transformation</li>
  <li>Highly Availability and fault tolerant</li>
  <li>Handling Failures - automatically retries failed activities</li>
  <li>Integrate with DynamoDB, RDS, Redshift and S3</li>
  <li>Works with EC2 and EMR</li>
  <li>Components: Pipeline definition (business logic), Managed Compute (create EC2 instance), task runners, Data Notes (location and types of data)</li>
  <li>Use cases: processing data in EMR using Hadoop streaming; Importing or exporting DynamoDB data; Copying CSF files or data between S3 buckets; Exporting RDS data to S3</li>
  <li>Can use SNS for failure notification andsuccess and other event-driven workflow</li>
</Ul>


<p><b>Managed Streaming for Apache Kafka (Amazon MSK)</b></p>

<ul>
  <li>Managed service to dun data streaming that needs Kafka</li>
  <li>Control Plane: creates, updates and delete clusters</li>
  <li>Data Plane: leverage Kafka data-plane operations for producing and consuming streming data</li>
  <li>Components: Broker Nodes (amount of broker nodes per AZ); ZooKeeper Nodes; Producer, Consumers and Topics; Flexible Cluster Operations</li>
  <li>Resiliency: Automatic Recovery, detection of broker failures; Reduce data (reuse storage); Impact time is limited; After recovery, the same broker IP will be used again </li>
  <li>Serverless</li>
  <li>Security and Logging
    <ul>
      <li>Integration with KMS</li>
      <li>Encryption at rest bu default</li>
      <li>TLS for encryption in trasit between brokers in clisters</li>
      <li>Deliver broker logs to CloudWatch, S3, Kinesis Data Firehose</li>
      <li>Metrics are gathered and sent to CloudWatch</li>
      <li>MSK API calls are logged to CloudTrail</li>
    </ul>
  </li>
</ul>


<p><b>OpenSearch</b><a href="https://aws.amazon.com/elasticsearch-service/features/">[1]</a></p>
<ul>
  <li>Successor of Elasticsearch</li>
  <li>Managed analytics and visualization service</li>
  <li>Quick Analysis in clusters, usually par of an TLS process</li>
  <li>Search any field</li>
  <li>Can be used as a component to another database</li>
  <li>Easily Scalable</li>
  <li>Security: via Cognit and IAM, VPC SG (cluster can be deployed in a VPC), encryption at rest and in transit (KMS encryption, TLS), field-level security. Cannot use IP-based access policies.</li>
  <li>Backup using snapshot</li>
  <li>Create cluster (OS domain), specify the number of instances and type</li>
  <li>Storage options: UltraWarm or Cold storage</li>
  <li>Multi-AZ capable: up to three AZs</li>
  <li>Flexible - SQL for BI apps. Support SQL is not native but can be enable via plugin</li>
  <li>Integration with CloudWatch, CloudTrail, S3, Kinesis</li>
  <li>Use case - creating a logging solution involving visualization of log file analytics or BI report</li>
</ul>


<p><center>
  <img src="/img/aws/big-data.png" height="100%" width="100%">
</center></p>


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
  <li>Stack is a regional resource</li>
</ul>

<p>AWS Elastic <b>Beantalk</b><a href="https://aws.amazon.com/elasticbeanstalk/">[1]</a><a href="https://digitalcloud.training/aws-elastic-beanstalk/">[2]</a></p>
<ul>
  <li>Integrate with VPC and IAM</li>
  <li>ZIP, WAR, Git</li>
  <li>Plataform as a Service (PaaS)</li>
  <li>Monitoring, metrics, and health checks are all included</li>
  <li>Wasy-to-use service for deploying (on EC2) and scaling web applications and services developed with Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker on familiar servers such as Apache, Nginx, Passenger, and IIS.</li>
  <li>It can fully manage the EC2 instance or developer can control that</li>
  <li>Shared Responsibility
    <ul>
      <li>Aws: performe the deployment strategy, OS, capacity, load balancing, auto-scaling, health-monitoring and responsiveness</li>
      <li>Customer: deployment strategy configuration, application code</li>
    </ul>
  </li>    
  <li>Pricing: Free but you pay for the underlying instances</li>
</ul>


<p>AWS <b>Systems Manager</b> <a href="https://aws.amazon.com/systems-manager/faq/">[1]</a><a href="https://digitalcloud.training/aws-systems-manager/">[2]</a></p>
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
  <li>Summary
    <ul>
      <li>Capabilities: Automation, run command, patch manager, parameter store, maintenance windows, session manager</li>
      <li>Session Manager: logging (to CloudWatch and CLoudTrail), SSM Agent</li>
      <li>System Manager Agent (SSM Agent): makes possible for System Manager to update, manage, and configure resoures where the agent is installed</li>
      <li>Parameter Store: free to store config and secret values</li>
    </ul>
  </li>
</ul>

<p style="text-align: justify;">AWS <b>Amplify</b>: develop and deploy scalable full stack web and mobile application</p>

<p style="text-align: justify;">AWS <b>Devise Farm</b>: service to test web application and mobile</p>

<p style="text-align: justify;">AWS <b><a href="https://aws.amazon.com/pinpoint/">Pinpoint</a></b>: marketing communication service (email, sms, voice) - engage with customers</p>


-----
<p style="text-align: justify;">AWS <a href="https://aws.amazon.com/cdk/"><b>Cloud Development Kit (CDK)</b></a></p>
<ul>
  <li>Open-source software development framework.</li>
  <li>Define your cloud infrastructure using a familiar language.</li>
  <li>The code is compiled into a CloudFormation template</li>
  <li>Provisions the resources using CloudFormation</li>
</ul>

<p style="text-align: justify;">AWS <b>OpsWorks</b><a href="https://digitalcloud.training/aws-opsworks/">[1]</a></p>
<ul>
  <li>Like Chef and Puppet - perform server configuration automatically.</li>
  <li>Alternative to SSM</li>
  <li><a href="https://docs.aws.amazon.com/opsworks/latest/userguide/best-practices-storage.html">Best Practices: Root Device Storage for Instances</a></li>
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

<p><b>CloudTrail</b><a href="https://aws.amazon.com/cloudtrail/"></a><a href="https://digitalcloud.training/aws-cloudtrail/">[2]</a>: </p>
<ul>
  <li><b>Record API calls</b>. It tracks events (history events/API calls). Log, monitoring and retain account activity (Who, What, When)(track user activities and API requests and filter logs to assist with operational analysis and troubleshooting). </li>
  <li><b>Governance, compliance, audit for AWS account</b>. It can be applied to all regions or one. It has encryptation enabled as default. </li>
  <li>Enabling the <b>insights</b> allows CloudTrail detect automatically <b>unusual API activities</b> in the customer account. </li>
</ul>

<p><a href="https://digitalcloud.training/aws-config/">AWS Config</a>:</p>
<ul>
  <li>Inventory management and control tool (it's not preventative)</li>
  <li>Record configuration changes (<u>configuration history</u>)</li>
  <li>Receive alerts via SNS for alerting (change and compliance notification)</li>
  <li>EventBridge can send events from Config events to other AWS service</li>
  <li>Helps with auditing and recording compliance of the AWS resources, and record configurations and changes.</li>
  <li>Per <u>Region</u> but can be aggreated across region and account.</li>
  <li>It can send alerts for changes and the configuration can be store inside S3.</li>
  <li>Use case: discover the architecture in a account (query); create rules to monitor and receive alerts when that rules are violated (enforce); get the history (learn)</li>
  <li>Pricing: pay per item and rule evaluation</li>
  <li>Remediation: can be automatic via SSM automation document which can leverage Lambda function for custom logic</li>
</ul>

<p><b>EventBridge</b> <a href="https://aws.amazon.com/eventbridge/">[1]</a></p>
<ul>
  <li>Serverless event bus</li>
  <li>Pass events from a source to an endpoint</li>
  <li>Build event-driven applications at scale, schedule (cron jobs), event pattern, trigger lambda functions,send SQS/SNS message, etc.</li>
  <li>Events Bus is the router that receives events and delivers them to targets.</li> 
  <li>Use it to trigger an action based on an event in AWS</li>
  <li>Sucessor of CloudWatchEvents</li>
  <li>Fastest way to respond to things happening in the environment</li>
</ul>

<p><b><a href="https://aws.amazon.com/xray/">AWS X-Ray</a></b>:</p>
<ul> 
  <li>Serverless</li>
  <li>Collect data to get insights about requests and responses</li>
  <li>Traces - tracing headers, send trace data</li>
  <li>Debugging in Production.</li>
  <li>Benefits: performance, uderstand dependencies, review request, find errors, identify users, trace request across microservice/AWS Service.</li>
  <li>Contepts: Segments, subsegments, service graph, traces, tracing headers</li>
</ul>


<p><b>CodeGuru</b>: automated code review and application performance recommendations</p>

<p><b><a href="https://status.aws.amazon.com/">AWS Helth Dashboard</a></b>:</p>
<ul>
  <li>Provides a dashboard for viewing both public AWS service events and account-specific events that affect resources within your AWS accounts</li>
  <li>Provides you continuous visibility into your resource performance and availability of AWS services</li>
  <li>Service history (Service health Dashboard) for all regions or by your account (Account Helth Dashboard). </li>
  <li>It shows general status.</li>
</ul>

<p><b><a href="https://aws.amazon.com/premiumsupport/technology/personal-health-dashboard/">AWS Personal Health Dashboard</a></b>: </p>
<ul>
  <li>Personalized view of the status of the AWS services that are part of customer Cloud architecture.</li>
  <li>Alerts are triggered by changes in the health of your AWS resources, giving event visibility, and guidance to help quickly diagnose and resolve issues and.</li>
  <li>Customer can quickly assess the impact on your business when AWS service(s) are experiencing issues.</li>
  <li>It gives a personalized view of performance and availability of the services used by customer.</li>
</ul>


<p><center>
  <img src="/img/aws/monitor.png" height="100%" width="100%">
</center></p>


<!-- ####################################################### -->



<br />
<hr>
<br />

<h2 id="security">Security</h2>

<p style="text-align: justify;"><a href="https://aws.amazon.com/compliance/shared-responsibility-model/"><b>Shared Responsibility</b></a> has the customer responsible for security IN the cloud (data, access, authentication, configuration, encryptation, network traffic protection). AWS is responsible for the security OF the cloud, protecting/mnaging all AWS Global infrastructure (Software [compute, storage, database, networking], and hardware [regions, AZ, Edge Locations])</p>


<p><b><u>Examples of Atacck</u>:</b></p>

<ul>
  <li><b>DDos</b>: Distributed Denial-of-Service
    <ul>
      <li>Attempts to make the application unavailable to the end users</li>
      <li>Layer 4 DDoS Atack is the same SYN flood. It works at the transport layer (TCP). It involves the 3-way handshake to establish the connection (client -> SYN packet to a server -> server replies SYN-ACK -> Client responds ACK). The atack overwhelm the server with SYN-ACK.</li>    
    </ul>
  </li>
  <li><b>Amplification Attack</b>: attacker send a third-party server a request using spoofed IP address. Th server responds to that IO.</li>
  <li><b>Layer 7 attack</b>: application receives a flood of GET or POST requests</li>
</ul>


<p><b><u>AWS Security Services and strategies</u>:</b></p>

<p>Loggin API Calls with <a href="#monitoring">CloudTrail</a>: It allows after-the-fact incident investigation; near real-time intrusion detection; industry and regulatory compliance. Store the logs in S3</p>


<p>Protecting application with <b>AWS Shield Standard</b></p>
<ul>
  <li>Protect AWS customers on ELB, CloudFront and Route 53</li>
  <li>AWS Shield Standard: free for every customer, protect websites and applications (SYN/UDP floods, reflection attacks, and over layer 3 and 4 attacks). </li>
  <li>AWS Shield Advanced: protection 24/7, optional DDoS migration services; protection on EC2, ELB, CloudFront, GLobal Acceleator, Route 53 against more sophisticated attacks. Detection and mitigation for network layer (layer 3), transport layer (layer 4) and application layer (layer 7) attacks. Near real-time notifications of DDoS attacks.</li>
  <li><a href="https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/mitigation-techniques.html">Mitigate</a></li>
</ul>

<p><b>WAF</b> <a href="https://docs.aws.amazon.com/waf/latest/developerguide/how-aws-waf-works.html">[1]</a><a href="https://digitalcloud.training/aws-waf-shield/">[2]</a> (Web Application Firewall):</p>
<ul>
  <li>Filtering traffic: filter specific requests based on rules - requests sent to CloudFront, ELB, API Gateway.</li>
  <li>Protection on layer 7  (HTTP) DDoS attacks, SQL Injection and Cross-Site Scripting(XSS) </li>
  <li>Define Web ACL (Web Access Control List - rate-based rules).</li>
  <li>Protecting a website that is hosted outside of AWS (the on-premise IP is added to a target group).</li>
  <li>Configuring a firewall in front of resources is a <a href="https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/mitigation-techniques.html">good practice</a> to protect against DDoS</li>
  <li>In case use CloudFront and is necessary to block an IP, WAF must be with CloudFront to block that IP and not in ALB because, in this case, ALB just can see the CloudFront ID; and for the same reason NACL is not enough.</li>
  <li><a href="https://aws.amazon.com/waf/features/">AWS WAF features</a></li>
</ul>

<p><b>Firewall Manager</b></p>
<ul>
  <li>Centralized service to manage rules across multiple AWS account and applications in AWS Organization</li>
  <li>Simplify the management of Firewall rules across account</li>
</ul>

<p><b>GuardDuty</b> <a href="https://aws.amazon.com/guardduty">[1]</a>:</p>
<ul>
  <li>Threat detection service to protect AWS account</li>
  <li>Monitor suspicious activity</li>
  <li>It uses Machine Learning and check Logs.</li>
  <li>Identify potential security issues.</li>
  <li>Analyse CloudTrail events, VPC Flow Logs, etc.</li>
  <li>Ex: unusual API calls, malicious IP, unauthorized deployment, compromised instances</li>
  <li>Feature: Alerts in GuardDuty console and ClaudWatch Event; receive feeds from thord party (e.g., AWS Security inform malicious IP); monitor CloudTrail, VPC Flow logs and DNS logs; centralize detection across multiple AWS account; automate response with CloudWatch Events and Lambda</li>
  <li>Pricing: 30 days frew; quantity of CloudTrail Events; volume of DNS and VPC Flow Logs data</li>
</ul>

<p><b>Macie</b> <a href="https://aws.amazon.com/macie/">[1]</a>:</p>
<ul>
  <li>Monitoring S3 bucket</li>
  <li>Fully managed data security and data privacy service (Identify potential security issues).</li>
  <li>Personally Identifiable Information (PII) - personal data used to establish an individual's identity</li>
  <li>It uses machine learning and pattern matching to discover and protect customers sensitive data in S3</li>
  <li>Alerts to uncrypted buckets, public buckets, shared buckets</li>
</ul>


<p><b>Inspector</b> <a href="https://aws.amazon.com/inspector/">[1]</a>: </p>
<ul>
  <li>Automated security assessment service that helps improve the security and compliance of applications deployed on AWS. </li>
  <li>Inspect running operating systems (OS) against known vulnerabilities</li>
  <li>Exposure, vulnerabilities, and deviations from best practices</li>
  <li>Reports and Integration with AWS security Hub</li>
  <li>After performing the assessment, it produces a detailed list of security findings prioritized by level of severity</li>
  <li>Types of assessment: Netework and Host</li>
  <li>Analyze against unintended network accessibility</li>
  <li>Automated Security Assessments for EC2 instances, Container images, Lambda Functions.</li>
  <li>Send findings to Amazon Event Bridge.</li>
  <li>Continous scanning of the infrastructure when it is needed</li>
  <li>Can use an agent to monitoring</li>
  <li>Cannot be used to prevent Distributed Denial-of-Service (DDoS) attack</li>
</ul>

<p><b>Encryptation</b></p>
<ul>
  <li><b>KMS</b><a href="https://digitalcloud.training/aws-kms/">[1]</a> - Key Management Service
    <ul>
      <li>Encryptation for Software</li>
      <li>AWS manage the encryptation keys</li>
      <li>CMK - customer master key: can be generated by KMS, customer key management or CloudHSM
        <ul>
          <li>AWS managed CMK: create, managed and used on the customers behalf by AWS; used by AWS services</li>
          <li>Customer Managed CMK: create, manage, use, enable or disable; rotation policy</li>
          <li>AWS owned CMK: collections of CMKs owned by AWS to use in multiple accounts. The customer cannot see those keys.</li>
          <li>CloudHSM Keys: created by the device</li>
        </ul>
      </li>
      <li>The key can be routated</li>
      <li>Create policies to access KMS CMKs</li>
      <li>Control permissions: key policy; IAM + key policy; grants + key policy</li>
      <li>Sometimes is necessary to encrypt the <b>data in rest</b>(data stored or archived on device) or <b>in transit</b>(being moved from an origin to a destiny throgh network)</li>
      <li>Encryptation is possible in all storage and database: EBS Volume, S3 bucket, Redshift, RDS, EFS</li>
      <li>Encryptation is automatically enabled to: CloudTrail Logs, <a href="https://docs.aws.amazon.com/amazonglacier/latest/dev/DataEncryption.html">S3 Glacier</a>, Storage Gateway</li>
    </ul>
  </li>
  <li><b>CloudHSM</b><a href="https://aws.amazon.com/cloudhsm/">[1]</a><a href="https://digitalcloud.training/aws-cloudhsm/">[2]</a>: 
    <ul>
      <li>cloud-based HSM that anables easily generate and use your own encryption keys in AWS cloud</li>
      <li>Hardware Security Module (physical device)</li>
      <li>Encryptation for Hardware;</li>
      <li>The customer manages the encryptation keys; use HSM device (level 3 compliance)</li>
    </ul>
  </li>
  <li>The <b>AWS encryption SDK</b> is a <a href="https://docs.aws.amazon.com/en_us/AmazonS3/latest/userguide/UsingClientSideEncryption.html">client-side encryption</a> library that is separate from the language–specific SDKs</li>
  <li>Amazon <b>S3 Managed Keys</b> (SSE-S3) is a <a href="https://docs.aws.amazon.com/en_us/AmazonS3/latest/userguide/serv-side-encryption.html">server-side encryption</a> where each object is encrypted with a unique key. As an additional safeguard, it encrypts the key itself with a root key that it regularly rotates.</li>
  <li>Server-side encryption with AWS Key Management Service (AWS KMS) keys <b>(SSE-KMS)</b> is similar to SSE-S3, but using this service. It provides audit trail.</li>
</ul>


<p>AWS <b>Secrets Manager</b></p>
<ul>
  <li>Storing secrets</li>
  <li>Rotation of secrets</li>
  <li>Integration with RDS</li>
  <li>Secrets encrypted using KMS</li>
</ul>

<p><b>Parameter Store</b></p>
<ul>
  <li>provides secure, hiararchical storage for configuration data management and secrets management</li>
  <li>Pricing: FREE!!!</li>
  <li>Limits: 10.000</li>
</ul>


<p><b>ACM</b> - AWS Certificate Manager</p>
<ul>
  <li>Customer can provise, manage and deploy SSL/TSL certiticates</li>
  <li>Provide encryptation for websites (HTTPS)</li>
  <li>Free charge for TLS certificate</li>
  <li>Integration with ELB, CloudFront, API Gateway</li>
  <li>Pricing: free</li>
</ul>


<p><b>Audit Manager</b>: Automated service for <b>continuous auditing</b> that procuces reports for PCI compliance, GDPR, etc</p>


<p style="text-align: justify;"><b>AWS Artifact</b> <a href="https://aws.amazon.com/artifact/">[1]</a>: Artifact reports (AWS security and compliance document) and Artifact Agreements (AWS agreements). PS: <b>Audits and download compliance reports</b>. Ex: Service Organization Control (SOC) reports, Payment Card Industry (PCI)</p>

<p><b>Cognito</b> <a href="https://digitalcloud.training/amazon-cognito/">[1]</a><a href="https://aws.amazon.com/cognito/">[2]</a></p>
<ul>
  <li>AWS Cognito is a fully managed service that provides secure and scalable customer identity and access management (CIAM), enabling user authentication, authorization, and data synchronization across devices and platforms for web and mobile applications, with support for both authenticated and unauthenticated users.</li>
  <li>The main role of AWS Cognito is to serve as a Customer Identity and Access Management solution.</li>
  <li>Alternative to IAM.</li>
  <li>Authentication, authorization, and user management for web and mobile apps</li>
  <li>Identity for your Web and <b>Mobile</b> applications users (sign-up/sign-in; social identity like Facebook)</li>
  <li>External</li>
  <li>Components: user pools and identity pools</li>
</ul>


<p><b>AWS Detective</b>: </p>
<ul>
  <li>deep analyses to isolate the <b>root cause</b> of the security issues or suspicious activities (ML/graphs)</li>
  <li>Machine learning, statistical analysis, and graph theory</li>
  <li>Sources: VPC Flow logs, CloudTrail logs, Kubernates audit logs, GuardDuty findings</li>
  <li>Use case: Triage security findings; Threat Hunting</li>
</ul>


<p><b>Network Firewall</b>: </p>
<ul>
  <li>Managed service that makes it easy to deploy physical firewall protection across VPCs.</li>
  <li>Use cases: Filter internet traffic; Finter outbound traffic; inspect VPC-to-VPC traffic.</li>
  <li>Scenario: Filtering the network traffic before it reaches the Internet Gateway, or intrusion requirement prevention system, or any hardware firewall requirement</li>
</ul>

<p><b>AWS Security Hub</b>:</p>
<ul>
  <li>Central Security Hub to view all security alerts</li>
  <li>Across multiple Accounts</li>
  <li>Automate security Checks. Create a dashboard. Identify potential security issues.</li>
</ul>
 



---


<p style="text-align: justify;"><a href="https://aws.amazon.com/config/">AWS <b>Config</b></a>:</p>
<ul>
  <li>Enables customer to assess, audit, and evaluate the configurations of their AWS resources.</li>
  <li>Continuous monitoring.</li>
  <li>Track all changes in the resources</li>
  <li>Auditing and recording compliance, configurations</li>
  <li>Allows automating the evaluation of recorded configurations</li>
  <li>Per region service; can be aggregated across regions and accounts</li>
</ul>

<p style="text-align: justify;">AWS <b>Directory Service</b><a href="https://digitalcloud.training/aws-directory-services/">[1]</a>:</p>
<ul>
  <li>It is fully manage version of Microsoft Active Directory (Database of objects (user, accounts, computers, etc).</li>
  <li>Centralized security management)</li>
  <li>Build AD in AWS</li>
  <li>Create a tunnel between AWS and on-premise AD</li>
  <li>Standalone directory pwered by Linux Samba Active Directory</li>
  <li>Managed Microsoft AD: migrate into AWS</li>
  <li>Ad Connector: leave on-primise but not move yet</li>
</ul>


<p style="text-align: justify;"><b><a href="https://aws.amazon.com/security/penetration-testing/">Penetration Testing</a></b></p>
<ul>
  <li>Against customer AWS infrastructure without prior approval, e.g. EC2 instances, NAT Gateway, ELB, RDS, CloudFront, Aurora, API Gateway, Lambda, Beanstalk environment and LightSail resources</li>
  <li>It cannot: Dos, Port flooding, etc</li>
</ul>





<p style="text-align: justify;"><a href="https://aws.amazon.com/premiumsupport/knowledge-center/report-aws-abuse/"><b>AWS Abuse</b></a>: Report suspected AWS resources used for abusive or illegal purposes (spam, port scanning, DoS, DDoS, etc)</p>

<p style="text-align: justify;">AWS <b>STS</b> - Security Token Service: temporary (short-term credentials), limited privileges credentials</p>



<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html"><b>AWS IAM Access Analyzer</b></a>: identify the resources in your organization and accounts, such as Amazon S3 buckets or IAM roles, shared with an external entity. This lets you identify unintended access to your resources and data, which is a security risk.</p>

<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/aws-security-services/">(DigitalCloud) Summary</a></li>
<li><a href="https://digitalcloud.training/aws-cloud-management-services/">(DigitalCloud) AWS Cloud Management Services</a></li>
<li><a href="https://aws.amazon.com/security/">AWS Cloud Security</a></li>




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


<p style="text-align: justify;"><a href="https://aws.amazon.com/snow"><b>Snow Family</b></a></p>
<ul>
  <li>Highly-secure, portable devices to collect and process data at the edge, and migrate data into and out of AWS</li>
  <li>Data migration: 
    <ul>
      <li>Snowcone: less size of storage, it is a small device, send data to AWS offline or using AWS DataSync (8TB of storage, $GB of memory, 2vCPUs)</li>
      <li>Snowball Edge (Storage Optimized (80TB) /Compute Optimized (42TB tp 81TB): data transfer throught the network, pay per data transfer job (Ex: disaster revovery), can have Storage Clustering (up to 15 nodes.) EC2 does this natively support. EC2 compute instance can be hosted on a Snowball.</li>
      <li>Snowmobile: More capacity (100PB - exabytes), high security</li>
    </ul>  
  </li>
  <li>Edge computing: Snowcone, Snowball Edge. Process data while it's being create on an edge location (Ex: process data, machine learning, transcoding media streams)</li>
  <li>OpsHub manage Snow Family device.</li>
  <li>Snowball Pricing: per data transfer job</li>
</ul>

<h3>Storage Gateway</h3>

<p style="text-align: justify;"><b>Storage Gateway</b><a href="https://docs.aws.amazon.com/storagegateway/latest/userguide/WhatIsStorageGateway.html">[1]</a><a href="https://aws.amazon.com/storagegateway/">[2]</a></p>
<ul>
  <li>Hybrid cloud storage service that helps to merge on-primes resources with cloud</li>
  <li>File Gateway caching local files in on-premise side. It extends on-primises storage and helps with migration. The data goes to AWS to Storage Gateway or S3</li>
  <li>Volume gateway is a kind of backup drive in on-premise. It can help in migration. The data does throught Storage Gateway to S3</li>
  <li>Tape gateway help the migration sending data throught Storage Gateway to Tape Archive (S3 Glacier) in AWS</li>
  <li>It is a hybrid cloud storage service: a bridge between on-premise data and cloud data in S3.</li>
  <li>Simplify storage management and reduce costs for key hybrid cloud storage use cases</li>
  <li>Virtually unlimited cloud storage</li>
  <li>Cannot be used to data archival</li>
  <li>Types: File Gateway, Volume Gateway and Tape Gateway</li>
  <li>Ex: moving backups to the cloud, low latency access, disaster recovery</li>
</ul>


<p>AWS <b>DataSync</b> <a href="https://aws.amazon.com/datasync/">[1]</a>:</p>
<ul>
  <li>Great for online data transfers to simplify, automate, and accelerate copying large amounts of data between on-premises storage, edge locations, other clouds, and AWS Storage services.</li>
  <li>Agent-based solution for migrating on-premises storage to AWS.</li>
  <li>Agent for self-managed locations</li>
  <li>The agent is not necessary when transferring data betwenn AWS storage in the same AWS account</li>
  <li>Move data between NFS/SMB and AWS storage solutions</li>
  <li>DataSync encrypts data in-transit via TLS.</li>
  <li>DataSync works best as a solution for one-time data migration.</li> 
  <li>DataSync can transfer data to archival storage, such as S3 Glacier Deep Archive.</li> 
</ul>


<p>AWS <b>Transfer Family</b> <a href="https://aws.amazon.com/aws-transfer-family/">[1]</a>:</p>
<ul>
  <li>Transfer Family allows you to integrate legacy applications that use FTPS and S3 together</li>
  <li>Move files in and out S3 or EFS using SFTP, FTPS, FTP.</li>
  <li>Easiest way to change nothing.</li>
</ul> 


<p>AWS <<b>Application Discovery Service</b><a href="https://docs.aws.amazon.com/application-discovery/latest/userguide/what-is-appdiscovery.html">[1]</a> </p>
<ul>
  <li>helps you plan your migration to the AWS cloud by collecting usage and configuration data about your on-premises servers.</li>
  <li>Types: Agentless and Agent Based</li>
  <li>RTO: Recovery Time Objective</li>
  <li>RPO: Recovery Point Objective</li>
</ul>

<p>AWS <b>Application Migration Service (MGN)</b> <a href="https://aws.amazon.com/application-migration-service/">[1]</a><a href="https://digitalcloud.training/aws-migration-services/">[2]</a>:</p>
<ul>
  <li>Plan migration projects</li>
  <li>Agentless Discovery or Agent-based</li>
  <li>This service is an automated lift-and-shift (rehost) solution for expediting migration of apps to AWS and can be used for physical, virtual, or cloud servers to avoid cutover windows or disruptions.</li>
  <li>Migrating to run natively on AWS</li>
</ul>


<p><b>DMS</b> (Database Migration Service) <a href="https://aws.amazon.com/dms/">[1]</a>:</p>
<ul>
  <li>Migrate to AWS (relational DBs, data warehouse, NoSQL, other data stores).</li>
  <li>With this is possible do continuous replication (ex: send to data warehouse)</li>
  <li>Option: perform a one-time migration or continuously replicate ongoing changes</li>
  <li>Types: Full Load; Full load and change Data capture (CDC); CDC only</li>
  <li>Source DB -> EC2 instance running DMS -> Target DB</li>
  <li>When Multi-AZ enabled, DMS give a synchronous stand replica in different AZ</li>
</ul>

<p><b>AWS Migration Hub</b> <a href="https://aws.amazon.com/migration-hub/features/">[1]</a>:</p>
<ul>
 <li>single location to track the progress of application migrations</li>
 <li>Integrate with Server Migration Server(SMS) and Database Migration Servie (DMS)</li>
</ul>

<p style="text-align: justify;"><b>AWS Server Migration Service (SMS)</b> is a fast agentless service easy to migrate thousands of on-premises workloads to AWS</p>



<!-- #################################################### -->



<br />
<hr>
<br />

<h2 id="machinelearning">Machine Learning</h2>

<p>Amazon <b>Rekognition</b>: find objects, people, text in images and videos. Create "familiar faces" database or compare against celebrities.</p>

<p>Amazon <b>SageMaker</b>: service for build, train and deploy machine models.</p>

---

<p><a href="ttps://aws.amazon.com/transcribe/">Amazon <b>Transcribe</b></a>: Convert speech to text.(deep learning process. Automatically remove Personal Identifiable Information (PII)</p>

<p><a href="https://aws.amazon.com/polly/">Amazon <b>Polly</b></a>: Turn text into lifelike speech. Deep learning.</p>

<p>Amazon <b>Translate</b>: Natural and accurate language translation</p>

<p>Amazon <b>Lex</b>: Automatic Speech Recognition (ASR) - speech to text (chatbots, call center bots)</p>

<p>Amazon <b>Connect</b>: receive calls, create contact flows</p>

<p>Amazon <b>Comprehend</b>: Natural Language Processing (NLP), serverless service; analyses and organize text; identify positive/negative experience </p>

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

<p style="text-align: justify;">AWS <b>Fault Inject Simulator (FIS)</b>: based on chaos engineering. stressing test.</p>

<p style="text-align: justify;">AWS <b>Ground Station</b>: control satellite communication</p>


<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/additional-aws-services/">DigitalCloud Summary</a></li>
<li><a href="https://aws.amazon.com/developer/tools/">Tools to Build on AWS</a></li>  
<li><a href="https://aws.amazon.com/datapipeline/">AWS Data Pipeline</a></li>




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
      <li><a href="https://aws.amazon.com/aws-cost-management/aws-cost-explorer/">Cost Explorer</a>: Tracking costs. Visualize data as graph, understand, and manage your AWS costs and usage over time. Future cost projection. Filter by Region, AZ, tags etc. Features: Time, filter, service</li>
    </ul>
  </li>
  <li><a href="https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-what-is.html">Billing Alarms</a> and <a href="https://aws.amazon.com/aws-cost-management/aws-budgets">Budgets</a>: Monitoring against cost plans. The AWS Budget allows companies to track and categorize spending on a detailed level.</li>
  <li>AWS <b>Cost Anomaly Detection</b>: Continuously monitor your cost and usage using ML to detect unusual spends</li>
  <li>AWS <b>Service Quotas</b>: Notify when a service is close of the quota (maximum value for the resources, actions and item in account) value is achieved</li>
  <li><a href="https://aws.amazon.com/premiumsupport/technology/trusted-advisor/">AWS <b>Trust Advisor</b></a>: fully managed best-practices <u>audit tool</u>. Analyse account and provide real-time <a href="https://aws.amazon.com/premiumsupport/technology/trusted-advisor/best-practice-checklist/">best practices</a> recommentation (Cost, performance, Security, Falt tolerance and Service limits). Ex: Checks security groups for rules that allow unrestrictec access to specific port. It is account level. Check Categories: Cost Optimization; Performance; Security; Fault Tolerance; Service Limits</li>
  <li>AWS <a href=" https://aws.amazon.com/compute-optimizer/"><b>Compute Optimizer</b></a>: Analyzes configurations and utilization metrics. Reports current usage optimizations and recomendation. Reduce costs and improve performance. Use ML. Helps the customer to choose optimal configuration and right size workload, including the CPU utilization and memory utilization. It delivers recommentations to EC2 instance, EC2 Scaling groups, EBS volumes and AWS lambda functions.</li>
</ul>  

<p style="text-align: justify;">AWS <b>Service Catalog</b>:</p>
<ul>
  <li>Stacks of authorized products</li>
  <li>Allows organizations to create and manage catalogs of IT services</li>
  <li>List resources like AMIs, servers, sofwtares, database,etc</li>
  <li>Centralized service</li>
  <li>EndUser can deploy preapproved catalog items within an organization</li>
  <li>Catalog templates are written and listed using CloudFormation templates</li>
  <li>Benefits: standardize, senf-service, access control, versioning</li>
</ul>

<p>AWS Proton</p>
<ul>
  <li>It is a service that creates and manages infrastructure and deployment tooling</li>
  <li>Automate IaC provisioning and deplyments</li>
  <li>Define standardized infrastructure</li>
  <li>Use templates to define and manage app stacks</li>
  <li>automatically provisions resources, configure CI/CD pipelines, and deploys code</li>
  <li>Supports CloudFormation and Terraform</li>
</ul>

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