# Overview
+ AWS CloudTrail is an AWS service that helps you enable **governance, compliance, and operational and risk auditing** of your AWS account.
+ **Actions** taken by a user, role, or an AWS service are **recorded as events in CloudTrail**.
+ Events include actions taken in the **AWS Management Console, AWS Command Line Interface, and AWS SDKs and APIs**.
+ Visibility into your AWS account activity is a key aspect of security and operational best practices. You can use CloudTrail to **view, search, download, archive, analyze, and respond to account activity across your AWS infrastructure**.
+ Optionally, you can **enable AWS CloudTrail Insights on a trail** to help you **identify and respond to unusual activity**.
# How CloudTrail works
+ CloudTrail is **enabled** on your AWS account when you create it.
+ When activity occurs in your AWS account, that activity is **recorded in a CloudTrail event**.
+ You can easily view events in the CloudTrail console by going to **Event history**.
+ **Event history** allows you to view, search, and download the **past 90 days of activity** in your AWS account.
+ In addition, you can **create a CloudTrail trail to archive, analyze, and respond to changes** in your AWS resources.
+ A trail is a configuration that **enables delivery of events to an Amazon S3 bucket** that you specify. You can also deliver and analyze events in a trail with **Amazon CloudWatch Logs and Amazon CloudWatch Events**.
+ You can create two types of trails for an AWS account: 
    + **A trail that applies to all regions**
    + **A trail that applies to one region**
    + If you create a trail that logs events in all AWS Regions, it will appear in the console in all AWS Regions. If you create a trail that only logs events in a single AWS Region, you can view and manage it only in that AWS Region
+ If you have created an organization in AWS Organizations, you can also create a trail that will **log all events for all AWS accounts in that organization**. This is referred to as an ***organization trail***.  
+ Organization trails can apply to all AWS Regions or one Region
+ Organization trails must be created in the management account
+ Member accounts will be able to see the organization trail, but cannot modify or delete it
+ By default, CloudTrail event log files are encrypted using **Amazon S3 server-side encryption (SSE)**. You can also choose to encrypt your log files with an AWS Key Management Service (AWS KMS) key. 
# Which problems does CloudTrail solve?
+ With AWS CloudTrail, you can monitor your AWS activity comprehensively.
+ You can gain visibility into users and resource activity by obtaining a history of all the AWS API calls made in your account.
+ With CloudTrail, you can monitor API calls made by using the AWS Management Console, the AWS SDKs, the command line tools, and higher-level AWS services. + You can identify which users and accounts called AWS APIs for services that support CloudTrail.
+ Additionally, you can **identify the source IP address** from which the calls were made, and when the calls occurred. This helps during operational, security incident troubleshooting, and also helps in risk auditing, governance, and compliance of your AWS account.
+ With CloudTrail, you can do the following:
    + Centralize a collection of activity data to manage multi-Region and multi-account environments.
    + Audit by automatically recording and storing activity logs.
    + Integrate with SQL query syntax for log analysis.
    + Address regulatory and compliance requirements for auditing.
    + Monitor data usage, detect exfiltration, and adjust AWS IAM roles' permissions.
    + Build security automation by tracking and responding to threats, and use CloudTrail Insights to detect unusual activity.
    + Troubleshoot security and operational issues by tracking changes in your accounts.
    + Detect operation issues by integrating with Amazon CloudWatch Logs.
# CloudTrail concepts
+ An **event** in CloudTrail is the record of an activity in an AWS account. 
    + This activity can be an action taken by **a user, role, or service** that is monitorable by CloudTrail.
    + CloudTrail events provide a history of both **API and non-API account activity** made through the **AWS Management Console, AWS SDKs, command line tools, and other AWS services**.
    + There are three types of events that can be logged in CloudTrail: 
        + **management events**: management operations that are performed on resources in your AWS account
        + **data events**: resource operations performed on or in a resource
        + **CloudTrail Insights events**: CloudTrail Insights events capture **unusual API call rate or error rate activity** in your AWS account. 
    + By default, trails log management events, but not data or Insights events.
+ **CloudTrail event history** provides a viewable, searchable, and downloadable record of the past 90 days of CloudTrail events.
+ A **trail** is a configuration that enables delivery of CloudTrail events to an Amazon S3 bucket, CloudWatch Logs, and CloudWatch Events.
    + Collect and store management and data events from multi-Region and multi-account environments.
    + Store the logs for a custom period of time to meet regulatory requirements.
    + Integrate trails for CloudTrail to store activity in CloudWatch Logs or AWS CloudTrail Lake.
    + Filter data events using advanced event selectors.
+ An **organization trail** is a configuration that enables delivery of CloudTrail events in the management account and all member accounts in an AWS Organizations organization to the same Amazon S3 bucket, CloudWatch Logs, and CloudWatch Events.
+ **CloudTrail Lake** lets you run **fine-grained SQL-based queries** on your events.
    + **Integration with CloudWatch Logs** enables CloudTrail to **send events containing API activity in your AWS account to a CloudWatch Logs log group**.
        + You can optionally configure **CloudWatch alarms** to send notifications or make changes to the resources that you are monitoring based on log stream events that your metric filters extract.
    + In **CloudWatch Events**, you can create rules that trigger on any event recorded by CloudTrail. 
# AWS CloudTrail Lake
+ It is a managed data lake that helps organizations aggregate, immutably store, and query events recorded by CloudTrail for auditing, security investigation, and operational troubleshooting.
+ It has a fully immutable collection of events.
+ The event data store is optimized for search using SQL queries.
+ It provides events management across multiple accounts and Regions within your AWS Organization in one central location.
+ You can filter events using advanced event selectors.
+ CloudTrail Lake is a managed data lake designed for organizations to aggregate, securely store, and query CloudTrail events for auditing, security investigation, and operational troubleshooting.
+ It ensures the full immutability of collected events and offers optimized event data storage for efficient search using SQL queries.
+ With CloudTrail Lake, you can conveniently manage events from multiple accounts and Regions within your AWS Organization, all in one centralized location.
+ Additionally, you can use advanced event selectors for seamless event filtering.
# AWS service integrations 
+ Using **Athena** with CloudTrail logs is a powerful way to enhance your analysis of AWS service activity. 
+ You can configure CloudTrail with **CloudWatch Logs** to monitor your trail logs and be notified when specific activity occurs.
+ You can create a trail in the management account for an organization that collects all event data for all AWS accounts in an organization in **AWS Organizations**.
# CloudTrail costs
+ Remember that CloudTrail provides the ﬁrst trail for CloudTrail for delivery of all management events included in the AWS Free Tier. If you conﬁgure more than one trail, additional charges will occur.
+ If you use other underlying services, such as CloudWatch Logs, to deliver a copy of CloudTrail logged events to CloudWatch Logs, additional charges will occur.
+ CloudTrail Lake offers 7 years of storage and is priced based on amount of storage used and data scanned from SQL querying on the logs.
+ CloudTrail insights is priced based on the total amount of events analyzed.
# CloudTrail Insights
+ CloudTrail Insights is not automatically activated, and you must explicitly turn it on.
+ When you turn on CloudTrail Insights events for a trail, CloudTrail starts monitoring the write management events captured by that trail for unusual patterns.
# Questions
+ What are the benefits of using AWS CloudTrail? (Select THREE.)
    + **Integrate with SQL tools, such as Amazon Athena, for log analysis.** 
    + Eliminate the need to set up a secure environment.
    + **Audit AWS account and API activity.**
    + **Integrate with a purpose-built data lake for auditing, security investigation, and operational troubleshooting.**
    + Store event history automatically for 7 years.
    + Monitor resource performance metrics.
+ Which problems does AWS CloudTrail solve?
    + **It provides auditing, security monitoring, and operational troubleshooting by tracking user activity and API usage.**
    + It offers automatic remediation for any suspicious activity.
    + It provides recommendations to improve security posture.
    + It automatically stores account activity for 7 years for audit purposes.(default 90 days)
    + It automatically tracks management and data events without any configuration, providing a holistic view during audits.
+ Which use case is an example for AWS CloudTrail?
    + **Detect unauthorized access.**
    + Prevent distributed denial of service (DDoS) attacks on servers.
    + Monitor resource usage.
    + Provide vulnerability assessments for Amazon Elastic Compute Cloud (Amazon EC2).
    + Throttle API activity in an AWS account.
+ If I am a new AWS customer or existing AWS customer and don’t have CloudTrail set up, do I need to enable or set up anything to view my account activity?
    + No, nothing is required to begin viewing your account activity. You can visit the AWS CloudTrail console or AWS CLI and begin viewing up to the past 90 days of account activity.
# Reference
+ [What Is AWS CloudTrail? - AWS CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)
+ [AWS CloudTrail Getting Started](https://explore.skillbuilder.aws/learn/course/193/play/97881/aws-cloudtrail-getting-started)