---
layout: post
title:  "AWS Cloud Practitioner - Foundational"
date:   2023-06-28
categories: infra
permalink: /:categories/aws-foundational
---


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


<table>
  <tr>
    <td><a href="#concept">Cloud Concepts</a></td>
    <td><a href="#globalinfra">AWS Global Infrastructure</a></td>
    <td><a href="#network">AWS networking services</a></td>
  </tr>
  <tr>
    <td><a href="#compute">AWS compute services</a></td>
    <td><a href="#storage">AWS Storage Services</a></td>
    <td><a href="#database">AWS database services</a></td>
  </tr>
  <tr>
    <td><a href="#others">Others Services</a></td>
    <td><a href="#migration">Migration</a></td>
    <td><a href="#security">Security</a></td>
  </tr>
  <tr>
    <td><a href="#machinelearning">Machine Learning</a></td>
    <td><a href="#pricing">Billing and Pricing</a></td>
    <td><a href="#architect">AWS Well-Architected</a></td>
  </tr>
  <tr>
    <td><a href="#support">Support</a></td>
    <td><a href="#shots">Some Shots</a></td>
    <td><a href="#conclusion">Conclusion</a></td>
  </tr>
</table>

<p>Here are some notes using those courses as support.</p>

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

<p style="text-align: justify;"><b>Scalability</b></p>
<ul>
  <li>Handle greater loads by adapting</li>
  <li><b>Scale Up</b>: scale by adding more power (CPU/RAM) to existent machine/node. Operation running on only one computer.</li>
  <li><b>Scale Out</b>: scale by adding more instance to existent pool of resources.  Fault Tolerance is achieved by scale out operation.</li>
  <li><b>Vertical</b>: inscrease the size of the instance. Common for non distributed system. Limited, e.g, by hardware.</li>
  <li><b><a href="https://wa.aws.amazon.com/wat.concept.horizontal-scaling.en.html">Horizontal</a></b>: increase the number of instances. Distributed system. Common for web applications. <a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html">Auto Scaling</a> Group and Load Balancer</li>
  <li><b>High Availability</b>: Direct relatioship with horizontal scalability. No interruption even with failover. Run across <a href="https://aws.amazon.com/rds/features/multi-az/">multi AZ</a>, at least in 2 AZ</li>
</ul>

<p style="text-align: justify;"><b>ASG</b> (<a href="https://aws.amazon.com/autoscaling/">Auto Scaling</a> Group): </p>
<ul>
  <li>ASG contains a collection of EC2 instance (logical group)</li>
  <li>Monitors and automatically adjusts the capacity; predictable performance at the lowest possible cost. It, e.g, add/remove (Scale out/in) EC2 instances when the load is increased/decreased. </li>
  <li>Replace unhealthy instances. </li> 
  <li>Only run at an optimal capacity.</li>
  <li>AWS EC2 Auto Scaling provides elasticity and scalability.</li>
  <li>A <a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/schedule_time.html">scheduled scaling policy</a> can be configured for known increase in app traffic (predictable load changes)</li>
  <li>Predictive scaling: uses daily and weekly trends to determine when scale</li>
  <li>Step scaling policy: launch resources in response to demand. It's not a guarantee the resources are ready when necessary</li>
  <li><b>Strategy</b>: Manual or Dynamic (1. SimpleStep Scaling (CloudWatch); 2.Target Tracking Scaling; 3. Scheduled Scaling</li>
  <li><a href="https://digitalcloud.training/auto-scaling-and-elastic-load-balancing/">DigitalCloud Summary</a></li>
</ul> 

<p style="text-align: justify;"><b><a href="https://aws.amazon.com/serverless/">Serverless</a>:</b> <em>technologies for running code, managing data, and integrating applications, all without managing servers. Serverless technologies feature automatic scaling, built-in high availability, and a pay-for-use billing model to increase agility and optimize costs. It eliminates infrastructure management tasks like capacity provisioning, patching and OS maintenance.</em> It not mean no server.</p>  

<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/aws-cloud-computing-concepts/">DigitalCloudSummary</a></li>
<li><a href="https://digitalcloud.training/auto-scaling-and-elastic-load-balancing/">(DigitalCloud) Auto Scaling and Elastic Load Balancing</a></li>
<li><a href="https://aws.amazon.com/what-is-cloud-computing/?nc2=h_ql_le_int_cc">AWS - What is cloud computing?</a></li>

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

<p style="text-align: justify;"><a href="https://aws.amazon.com/cloudfront/"><b>Amazon CloudFront</b></a>: Global Content Delivery Network (CDN)</p>
<ul>
  <li>Replicate part of your application to AWS Edge Locations (content is served at the edge). </li>
  <li>It can use cache at the edge to reduce latency. Improves read performance. </li>
  <li>DDoS protection, integration with Shield, Firewall</li>
  <li>S3 bucket: distribute files and caching at the edge, security with OAC (Origing Access Control)</li>
  <li>Customer origin: ALB, EC2 instance, S3 website</li>
  <li>Great for static content that must be available everywhere; in oposite of S3 Cross Region Replication that is great for dynamic content that needs to be available at low latency in few regions</li>
  <li><b>Pricing</b>: Traffic distribution; Requests; Data transfer out. Price is different for region</li>
</ul>

<p style="text-align: justify;"><b>S3 Transfer Acceleration</b></p>
<ul>
  <li>Accelerate global uploads & downloads into Amazon S3</li>
  <li>Increase transfer speed to Edge Location</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/global-accelerator/"><b>AWS Global Accelerator</b></a></p>
<ul>
  <li>Improve global application availability and performance</li>
  <li>Optimize the rote</li>
  <li>Use Edge Locations to the traffic</li>
  <li>Global Network</li>
  <li>Integration with Shield for DDoS protection</li>
  <li>No caching and has proxy packets at the edge</li>
  <li>Improve performance over TCP/UDP</li>
  <li>Good when use static IP and need determinist and fast regional failover.</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/outposts/"><b>AWS Outspots</b></a></p>
<ul>
  <li><em> virtually any on-premises or edge location</em></li>
  <li>Hybrid cloud</li>
  <li>Server racks -> customer is responsible for that</li>
  <li>Low latency, local data, data residency, easier migration, fully managed service</li>
</ul>  

<p style="text-align: justify;"><a href="https://aws.amazon.com/wavelength/"><b>AWS WaveLength</b></a>: Infrastructure embedded within the telecommunication provides datacenters at 5G network</p>
 
<p style="text-align: justify;">Cloud Integration (the services can be scale)</p>
<ul>
  <li><b>SQS</b> (cloud native service): queue model. Retention os message (4-14 days) and deleted after to be read. Decouple. Distributed application. Pay-as-you-go pricing.</li>
  <li><a href="https://aws.amazon.com/sns/"><b>SNS</b></a> (cloud native service): pub/sub model. It can send a message to many receivers. Publisher -> SNS topic. Subscriber -> get all messages from the topic</li>
  <li>Amazon MQ: message broker. Good when migrating to the cloud</li>
  <li><b>Kinesis</b>: real-time data streaming model</li>
</ul>  

<p style="text-align: justify;">Cloud Monitoring</p>
<ul>
  <li><a href="https://aws.amazon.com/cloudwatch/"><b>CloudWatch</b></a> (Metrics, Logs, Alarms, Events): It is a  monitoring and observability service. Provide <b>metrics</b> and <b>insights</b> (interactively search and analyze log data). The alarms trigger notifications for metric. The <a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html">CloudWatch Logs</a> enable real-time monitoring, can store and access customers log file from EC2 instance, CloudTrail, etc. Centralize logs, quering logs, audit, etc. It cannot provide the <b>status</b> of the customer resources. Adjustable retention. </li>
  <li><a href="https://aws.amazon.com/eventbridge/"><b>EventBridge</b></a> (CloudWatch Events): serverless, build event-driven applications at scale, schedule (cron jobs), event pattern, trigger lambda functions,send SQS/SNS message, etc. Schema Registry, Archive events, replay archive events</li>
  <li><a href="https://aws.amazon.com/cloudtrail/"><b>CloudTrail</b></a>: track events (history events/API calls). Log, monitoring and retain account activity (Who, What, When)(track user activities and API requests and filter logs to assist with operational analysis and troubleshooting). Governance, compliance, audit for AWS account. It can be applied to all regions or one. It has encryptation enabled as default. Enabling the <b>insights</b> allows CloudTrail detect automatically unusual API activities in the customer account. </li>
  <li><b><a href="https://aws.amazon.com/xray/">AWS X-Ray</a></b>: Debugging in Production. Benefits: performance, uderstand dependencies, review request, find errors, identify users, trace request across microservice/AWS Service.</li>
  <li><b>CodeGuru</b>: automated code review and application performance recommendations</li>
  <li><b><a href="https://status.aws.amazon.com/">AWS Helth Dashboard</a></b>: service history (Service health Dashboard) for all regions or by your account (Account Helth Dashboard). It shows general status.</li>
  <li><b><a href="https://aws.amazon.com/premiumsupport/technology/personal-health-dashboard/">AWS Personal Health Dashboard</a></b>: personalized view of the status of the AWS services that are part of customer Cloud architecture. Alerts are triggered by changes in the health of your AWS resources, giving event visibility, and guidance to help quickly diagnose and resolve issues and. Customer can quickly assess the impact on your business when AWS service(s) are experiencing issues. It gives a personalized view of performance and availability of the services used by customer.</li>
</ul>  

<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/aws-global-infrastructure/">DigitalCloud Summary</a></li>
<li><a href="https://digitalcloud.training/aws-application-integration/">DigitalCloud - AWS Application Integration Services</a></li>
<li><a href="https://infrastructure.aws/">Regions and Availability Zones</a></li>

<br />
<hr>
<br />

<h2 id="network">AWS networking services</h2>

<p style="text-align: justify;"><a href="https://aws.amazon.com/vpc"><b>VPC</b></a> (Virtual Private Cloud): your own isolated network in AWS cloud</p>
<ul>
  <li><a href="https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html">VPC Peering</a> - connect two VPC. Private addresses.</li> 
  <li>VPC Endpoint - connect to AWS services using private Network (Gateway [S3 and DynamoDB]; Interface [the rest]). Use AWS PrivateLink (provides private connectivity between VPCs, AWS services, and your on-premises networks, without exposing your traffic to the public internet).</li>
  <li><a href="https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html">VPC Flow Logs</a>: capture information about the IP traffic going to and from network interfaces in your VPC</li>
  <li>When the VPC is created is defined the range of IP</li>
  <p style="text-align: justify;"><b>Elastic IP</b>: static IP to a public IP to EC2 instance</p>
  <li><b>High avalilability with VPC</b>:two subnets configured in one AZ</li>
  <li><b>Subnet</b>: partition the network inside the VPC and AZ. The public is accessible from the internet. <b>Route Tables</b> make possible the access of the internet and between subnets.</li>
  <li><a href="https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html"><b>Security Group</b></a>: instance level, virtual firewall to ENI/EC2 instance (ALLOW rule -IP and other security groups). Stateful. Protect against low level network attack like UDP floods.</li>
  <li><b>Network ACL</b> (Access Control List): subnet level, firewall to subnets (ALLOW and DENY rules - only IP). Stateless. Customer is responsible for configure it.</li>
  <li><b>Internet Gateways</b>: helps VPC to connect to internet. The public subnet has a route to the internet gateway, but private subnet does NOT have a route to Internet Gateway.</li>
  <li><b>NAT Gateway</b> (AWS-managed) and <b>NAT instance</b> (self-managed): allows the instance inside the private Subnets to access the internet. But denying inbound traffic from internet</li>
</ul>
  
<p style="text-align: justify;"><a href="https://aws.amazon.com/vpn/">Virtual Private Network</a> (<b>VPN</b>): </p>
<ul>
  <li>Establish secure connections between your on-premises networks, remote offices, client devices, and the AWS global network</li>
  <li><b><a href="https://docs.aws.amazon.com/vpn/latest/s2svpn/how_it_works.html">Site to Site VPN</a></b>: connect (encrypted) on premises VPN to AWS. Over the public internet</li>
  <li><b>AWS Managed VPN</b>: Tunnels from VPC to on premises</li>
  <li><b>VPN Gateway</b>: connect one VPC to customer network</li>
  <li><b>Customer Gateway</b>: installed in customer network</li>
  <li><b>Client VPN</b>: connect to your computer using OpenVPN. Connect to EC2 instance over a private IP.</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/directconnect/"><b>Direct Connect (DX)</b></a>: physical connection (private) between on premises and AWS. No public internet. The company should use <a href="https://aws.amazon.com/transit-gateway/">AWS Transit Gateway</a> (connect VPC and on-primise network through a central hub - acts like a cloud router)</p>

<p style="text-align: justify;"><b>Route 53</b>: Global Managed DNS. Helth check. Reliability and cost-effective way to route end users. <a href="https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html">Weighted routing policy</a> is used to route traffic to multiple resources (associated with a single domain/subdomain) and to choose how much traffic is routed to each resource. It can be used, e.g, for load balancing purpose. It is a hybrid architecture.</p>

<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/aws-networking-services/">DigitalCloud Summary</li>
<li><a href="https://digitalcloud.training/aws-content-delivery-and-dns-services/">(DigitalCloud) AWS Content Delivery and DNS Services</a></li>


<br />
<hr>
<br />

<h2 id="compute">AWS compute services</h2>

<p style="text-align: justify;"><a href="https://aws.amazon.com/ec2/"><b>Amazon EC2</b></a> (Elastic Compute Cloud): </p>
<ul>
  <li><b>IaaS</b> (Infrastructure as a service)</li>
  <li>It can run virtual server instances in the cloud</li>
  <li>Each instance can run Windows/Linux/MacOS</li>
  <li>It can storing data (EBS/EFS), distributing load (ELB), scaling services (ASG)</li>
  <li>It's possible to run commands when the machine starts (EC2 User data scripts): install updates, softwares, etc. Those scripts run with root user.</li>
  <li>Instance metadata is information about the instance. User data and metadata are not encrypted. The metadata is available at http://169.254.169.254/latest/meta-data</li>
  <li>When the instance is stopped and started again the public IP will change. The private IP not change.</li>
  <li>If you have a legacy, the EC2 instance is a good solution to migrate to cloud that is right-sized (right amount of resources for the application)</li>
  <li><b>Shared Responsability</b>
    <ul>
      <li>AWS: Infrastructure (global network security), Isolation on physical hosts, Replacing hoardware, Compliance Validation</li>
      <li>Customer: Security Groups rules, OS patches and updates, Software and utilities installed on the EC2 instance, IAM Roles assigned to EC2 and IAM user access management, Data security on your instance.</li>
    </ul>
  </li>
</ul>

<p style="text-align: justify;">Amazon EC2 <a href="https://aws.amazon.com/ec2/spot/">Spot Instances</a></p>
<ul>
  <li><em>Let you take advantage of unused EC2 capacity in the AWS cloud. Spot Instances are available at up to a 90% discount compared to On-Demand prices. You can use Spot Instances for various stateless, fault-tolerant, or flexible applications such as big data, containerized workloads, CI/CD, web servers, high-performance computing (HPC), and test & development workloads.</em></li>
  <li>Useful for workloads resilient to failure (batch, data analysis, Image processing, distributed workload). However, it is not suitable for critical jobs or databases.</li>
  <li>Useful when workload is not immediate and can be stopped for a moment and continue from that point after</li>
</ul>

<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html">Amazon <b>AMI</b></a> (Amazon Machine Image)</p>
<ul>
  <li>Launch EC2 one or more pre-configured instance </li>
  <li>It can be customized </li>
  <li>it is build for a specific region. The AMI must be in the same region as that of the EC2 instance to be launched; but can be copied to another one where want to create another instance.</li>
  <li>An EBS snapshot is created when an AMI is builded</li>
</ul> 

<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/imagebuilder/latest/userguide/what-is-image-builder.html"><b>EC2 Image Builder</b></a></p>
<ul>
  <li>It creates Virtual Machine or container images</li>
  <li>Automate the creation, maintain, validate and test EC2 AMIs</li>
  <li>The execution can be scheduled and after the process the AMI can be distributed (multiple regions)</li>
</ul> 

<p style="text-align: justify;">Amazon <b>Lambda</b></p>
<ul>
  <li>FaaS</li>
  <li>Virtual functions</li>
  <li>Serverless</li>
  <li>Run on-demand</li>
  <li>Scaling automatically</li>
  <li>Event-driven</li>
  <li>Can be monitoring through <b>CloudWatch</b></li>
  <li>Integrated with Load balancer (<b>ELB</b>)</li>
  <li>Pricing: Pay per call (request) and duration (time of execution)</li>
</ul>

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

<p style="text-align: justify;"><b>EBL</b> - <a href="https://aws.amazon.com/elasticloadbalancing/">Elastic Load Balancer</a></p>
<ul>
  <li>Servers that handle the traffic and distribute it across, e.g., EC2 instance, containers and IP address. Single AZ or Multiple AZ. </li>
  <li>It has only one point of access (DNS). </li>
  <li>Single Region</li>
  <li>Benefits: High availability across zones, automatic scaling and Fault Tolerance.</li>
  <li>Types:
    <ul> 
      <li><b>ALB</b> (Application Load Babancer): HTTP/S; Static DNS (URL); Layer 7; It is a single point of contact for client. Distributes incoming application traffic across multiple targets in multiple AZ.</li>
      <li><b>NLB</b> (Network Load Balancer): high performance/low latency (TCP/UDP); static IP throught Elastic IP; layer 4. It distributes traffic.</li> 
      <li><b>GLB</b> (Gateway Load Balancer): route traffic to firewalls managing in EC2 instance (Layer 3); Classic Load Balancer (Layer 4 and 7)</li>
    </ul>
  </li>
  <li><b>Shared responsibility</b>: AWS is responsable to keep it working, upgrade, maintain, and provide only few configurations.</li>
</ul>

<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/aws-compute-services/">DigitalCloud Summary</a></li>
<li><a href="https://aws.amazon.com/ec2/instance-types/">Instance Types</a></li>
<li><a href="https://docs.aws.amazon.com/autoscaling/ec2/userguide/schedule_time.html">Scheduled scaling for Amazon EC2 Auto Scaling</a></li>
<li><a href="https://aws.amazon.com/aws-cost-management/aws-cost-optimization/right-sizing/">Right Sizing</a></li>
<li><a href="https://instances.vantage.sh/">Instance Types - Vantage</a></li>

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

<p style="text-align: justify;"><a href="https://aws.amazon.com/s3/"><b>S3</b></a> - Amazon Simple Storage Service</p>
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
  <li><b>Features</b>: Transfer acceleration (CloudFront), Requester payes, Events (SNS, SQS, Lambda), Static website hosting, Encryptation, Replication (Cross-Region Replication - CRR; Same-Region Replication - SRR)</li>
  <li><b>Write-once-read-many</b> (WORM) - prevention of deletion or overwritten</li>
  <li>Use cases: backup, disaster recovery, archive, application hosting, media hosting, Software delivery, static website</li>
  <li><b>Security</b>: User-Based (IAM Policies), Resource-Based (<a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-iam-policies.html">Bucket Polices)</a>, Object/Bucket Access Control List (ACL), Encryptation</li>
  <li><b>Shared Responsibility</b>
    <ul>
      <li>AWS: Infrastructure (global security, durability, availability), Configuration and vulnerability analysis, Compliance validation, AWS employees can't not access the customer data, separation between customers</li>
      <li>Customer: version, bucket policies, replication, logging and monitoring, storage class, data encryptation, IAM user and roles</li>
    </ul>
  </li>
  <li><b>Pricing</b>: Depends the storage class; storage quantity; number of request; transition request; data transfer.</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/ebs/"><b>EBS</b></a> - Amazon Elastic Block Store (Amazon <b>EBS)</b></p>
<ul>
  <li>EBS <b>Volume</b>: attached to one instance.</li> 
  <li>The EBS volumes not need to be attached to an instance.</li> 
  <li>The EBS volumes cannot be accessed simultaneously by multiple EC2 instance (only with constrains)</li> 
  <li><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volumes-multi.html">Attach a volume to multiple instances with Amazon EBS Multi-Attach</a>: Same AZ, only to SSD volume, allowed only in some regions, and others restrictions</li> 
  <li>It allows the instance to persist data even after termination, however, Root EBS volumes are deleted on termination by default</li>
  <li>It can be mounted to one instance at a time and can be attached and detached from EC2 instance to another quickly. However it is locked to an AZ. To move to another AZ is necessary to create a <b>snapshot</b> and it can be copy across AZ or Region. </li>
  <li>A <b>snapshot</b> is a backup of the EBS Volume at a point in time. The snapshots are stored on Amazon S3 and they are incremental. EBS Snapshot features are <b>EBS Snapshot Archive</b> and <b>Recycle Bin for EBS Snapshot</b>. The process with snapshots (creating, deletion, updates) can be automated with <b>DLM</b> (Data Lifecycle Manager).</li> 
  <li>It has a limited performance.</li> 
  <li><b>Pricing</b>: Volumes type (performance); storage volume in GB per month provisioned; Snapshots (data storage per month); Data Transfer (OUT)</li>
</ul>

<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html"><b>EC2 Instance Store</b></a> is an alternative to EBS with a high-performance hardware disk, better I/O performance. However, it lose their storage when they stop. So, the best scenarios to be used are, e.g, buffer, cache, temporary content.</p>

<p style="text-align: justify;"><b><a href="https://aws.amazon.com/efs/">EFS</a></b> - Amazon Elastic File System</p>
<ul>
  <li>Shared File storage service for use with EC2.</li>
  <li>Managed NFS and works with Linux instance in multi-AZ. It is considered highly available, scalable, expensive, pay per use.</li>
  <li>Different AZ can share the same EFS.</li>
  <li>EFS Infrequent Access (EFS-IA) is a storage class that is cost-optimized for files not accessed and has lower cost than EFS standard. It is based on the last access. You can use a policy to move a file from EFS Stanrd to EFS-IA.</li>
</ul>

<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/storagegateway/latest/userguide/WhatIsStorageGateway.html"><b>Storage Gateway</b></a></p>
<ul>
  <li>It is a hybrid cloud storage service: a bridge between on-premise data and cloud data in S3.</li>
  <li>Simplify storage management and reduce costs for key hybrid cloud storage use cases</li>
  <li>Virtually unlimited cloud storage</li>
  <li>Cannot be used to data archival</li>
  <li>Types: File Gateway, Volume Gateway and Tape Gateway</li>
  <li>Ex: moving backups to the cloud, low latency access, disaster recovery</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/fsx/windows/">Amazon FSx</a> for Windows File Server provides fully managed Microsoft Windows file servers, backed by a fully native Windows file system. Amazon FSx supports a broad set of enterprise Windows workloads with fully managed file storage built on Microsoft Windows Server. Amazon FSx has native support for Windows file system features and for the industry-standard Server Message Block (SMB) protocol to access file storage over a network</p>

<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/aws-storage-services/">DigitalCloud Summary</a></li>
<li><a href="https://docs.aws.amazon.com/opsworks/latest/userguide/best-practices-storage.html">Best Practices: Root Device Storage for Instances</a></li>
<li><a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-iam-policies.html">Bucket policies and user policies</a></li>

<br />
<hr>
<br />

<h2 id="database">AWS database services</h2>

<p style="text-align: justify;">It's possible to install database in EC2 instance. It can be necessary when is needed full control over instance and database; and using a third-party database engine</p>

<p style="text-align: justify;"><a href="https://aws.amazon.com/rds/"><b>RDS</b></a> - Amazon Relational Database Service</p>
<ul>
  <li>Use EC2 instance</li>
  <li>Benefits to deploy database on RDS instead EC2: hardware provision, database setup, Automated backup and software patching. It reduce the database administration tasks. There is no need to manage OS</li>
  <li>Aurora, MySQL and PostgreSQL compatible</li>
  <li>It's possible encrypt the RDS instances using AWS Key Management Service (KMS) and snapshot</li>
  <li>Sales up by increaing instance size (compute and storage)</li>
  <li>Replics is only to ready. It improves database scalability.</li>
  <li>It can use Auto scaling to add replicas</li>
  <li>Serveless</li>
  <li>You can't use SSH to access instances.</li>
  <li>It is suited for OLTP workloads</li>
  <li>Shared Responsibility
    <ul>
      <li>AWS: Manage the underlyning EC2 instance, disable ssh access; Automated DB and OS patching, guarantee the hardware</li>
      <li>Consutmer: Check ports, IP, Security groups inbound rules; users and permissions for database; create database (public/private access); config DB to only allow SSL connection; database encryptation setting; createing schema (table, indexes,etc), Schema Optimization.</li>
    </ul>
  </li>
  <li>Pricing: Depends the Clock hours of server uptime; Database characteristics (size, mem); Database purchase type (on demand, reserved instance); Number of database instances; Provisioned storage; Additional storage; Requests; Deployment type; Data transfer (OUT); Reserved Instances.</li>
</ul>

<p style="text-align: justify;"><b><a href="https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-multi-master.html">Aurora</a></b></p>
<ul>
  <li>Relational DB from AWS fully managed.</li>
  <li>Faster, auto-scales (up 128 TB), automatic backup enabled</li>
  <li>Compatible with <a href="https://aws.amazon.com/rds/aurora/mysql-features/">MySQL</a>, PostgreSQL, Oracle, Microsoft SQL Server</li>
  <li>You can also deploy replics for read scaling within and across Regions</li>
</ul>

<p style="text-align: justify;">Amazon <a href="https://aws.amazon.com/elasticache"><b>ElastiCache</b></a></p>
<ul>
  <li>Manage Mem cached</li>
  <li>Service that adds caching layers on top of your databases</li>
  <li>In-Memory databases with high performance and low latency (under a millisecond)</li>
  <li>Shared Responsibility: AWS takes care of OS maintenance / patching, optimizations, setup, configuration, monitoring, failure recovery and backups</li>
</ul>

<p style="text-align: justify;">Amazon <b><a href="https://aws.amazon.com/dynamodb/features/">DynamoDB</a></b></p>
<ul>
  <li>Highly available with replication across 3 AZ.</li>
  <li>Multi-Region replication. Ative-Active with cross region support. The global tables replicate data automatically across the customer choise of regions</li>
  <li><a href="https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/SQLtoNoSQL.WhyDynamoDB.html">NoSQL</a> database</li>
  <li>Distributed serverless database</li>
  <li>Hight performance</li>
  <li>Low latency retrieval</li>
  <li>Integrated with IAM for security, authorization and administration</li>
  <li>Low cost and auto scaling</li>
  <li>Horizontal Scaling</li>
  <li>Standard and IA (Infrequent Access) Table class</li>
  <li><a href="https://aws.amazon.com/dynamodb/dax/">DynamoDB <b>Accelarator</b> (DAX)</a> is fully managed in memory cache, the performance is improved, highly scalable and available. Only used with DynamoDB</li>
  <li>Considering a <a href="https://aws.amazon.com/blogs/aws/new-amazon-dynamodb-continuous-backups-and-point-in-time-recovery-pitr/"><b>point-in-time recovery</b></a> (PITR)(continuous backup) for DynamoDB, the customer is responsible to configure (turn on) and AWS is responsible for the backup. Amazon RDS database instance can be restored to a specific point in time with a granularity of 5 minutes</li>
  <li>Pricing: throughput; Indexed data storage; Data tranfer; Global tables; reserved capacity; On-demand capacity mode; Provisioned capacity mode</li>
</ul>

<p style="text-align: justify;">Amazon <a href="https://aws.amazon.com/redshift"><b>Redshift</b></a></p>
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

<p style="text-align: justify;"><a href="https://aws.amazon.com/glue/">Amazon <b>Glue</b></a></p>
<ul>
  <li>extract, transform, and load (ETL) service</li>
  <li>serverless service</li>
  <li>prepare and load their data for analytics</li>
  <li>The AWS Glue Data Catalog is a central repository to store structural and operational metadata for all your data assets. </li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/emr/">Amazon <b>EMR</b></a> (Elastic MapReduce)</p>
<ul>
  <li>Helps to create Hadoop clusters (Big Data)</li>
  <li>Take care of all the provisioning and configuration</li>
  <li>Auto Scaling</li>
  <li>Ex: machine learn and big data</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/documentdb"><b>DocumentDB</b></a>: Implementation of MongoDB, Ex: User profile.</p>

<p style="text-align: justify;"><a href="https://aws.amazon.com/qldb"><b>QLDB</b></a>(Quantum Ledger Database): Fully managed graph database; no decentralization component; immutable ledger database. Ex: review a complete history of all the changes</p>

<p style="text-align: justify;"><a href="Amazon Managed Blockchain"><b>Managed Blockchain</b></a>: create and manage blockchain networks with open-source frameworks</p>

<p style="text-align: justify;">Analyses</p>
<ul> <a href="https://aws.amazon.com/neptune"><b>Neptune</b></a>: Fully managed graph database. Good to app with highly connected datasets, as fraud detection and knowledge grapns</li>
  <li><a href="https://aws.amazon.com/quicksight/"><b>QuickSight</b></a>:  scalable, serverless, embeddable, machine learning-powered business intelligence (BI) service</li>
  <li><a href="https://aws.amazon.com/athena/features/"><b>Athena</b></a>: Analyze data in S3 using SQL; it is serverless (no infrastructure to manage); Pricing: you pay only for the queries that you run. Ex: BI, analytics, reporting</li>
</ul>

<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/aws-database-services/">DigitalCloud Summary</a></li>
<li><a href="https://aws.amazon.com/emr/features/">Amazon EMR features</a></li>
<li><a href="https://aws.amazon.com/products/databases/">AwS Database</a></li>

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

<p style="text-align: justify;"><a href="https://aws.amazon.com/cloudformation/">Amazon <b>CloudFormation</b></a></p>
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

<p style="text-align: justify;">AWS Elastic <a href="https://aws.amazon.com/elasticbeanstalk/"><b>Beantalk</b></a></p>
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

<p style="text-align: justify;">AWS <b><a href="https://aws.amazon.com/systems-manager/faq/">Systems Manager</a></b> (SSM) Session Manager</p>
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

<p style="text-align: justify;">AWS <b>OpsWorks</b></p>
<ul>
  <li>Like Chef and Puppet - perform server configuration automatically.</li>
  <li>Alternative to SSM</li>
</ul>


<p style="text-align: justify;">Amazon <b>API Gateway</b>: Fully managed service for developers, Serverless and scalable, Restful and WeSocket</p>
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
<p style="text-align: justify;">AWS <b>Step Functions</b>: workflow to lambda function.</p>
<p style="text-align: justify;">AWS <b>Ground Station</b>: control satellite communication</p>
<p style="text-align: justify;">AWS <b><a href="https://aws.amazon.com/pinpoint/">Pinpoint</a></b>: marketing communication service (email, sms, voice)</p>
<p style="text-align: justify;">Amazon Elastic Container Service for Kubernetes (<a href="https://aws.amazon.com/eks/">EKS</a>)</p>

<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/additional-aws-services/">DigitalCloud Summary</a></li>
<li><a href="https://aws.amazon.com/developer/tools/">Tools to Build on AWS</a></li>  
<li><a href="https://aws.amazon.com/datapipeline/">AWS Data Pipeline</a></li>
<li><a href="https://aws.amazon.com/elasticsearch-service/features/">Amazon OpenSearch Service Features</a></li>

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

<p style="text-align: justify;"><a href="https://aws.amazon.com/application-migration-service/">AWS Application Migration Service</a> <b>(MGN)</b>: Migrating to native AWS</p>

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

<br />
<hr>
<br />

<h2 id="security">Security</h2>

<p style="text-align: justify;"><b>Users</b> are accounts without permissions by default. They are create with NO access to any AWS services, only login to the AWS console. They log in using <em>user name</em> and <em>password</em>. They can change some configurations or delete resources in your AWS account.</p>

<p style="text-align: justify;"><b>Groups</b> are a way to organize the users (only) and apply <b>policies</b> (permissions) to a collection of users in the same time. A user can belong to multiple groups. Only users and cannot be nested.</p>

<p style="text-align: justify;"><b>Roles</b> delegate permissions. Roles are assumed by users, applications, and services. It provides temporary security credentials for customer role session</p>

<p style="text-align: justify;">The <b>policies</b> can be applied to users, groups and roles. It is a document written in JSON. <a href="https://docs.aws.amazon.com/en_us/IAM/latest/UserGuide/access_policies.html">Policy main elements</a>:
<ul>
  <li>Version</li>
  <li>Effect: allow/deny</li>
  <li>Action: type of action that should be allowed or denied</li>
  <li>Resource: specifies the object or objects that the policy statement covers</li>
  <li>Condition: circumstances under which the policy grants permission</li>
  <li>Principal: account, user, role, or federated user</li>
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/organizations/">AWS Organization</a> is a feature to control many accounts</p>
<ul>
  <li><b>Service Control Policies (SCPs)</b> is in AWS Organization and can control a lot of available permissions in AWS account, but NOT grant permissions.</li>    
  <li>To remove an account from the AWS Organization that should be as standalone</li>
</ul>

<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys"><b>Access keys</b></a> are used to programmatic access (API/SDK). It is generated through thr AWS Console</p>

<p style="text-align: justify;"><b>SSH key</b> is an IAM feature to allow developer to access AWS services through the AWS CLI.</p>

<p style="text-align: justify;"><a href="https://aws.amazon.com/iam/">Identify AWS access management (IAM)</a> capabilities</p>
<ul>
  <li><b>IAM</b> is a <b>Global</b> service used to control the access to AWS resources (authentication/authorization). </li>
  <li><a href="https://docs.aws.amazon.com/general/latest/gr/root-vs-iam.html"><b>Root</b></a> has <b>full permissions</b> and complete access to all AWS services and resource.  <a href="https://docs.aws.amazon.com/accounts/latest/reference/root-user-tasks.html">Actions allowed only to root</a>: change account setting, close account, restore IAM permission, change or cancel AWS support paln, register as a seller, config S3 bucket to enable <a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html">MFA</a>, edit/delete S3 bucket policies.</li>
  <li>IAM Security Tool: 
    <ul>
      <li>IAM Credential Report (account-level): account's users and their credential status. Access it by IAM menu Credential Report</li> 
      <li><a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_access-advisor.html">IAM Access Advisor</a> (user-level): services permissions and last access. Access it by IAM User menu. Using it is possible to identify unnecessary permissions that have been assigned to users.</li>
    </ul>
  </li>
</ul>

<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html">Best Practices</a></p>
  <ul>
    <li>Use IAM user instead of root user in regular activities</li>
    <li>Add user into groups</li>
    <li>Strong password</li>
    <li>Use MFA</li>
    <li>Create roles for permissions to AWS services</li>
    <li>User Access Keys for programmatic access (CLI/SDK)</li>
    <li>Audit permissions through IAM Credential Reports and IAM Access Advisor</li>
    <li>Protectect you access key</li>
    <li>Prefer customer managed policies (managed policies cannot be edited)</li>
    <li>Use roles for applications that run EC2 and to delegate permissions</li>
    <li>Rotate credentials</li>
    <li>Give only credentials that is really needed (Least privilege)</li>
  </ul>

<p style="text-align: justify;"><b>Security Groups</b></p>
<ul>
  <li>It operates at instance level (can be attached to multiple instances) and are applied to the network security, controlling the traffic into or out of the EC2 instance, acting like a firewall (by default, inbound traffic is blocked and outbound traffic is authorised).</li>
  <li>It contains only <b>rules</b> and these rules can reference by IP or by security group. They are stateful and locked down to a region/VPC combination.</li> 
  <li>They regulate access to Ports and authorised IP ranges.</li>
  <li>A good practices is to create a separate security group for SSH access.</li>
  <li>Tips: errors with time out is a security group issue; error of connection refused can be an application error.</li>
</ul>  

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
  <li>AWS <a href="https://docs.aws.amazon.com/waf/latest/developerguide/how-aws-waf-works.html">WAF</a> (Web Application Firewall): filter specific requests based on rules, protection on layer 7 (HTTP), ALB, API Gateway, CloudFront, Define Web ACL (Web Access Control List - protect SQL Injection and Cross-Site Scripting(XSS), rate-based rules). Protecting a website that is hosted outside of AWS (the on-premise IP is added to a target group).</li>
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
  <li>AWS <b>KMS</b> - Key Management Service
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
  <li><b><a href="https://aws.amazon.com/cloudhsm/">CloudHSM</a></b>: Hardware Security Module. Encryptation for Hardware; The customer manages the encryptation keys; use HSM device (level 3 compliance)</li>
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

<p style="text-align: justify;">AWS <b>Directory Service</b>: AWS Managed Microsoft Active Directory (Database of objects (user, accounts, computers, etc). Centralized security management)</p>

<p style="text-align: justify;">AWS <b>IAM Identify Center</b>: One loging like <a href="https://aws.amazon.com/single-sign-on/">SSO</a>.</p>

<p style="text-align: justify;"><a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html"><b>AWS IAM Access Analyzer</b></a>: identify the resources in your organization and accounts, such as Amazon S3 buckets or IAM roles, shared with an external entity. This lets you identify unintended access to your resources and data, which is a security risk.</p>


<p><b>Aditional References:</b></p>
<li><a href="https://digitalcloud.training/aws-security-services/">(DigitalCloud) Summary</a></li>
<li><a href="https://digitalcloud.training/aws-cloud-management-services/">(DigitalCloud) AWS Cloud Management Services</a></li>
<li><a href="https://aws.amazon.com/security/">AWS Cloud Security</a></li>
<li><a href="https://aws.amazon.com/waf/features/">AWS WAF features</a></li>

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

<p style="text-align: justify;"><b>EC2 Pricing:</b> the price for it depends the instance (number, type), load balance, IP adreess, etc.</p>
<ul>
  <li><b>On-Demand:</b> short workload, predictable pricing, billing per second/hour, pay for what you use, no long-term commitment, highest cost, no discount. Best use to <b>short-term and un-interrupted worloads</b>.</li>
  <li><b>Reservations (1-3 years):</b> predicted workload. various services like Ec2, DynamoDB, ElastiCache, RDS and RedShift. <a href="https://aws.amazon.com/ec2/pricing/reserved-instances/">Discount up 72%</a>.
    <ul>
      <li><b>Reserved instances (RI)</b>: long workloads; has a big discount and has as scope Regional or Zonal. Indicated for steady-state usage application. It cannot be interrupted.</li> 
      <li><a href="https://docs.aws.amazon.com/whitepapers/latest/cost-optimization-reservation-models/standard-vs.-convertible-offering-classes.html"><b>Convertible Reserved Instances</b></a> long workload with flexible instances; gives a big discount. This model change the attributes of the RI as long as the exchange results in the creation of RIs of equal or greater value</li>
    </ul>
  </li>
  <li><b>EC2 <a href="https://aws.amazon.com/savingsplans/pricing/">Savings Plain</a></b>: reduce compute cost based on long term (1-3y). Locked to a specific instance family and region. Lot of flexibility (EC2, Fargate, Lambda). No Upfront or Partial Upfront or All Upfront Payments</li> 
  <li><b>Spot Instance:</b> High discount (up to 90%). It is the most cost-efficient instanves in AWS.</li> 
  <li><a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-hosts-overview.html"><b>Dedicated host</b></a> (single customer, your VPC): physical server with EC2 instance dedicated, can use your own licenses. It can be purchasing <b>On-Demand</b> or <b>Reserved</b>. It is the most expensive.</li> 
  <li><b>Dedicated Instance</b>: single customer, isolated hardware dedicated to your application, but this hardware can be shared with other instances in the same account.</b></li>
  <li><a href="https://aws.amazon.com/blogs/aws/new-per-second-billing-for-ec2-instances-and-ebs-volumes/">Minimum charge</a>: one-minute for Linux based EC2 instances.</li>    
</ul>

<p style="text-align: justify;"><a href="https://aws.amazon.com/organizations/">AWS <b>Organization</b></a></p>
<ul>
  <li>provides volume discounts or EC2 and S3 aggregated across the member AWS account.</li>
  <li><a href="https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/consolidated-billing.html">Consolidate billing</a>: bill for multiple accounts and volume discounts as usage in all accounts is combined, easy to tracking or charges across accounts, combined usege across accounts and sharing of volume pricing discounts, reserved instance discounts and saving plans.</li>
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
  <li>AWS <b>Control Tower</b>: set up and govern a secure and compliant multi-account AWS environment. Monitor compliance through a dashboard. It run on top of <b>AWS Organization</b></li>
  <li>AWS <a href=" https://aws.amazon.com/compute-optimizer/"><b>Compute Optimizer</b></a>: Reduce costs and improve performance. Use ML. Helps the customer to choose optimal configuration and right size workload, including the CPU utilization and memory utilization. It delivers recommentations to EC2 instance, EC2 Scaling groups, EBS volumes and AWS lambda functions.</li>
</ul>  

<p style="text-align: justify;">AWS <b>Service Catalog</b>: stacks of authorized products</p>

<p><b>Aditional References</b></p>
<li><a href="https://digitalcloud.training/aws-billing-and-pricing/">DigitalCloud Summary</a></li>
<li><a href="https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html">Using AWS cost allocation tags</a></li>
<li><a href="https://aws.amazon.com/aws-cost-management/">Cloud Financial Management with AWS</a></li>

<br />
<hr>
<br />

<h2 id="architect">AWS Architecture and Ecosystem</h2>

<p style="text-align: justify;"><a href="https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf">AWS Well-Architectured Framework</a> helps to build secure, high-performing, resilient, and efficient infrastructure</p>

<p style="text-align: justify;">AWS Best Practices - Design Principles</p>
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

<p style="text-align: justify;"><b><a href="https://aws.amazon.com/blogs/apn/the-6-pillars-of-the-aws-well-architected-framework/">Pillars</a></b>:</p> 
<ul>
  <li><a href="https://wa.aws.amazon.com/wat.pillar.operationalExcellence.en.html">Operational Excellence</a>: run and monitor system 
    <ul>
      <li>Design Principles: IaaC annotate doc; frequent, small, reversible changes; refine operations; anticipate failure; learn with failures</li>
      <li>Best Practices: creates, use procedures and validate; collect metrics; continuous change</li>
    </ul> 
  </li>
  <li>Security: protect information, systems and assets
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
  <li>Performance Efficiency: use compute resources efficiently 
    <ul>
      <li>Design Principles: democratize advanced technology; go global in minutes; experiment more often; Mechanical sympathy</li>
      <li>Best practices: Data-driven approach; review the choices;make trade-offs;</li>
    </ul> 
  </li>
  <li>Cost Optimization: run system to delivery value at the loest price 
    <ul>
      <li>Design Principles: adopt a consumption mode, measure overall efficinecy; stop spending money on data center operations; analyze and attribute expenditure; use managed and application level services to reduce cost</li>
      <li>Best Practices: using the appropriate services, resources, and configurations for the specific workloads</li>
    </ul> 
  </li>
  <li>Sustainability (shared responsibility): minimizing the environmental impacts of running cloud workloads
    <ul>
      <li>Design Principles: understand impacts; establish sustainability goals; maximize utilization; anticipate and adopt new solutions; use managed services; reduce downstream impact</li>
    </ul>
  </li>
</ul>

<p><b>Aditional References</b></p>
<li><a href="https://digitalcloud.training/architecting-for-the-cloud/">DigitalCloud Summary</a></li>
<li><a href="https://aws.amazon.com/architecture/well-architected/">AWS Well-Architected</a></li>
<li><a href="https://aws.amazon.com/blogs/apn/the-5-pillars-of-the-aws-well-architected-framework/">The 6 Pillars of the AWS Well-Architected Framework</a></li>

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

<br />
<hr>
<br />

<h2 id="shots">Some Shots</h2>

<p style="text-align: justify;"><b>Computing Service</b>: Batch, EC2, EC2 Image Builder, Elastic Beanstalk, Lambda, Lightsail, AWS Outspots, Serverless Application Repository, AWS SimSpace Weaver, AWS App Runner</p>

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

<p><b>Hybrid</b>: Storage Gateway, Outspots, SSM, Route 53, Virtual Private Gateway</p>

<p><b>Audit</b>: CloudWatch, CloudTrail, SSE-KMS, AWS Config</p>

<p><b>Encryptation</b>: AZ traffic (Default), CloudTrail (default), Site-To-Site VPN (default), all storage (RDS, S3, EBS, Redshift, EFS)</p>

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