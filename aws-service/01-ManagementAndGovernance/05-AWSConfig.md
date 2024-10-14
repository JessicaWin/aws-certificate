

# Overview
+ AWS Config provides a **detailed view of the configuration of AWS resources** in your AWS account.
+ This includes **how the resources are related to one another and how they were configured in the past** so that you can see how the configurations and relationships change over time.
+ With AWS Config, you can do the following: 
    + Evaluate your AWS resource configurations for desired settings.
    + Get a snapshot of the current configurations of the supported resources that are associated with your AWS account.
    + Retrieve configurations of one or more resources that exist in your account.
    + Retrieve historical configurations of one or more resources.
    + Receive a notification whenever a resource is created, modified, or deleted.
    + View relationships between resources. For example, you might want to find all resources that use a particular security group.
# AWS Config Concepts
+ A **configuration history** is a collection of the configuration items for a given resource over any time period. 
    + A configuration history can help you answer questions about, for example, when the resource was first created, how the resource has been configured over the last month, and what configuration changes were introduced yesterday at 9 AM. 
+ A **configuration item** represents a point-in-time view of the various attributes of a supported AWS resource that exists in your account. 
    + The components of a configuration item **include metadata, attributes, relationships, current configuration, and related events**.
    + AWS Config creates a configuration item whenever it **detects a change** to a resource type that it is recording. 
+ The **configuration recorder** stores the configurations of the supported resources in your account as configuration items. 
    + You must first **create and then start the configuration recorder** before you can start recording.
    + You can stop and restart the configuration recorder at any time.
    + By default, the configuration recorder records all supported resources in the Region where AWS Config is running. You can create a customized configuration recorder that records only the resource types that you specify
+ A **configuration snapshot** is a collection of the configuration items for the supported resources that exist in your account. This configuration snapshot is **a complete picture of the resources that are being recorded** and their configurations.
+ A **configuration stream is an automatically updated list of all configuration items** for the resources that AWS Config is recording. Every time a resource is created, modified, or deleted, AWS Config **creates a configuration item and adds to the configuration stream**.
+ Resource Relationship: AWS Config discovers AWS resources in your account and then creates a map of relationships between AWS resources.
+ An **AWS Config rule** represents your desired configuration settings for specific AWS resources or for an entire AWS account. 
    + If a resource violates a rule, AWS Config flags the resource and rule as noncompliant, and AWS Config notifies you through Amazon SNS.
+ **A conformance pack** is a collection of AWS Config rules and remediation actions that can be deployed as a single entity in an account and Region or across an organization in AWS Organizations.
+ **Multi-account multi-region data aggregation** in AWS Config allows you to aggregate AWS Config configuration and compliance data from multiple accounts and regions into a single account.
+ **Advanced queries**： You can use AWS Config to query the current configuration state of AWS resources based on configuration properties for a single account and Region or across multiple accounts and Regions. You can perform property-based queries against current AWS resource state metadata across all resources that AWS Config supports.  
# What does AWS Config do?
+ AWS Config **continually monitors and records your AWS resource configurations**, which can help you automate the evaluation of recorded configurations against desired configurations.
    + The CloudFormation StackSets templates help you create, update, or delete stacks across multiple accounts and AWS Regions with a single operation
+ With AWS Config, you can **examine detailed resource configuration histories** and determine your overall compliance against the configurations specified in your internal guidelines.
+ These capabilities can help with **compliance auditing, security analysis, resource change tracking, and troubleshooting**.
+ AWS Config provides the building blocks for many other security and compliance services on AWS. Through seamless integration, services like AWS Security Hub, AWS Firewall Manager, and AWS Control Tower **use AWS Config to evaluate and provide findings**. This, as well as the ability to **visualize compliance and resource data**, makes AWS Config your **central compliance hub**.
# What problems does AWS Config solve?
+ AWS Config can help you understand your resource configuration changes in the cloud.
# What are the benefits of AWS Config?
+ **Continual monitoring**: With AWS Config, you can continually monitor and record configuration changes of your AWS resources.
+ **Change management**: With AWS Config, you can track the relationships among resources and review resource dependencies before making changes.
+ **Operational troubleshooting**: You can use AWS Config to capture a comprehensive history of your AWS resource configuration changes to help troubleshoot operational issues.
+ **Continual assessment**: AWS Config provides a way for you to continually audit and assess the overall compliance of your AWS resource configurations with your organization’s policies and guidelines.
+ **Enterprise-wide compliance monitoring**: With multi-account, multi-Region data aggregation in AWS Config, you can view compliance status across your enterprise and identify noncompliant accounts.
+ **Support for third-party resources**: AWS Config is designed to be your primary tool to perform configuration audit and compliance verification of both your AWS and third-party resources. You can publish the configuration of third-party resources such as GitHub repositories, Microsoft Active Directory resources, or any on-premises server into AWS.
+ **Enhanced visibility and resource tracking**：With AWS Config, you gain a comprehensive view of your AWS resources and their configuration history. You can track changes, identify relationships between resources, and troubleshoot issues.
+ **Automated compliance and auditing**： AWS Config automates compliance checks by evaluating resource configurations against predefined rules, industry standards, or custom policies. You can quickly identify noncompliant resources and demonstrate compliance during audits.
+ **Proactive security management**： AWS Config helps you proactively manage security by detecting drifts from desired configurations, identifying potential risks, and providing notifications of configuration changes. With AWS Config, you can take timely corrective actions to maintain a secure environment.
+ **Automated remediation**：By integrating with AWS services like AWS Lambda, AWS Config creates automated remediation actions that engage when it detects specific rule violations. This ensures timely resolution of noncompliant resources and reduces the need for manual intervention.
+ **Cost optimization and resource usage**：AWS Config provides insights into resource usage. With those insights, you can optimize costs by identifying underused or unused resources. You can also use them to make informed decisions regarding resource allocation and scaling.
+ **Seamless integration with the AWS environment**：AWS Config integrates with various AWS services, such as AWS CloudTrail, AWS Security Hub, and AWS Organizations. With this integration, you can create a unified monitoring, security, and compliance management solution across your entire AWS infrastructure.
+ **Hybrid and multicloud support**：AWS Config can record configurations and monitor the resource inventory and configuration history of third-party resources with an API. Hybrid and multicloud environments benefit from AWS Config rules and conformance pack best practice evaluations.
# How much does AWS Config cost?
+ With AWS Config, you are charged based on the **number of configuration items recorded**, **the number of active AWS Config rule evaluations**, and **the number of conformance pack evaluations in your account**. 
# How is AWS Config used to architect a cloud solution
+ With AWS Config, you can automate your compliance and risk management, and manage and report on your compliance in an automated way using AWS services.
# What else should I keep in mind about AWS Config?
+ Activate AWS Config in all accounts and Regions
+ Use a secure Amazon S3 bucket to collect the configuration history and snapshot files
+ Control costs by routinely identifying frequently modified resources
+ Start with conformance pack sample templates
+ Integrate with other services
# Use Case 1
+ Issue: **AnyCompany faced a concerning situation where they discovered a sensitive, data-laden S3 bucket had been publicly exposed.**
+ After disabling public access to the S3 bucket, they used **AWS Config to gather the configuration history of the exposed S3 bucket**. This historical data provided **a detailed timeline of all configuration changes to the S3 bucket since its creation**. This timeline included any changes to permissions or policies that potentially led to its public exposure.
+ Using AWS Config, the security team also **analyzed the configuration item associated with the S3 bucket at the time of exposure**. This snapshot revealed **the exact state of the resource when it was exposed**, including its relationships with other AWS resources. It gave insights into potential attack vectors that could have been exploited because of the misconfiguration.
+ Simultaneously, AnyCompany **examined the CloudTrail logs to track API activity around the time of the incident**. CloudTrail provided an audit of actions taken by users and services, which offered crucial clues. By combining the AWS Config configuration history and CloudTrail events, the security team looked back in time and pinpointed the exact moment and event that led to the bucket becoming public. They discovered that an employee made an inadvertent change to the S3 bucket's public access policy, which caused the exposure.
+ AnyCompany identified the root cause and then used **AWS Config rules to actively scan their entire AWS environment for similar misconfigurations**. This proactive measure confirmed that they had not mistakenly configured any other S3 buckets for public access.
+ To prevent such an incident from recurring, AnyCompany **developed and deployed conformance packs**. These packs contained a set of AWS Config rules that embodied their security policies, including one that disallowed public read access on S3 buckets. With conformance packs, AnyCompany enforced these security policies across all their AWS accounts and Regions.
+ In the end, by using **AWS Config configuration history**, **configuration items**, **AWS Config rules**, and **conformance packs**, along with **CloudTrail**, AnyCompany managed to mitigate a potentially disastrous situation.
## Question
+ Which feature did AnyCompany use to identify the exact state and resource relationship of the publicly exposed Amazon Simple Storage Service (Amazon S3) bucket during the incident?
    + AWS CloudTrail logs
    + **AWS Config configuration items**
    + AWS Config configuration history
    + AWS Config rules
    + An AWS Config configuration item provided AnyCompany with a snapshot of the exact state of the exposed S3 bucket during the incident. This included its relationships with other AWS resources. This snapshot revealed the exact configuration attributes of the resource when it was exposed and helped the security team investigate the incident.
+ Which feature of AWS Config did AnyCompany use to trace back the timeline of changes made to the publicly exposed Amazon Simple Storage Service (Amazon S3) bucket?
    + AWS Config rules
    + AWS Config configuration items
    + AWS Config conformance packs
    + **AWS Config configuration history**
    + With AWS Config configuration history, AnyCompany had a comprehensive record of the configuration changes made to the S3 bucket over time. This feature facilitated tracing back the specific changes and conditions that led to the bucket becoming publicly exposed.
+ Which feature did AnyCompany use to ensure that no other Amazon Simple Storage Service (Amazon S3) buckets in their environment were similarly misconfigured after discovering the publicly exposed bucket?
    + AWS CloudTrail logs
    + AWS Config configuration items
    + **AWS Config rules**
    + AWS Config conformance packs
    + AnyCompany used AWS Config rules to continuously scan their entire AWS environment for compliance with their security policies. In this instance, the rules helped to check whether any other S3 buckets were mistakenly configured to public access.
# Integrating AWS Config with AWS Security Services
## Amazon GuardDuty
+ Amazon GuardDuty is a **managed threat detection service** that **continuously monitors your AWS environment for malicious activities and unauthorized behavior**.
+ It analyzes events from **multiple AWS data sources**, such as CloudTrail, Amazon Virtual Private Cloud (Amazon VPC) Flow Logs, and DNS logs, to identify potential security threats.
+ GuardDuty detects activities such as **unusual API calls, cryptocurrency mining, and unauthorized infrastructure deployments**.
### How does GuardDuty work with AWS Config?
+ **Configuration history**: AWS Config keeps a **detailed history of configuration changes** to your AWS resources. GuardDuty administrators use configuration history to correlate detected threats with specific configuration changes, aiding in investigations and incident response.
+ **Configuration snapshots**: AWS Config can generate **a point-in-time snapshot of all your resource configurations in an AWS Region**. GuardDuty administrators use snapshots to **understand the context of a detected threat, which aids in investigations**. 
+ **AWS Config rules**: With AWS Config, you **create rules that automatically check the compliance of your AWS resources against specific desired configurations**. You can use these rules to enforce security best practices and prevent misconfigurations that could lead to vulnerabilities detected by GuardDuty. 
## Amazon Inspector
+ Amazon Inspector is an **automated vulnerability management service** that helps **improve the security and compliance of workloads deployed on AWS**. It continually evaluates your AWS resources for **software vulnerabilities and unintended network exposure**. Amazon Inspector provides **a detailed report and risk score of the findings**.
### How does Amazon Inspector work with AWS Config?
+ Amazon Inspector does not require AWS Config to function, but it can use the information AWS Config provides to enhance its security assessment capabilities. AWS Config offers a comprehensive view of resource configurations, relationships, and changes over time, which can help Amazon Inspector to better identify potential security risks.
+ **Resource inventory and discovery**: AWS Config automatically **discovers and records the configuration details for your AWS resources**. It also maintains **an inventory of these resources over time**. Amazon Inspector administrators use this information to understand the resources in your environment and their relationships, which is crucial for performing comprehensive security assessments. 
+ **Configuration history**: AWS Config provides a historical view of the configurations for each AWS resource and tracks changes over time. This can be useful to Amazon Inspector administrators, who can use this history to identify changes that could potentially introduce security vulnerabilities. 
+ **AWS CONFIG RULES**: You can create custom rules that automatically check the configuration of your AWS resources with AWS Config. These rules can enforce best practices and identify potential security risks. They provide Amazon Inspector administrators with additional data points for assessing the security of your environment. 
## AWS Systems Manager Patch Manager
+ Patch Manager, a capability of AWS Systems Manager, is a service you can use to /88automate the process of patching managed instances, including EC2 instances and on-premises servers**.
+ With Patch Manager, you can keep your infrastructure **up to date with the latest patches for security vulnerabilities, bug fixes, and other updates**. 
+ You can create patch baselines, schedule patching windows, and track the compliance status of your instances.
+ Patch Manager integrates with AWS Config.
### How does Patch Manager work with AWS Config?
+ Patch Manager automates the process of patching managed instances. It provides a set of capabilities that help you scan instances for missing patches, set different patching criteria, and patch instances across multiple AWS accounts and Regions. **AWS Config can augment the capabilities of Patch Manager**.
+ **Configuration history**: AWS Config maintains a history of the configuration of your AWS resources. This feature can help Patch Manager identify changes in your instances that could affect patching operations. 
+ **Resource inventory and discovery**: AWS Config automatically discovers and records the configuration of your AWS resources. This gives Patch Manager an up-to-date view of your instances, helping it identify which instances require patching and which do not, based on their current configuration. 
+ **AWS CONFIG RULES**: With AWS Config, you can create custom rules that check the configuration of your AWS resources. These rules can enforce best practices for patch management. 
## Security Hub
+ Security Hub is a **centralized security and compliance management service** that provides a **comprehensive view of the security state of your AWS resources**.
+ It **collects and aggregates findings** from various AWS security services, such as GuardDuty, Amazon Inspector, and Patch Manager, in addition to third-party security tools.
+ With Security Hub, you can identify and prioritize security issues, automate compliance checks, and improve your overall security posture.
+ **If your accounts use Security Hub, they must have AWS Config**.
### How does Security Hub work with AWS Config?
+ Security Hub security checks **use the configuration items** recorded by AWS Config
+ **Configuration history**: AWS Config keeps a detailed history of your resource configurations. This can provide valuable context to Security Hub findings.
+ **Resource inventory and discovery**: AWS Config automatically discovers and records the configuration of your AWS resources. This provides Security Hub with an up-to-date view of your AWS environment, which can help to identify unprotected resources or resources that don’t comply with your security policies. 
+ **AWS CONFIG RULES**: You can define custom rules in AWS Config to automatically compare the configuration of your AWS resources with desired configurations. AWS Config can then send the evaluation results to Security Hub, offering continuous compliance checks and helping you pinpoint resources that fall outside your security and compliance standards. 
## Five key takeaways
+ **AWS security services**: You should now have a better understanding of the different AWS security services, such as **AWS Config, GuardDuty, CloudTrail, Amazon Inspector, Patch Manager, and Security Hub**. You should also understand how these services work individually and how they can be integrated with AWS Config for a unified security approach.
+ **Importance of configuration management and audits**: AWS Config tracks resource configurations over time, offers auditing tools for any resource state, and **enforces compliance with rules and conformance packs**. You can use these tools in incident response, compliance, and ongoing security management.
+ **Incident response and investigation**: You can use AWS services for **threat discovery (GuardDuty)**, investigating the incident (configuration history, configuration items, and CloudTrail), and **analyzing vulnerabilities (Amazon Inspector)**.
+ **Automated remediation and compliance**: By integrating **Patch Manager** with AWS Config, you can **automatically patch vulnerabilities**. AWS Config rules and conformance packs enforce compliance across AWS resources, which **minimizes the likelihood of human error leading to security incidents**.
+ **Ongoing security monitoring**: When you integrate AWS security services with Security Hub, you get a centralized view to continuously monitor and manage security alerts and compliance status.
## Use Case
+ Issue: **AnyCompany, in an initiative to bolster its security posture, deployed GuardDuty for a 30-day trial. During this period, GuardDuty raised an alarm signaling suspicious command and control traffic emanating from an EC2 instance running a web application within their virtual private cloud (VPC).**
+ In response, AnyCompany's security team used the details from the GuardDuty findings for their initial incident discovery and analysis. **They flagged the EC2 instance and promptly isolated it to prevent any potential spread of malicious activity.**
+ Simultaneously, the team employed **AWS Config to delve into the configuration history** of the flagged EC2 instance. The configuration history provided a thorough record of all configuration changes made to the instance over the past month.
+ **Detailed CloudTrail logs** aided the security team in backtracking, revealing changes to the Amazon EC2 web app and identifying introduced vulnerabilities promptly.
+ They discovered that a month prior, an update to the web application had inadvertently opened a security hole, which allowed command and control traffic to the EC2 instance. The **AWS Config configuration items** provided further insights into the vulnerable state of the EC2 instance.
+ After identifying the security flaw, the team used **Amazon Inspector to evaluate the compromised EC2 instance and all other EC2 instances for potential vulnerabilities**. Amazon Inspector revealed more EC2 instances with similar threats because of the same web application vulnerability.
+ **For remediation, the team used Patch Manager, integrating it with AWS Config, to automate the patching process for the vulnerabilities identified by Amazon Inspector**. The patching solution rectified the vulnerabilities and helped to secure the compromised EC2 instances.
+ To counteract the command and control traffic, AnyCompany adjusted their security groups and network access control lists (network ACLs) to block suspicious traffic. They also **used AWS Config conformance packs to regularly check and enforce these security group configurations and prevent any inadvertent exposure in the future**.
+ To continuously monitor and manage their security alerts and compliance status, the team integrated **GuardDuty*, CloudTrail, Amazon Inspector, and Patch Manager with Security Hub (powered by AWS Config)**. This unified view streamlined their security operations and helped them to detect and respond to security threats.
+ By using the suite of AWS security services, AnyCompany successfully navigated the security incident. They swiftly identified and mitigated a critical vulnerability, but also enhanced their security posture and processes to prevent future threats.
# Reference
+ [What Is AWS Config? - AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html)
+ [Getting Started with AWS Config](https://explore.skillbuilder.aws/learn/course/12609/play/49572/getting-started-with-aws-config)
+ [Build with AWS Config](https://explore.skillbuilder.aws/learn/course/18288/play/97894/build-with-aws-config)
