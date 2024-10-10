# Overview
+ AWS Directory Service provides **multiple ways to use Microsoft Active Directory (AD) with other AWS services**.
+ Directories store information about **users, groups, and devices**, and administrators use them to **manage access to information and resources**.
+ AWS Directory Service provides multiple directory choices for customers who want to use existing **Microsoft AD or Lightweight Directory Access Protocol** (LDAP)–aware applications in the cloud.
# Which to choose
+ **AWS Managed Microsoft AD** is your best choice if you **need actual Active Directory features** to support AWS applications or Windows workloads, including Amazon Relational Database Service for Microsoft SQL Server. It's also best if you **want a standalone AD in the AWS Cloud that supports Office 365** or you **need an LDAP directory to support your Linux applications**.
+ **AD Connector** is your best choice when you want to **use your existing on-premises directory with compatible AWS services**.
+ Use **Simple AD** if you need a low-scale, low-cost directory with basic Active Directory compatibility that supports Samba 4–compatible applications, or you need LDAP compatibility for LDAP-aware applications.
+ Use [Amazon Cognito](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/what_is.html#cognito) if you develop high-scale SaaS applications and need a scalable directory to manage and authenticate your subscribers and that works with social media identities.
# AWS Managed Microsoft AD
+ AWS Directory Service lets you run Microsoft Active Directory (AD) as a managed service.
+ When you select and launch this directory type, it is created as **a highly available pair of domain controllers** connected to your virtual private cloud (VPC)
+ By default each directory consists of **two DCs**, each installed in a **different Availability Zone**. 
+ The domain controllers run in different Availability Zones in a Region of your choice. 
+ With AWS Managed Microsoft AD, you can run **directory-aware workloads** in the AWS Cloud, including Microsoft SharePoint and custom .NET and SQL Server-based applications.
+ You can also **configure a trust relationship between AWS Managed Microsoft AD in the AWS Cloud and your existing on-premises Microsoft Active Directory**, providing users and groups with access to resources in either domain, using **single sign-on (SSO)**.
+ Once your directory is created, you can use it for a variety of tasks: 
    +  Manage users and groups
    + Provide single sign-on to applications and services
    + Create and apply group policy
    + Simplify the deployment and management of cloud-based Linux and Microsoft Windows workloads
    + You can use AWS Managed Microsoft AD to enable multi-factor authentication by integrating with your existing RADIUS-based MFA infrastructure to provide an additional layer of security when users access AWS applications.
    + Securely connect to A mazon EC2 Linux and Windows instances 
##  Prerequisites
+  At least **two subnets**. Each of the subnets must be in a different Availability Zone.
+ The VPC must have **default hardware tenancy**.
+ You cannot create a AWS Managed Microsoft AD in a VPC using addresses in the 198.18.0.0/15 address space.
+  AWS Directory Service uses a two VPC structure. **The EC2 instances which make up your directory run outside of your AWS account, and are managed by AWS**. They have two network adapters, `ETH0` and `ETH1`. **`ETH0` is the management adapter, and exists outside of your account**. `ETH1` is created within your account.
+ The management IP range of your directory's **ETH0 network is 198.18.0.0/15**.  
## Active Directory schema
+ A schema is the **definition of attributes and classes** that are part of a distributed directory and is similar to fields and tables in a database.
+ Schemas include **a set of rules which determine the type and format of data that can be added or included in the database**.
+ **Attributes, classes and objects** are the basic elements that are used to build object definitions in the schema.
## Patching and maintenance
+ By default each directory consists of **two DCs**, each installed in a different Availability Zone. At your option, you may add DCs to further increase availability.
+ AWS patches your DCs **sequentially**, during which time the DC that AWS is actively patching is unavailable. In the event that one or more of your DCs is temporarily out of service, AWS **defers patching until your directory has at least two operational DCs**.
+ To ensure your applications can reach an operating DC in the event that one or more DCs is unavailable for any reason, including patching, your applications should **use the Windows DC locator service and not use static DC addresses**.
## Use Case
+ Sign in to AWS applications and services with AD credentials: When you enable an AWS application or service in your directory, your users can **access the application or service with their AD credentials**.
+ Manage Amazon EC2 instances 
+ Using familiar AD administration tools, you can apply AD group policy objects (GPOs) to **centrally manage your Amazon EC2** for Windows or Linux instances by [joining your instances to your AWS Managed Microsoft AD domain](https://docs.aws.amazon.com/en_us/directoryservice/latest/admin-guide/ms_ad_join_instance.html).
+ In addition, your users can **sign in to your instances with their AD credentials**. This eliminates the need to use individual instance credentials or distribute private key (PEM) files. 
+ Provide directory services to your AD-aware workloads
+ You can use AWS Managed Microsoft AD to provide SSO for cloud applications.
+ Extend your on-premises AD to the AWS Cloud 
+ If you already have an AD infrastructure and want to use it when migrating AD-aware workloads to the AWS Cloud, AWS Managed Microsoft AD can help.
    + You can use [AD trusts](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/ms_ad_tutorial_test_lab_trust.html) to connect AWS Managed Microsoft AD to your existing AD.
    + This means your users can access AD-aware and AWS applications with their on-premises AD credentials, without needing you to synchronize users, groups, or passwords.
+ Share your directory to seamlessly join Amazon EC2 instances to a domain across AWS accounts 
+ Sharing your directory across multiple AWS accounts enables you to manage AWS services such as Amazon EC2 easily without the need to operate a directory for each account and each VPC
    + This capability makes it easier and more cost effective to manage directory-aware workloads with a single directory across accounts and VPCs
## Secure your AWS Managed Microsoft AD directory
+ Manage **password policies**
+ enable multi-factor authentication (**MFA**) 
+ Enable secure LDAP (**LDAPS**) 
+ By default, communications over LDAP are not encrypted.
+ **Server-side LDAPS** support encrypts LDAP communications between your commercial or homegrown LDAP-aware applications and your AWS Managed Microsoft AD directory.
+ **Client-side LDAPS** support in AWS Managed Microsoft AD encrypts communications between Microsoft Active Directory (AD) and AWS applications.
## Multi-Region replication
+ Multi-Region replication can be used to **automatically replicate** your AWS Managed Microsoft AD directory data **across multiple Regions**.
+ When configured, AWS replicates all customer directory data including users, groups, group policies, and schema across multiple AWS Regions
+ This replication can **improve performance** for users and applications in disperse geographic locations. 
+ Multi-Region replication is only supported for the **Enterprise Edition** of AWS Managed Microsoft AD
+ The initial Region where you first created your directory is referred to as the **primary Region**.
+ You can perform only **global directory level operations** such as creating Active Directory trusts and updating the AD schema from the primary Region.
+ Any Regions that you have added to your directory are referred to as **additional Regions**
+ Although some features can be managed globally for all Regions, others are managed individually per Region.
# Active Directory Connector
+ AD Connector is **a directory gateway** with which you can **redirect directory requests to your on-premises Microsoft Active Directory** without caching any information in the cloud.
+ AD Connectors and your on-premises AD domains have a **1-to-1 relationship**
+ AD Connector cannot be shared with other AWS accounts.
+ Once set up, AD Connector offers the following benefits: 
    + Your end users and IT administrators can use their existing corporate credentials to log on to AWS applications such as WorkSpaces, Amazon WorkDocs, or Amazon WorkMail.
    + You can manage AWS resources like Amazon EC2 instances or Amazon S3 buckets through IAM role-based access to the AWS Management Console.
    + You can consistently enforce existing security policies (such as password expiration, password history, and account lockouts) whether users or IT administrators are accessing resources in your on-premises infrastructure or in the AWS Cloud.
    + You can use AD Connector to enable multi-factor authentication by integrating with your existing RADIUS-based MFA infrastructure to provide an additional layer of security when users access AWS applications
+ To connect to your existing directory with AD Connector, you need set up a VPC with the following: 
    + At least two subnets. Each of the subnets must be in a different Availability Zone.
    + The VPC must be connected to your existing network through a virtual private network (VPN) connection or AWS Direct Connect.
    + The VPC must have default hardware tenancy.
# Simple Active Directory
+ Simple AD is a **standalone managed directory** that is powered by a Samba 4 Active Directory Compatible Server. It is available in two sizes. 
    + Small - Supports up to 500 users (approximately 2,000 objects including users, groups, and computers).
    + Large - Supports up to 5,000 users (approximately 20,000 objects including users, groups, and computers).
+ Simple AD provides **a subset of the features offered by AWS Managed Microsoft AD**, including the ability to manage user accounts and group memberships, create and apply group policies, securely connect to Amazon EC2 instances, and provide Kerberos-based single sign-on (SSO)
+ To create a Simple AD directory, you need a VPC with the following: 
    + At least two subnets.
    + The VPC must have default hardware tenancy.
# Reference
[What is AWS Directory Service? - AWS Directory Service](https://docs.aws.amazon.com/directoryservice/latest/admin-guide/what_is.html)
