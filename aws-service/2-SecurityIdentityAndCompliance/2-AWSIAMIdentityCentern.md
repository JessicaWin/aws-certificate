# Overview
+ AWS IAM Identity Center is the recommended AWS service for **managing human user access to AWS resources**. 
+ It is **a single place** where you can assign your workforce users, also known as workforce identities, consistent **access to multiple AWS accounts and application**s.
+ You can use **multi-account permissions** to assign your workforce users access to AWS accounts.
+ You can use **application assignments** to assign your users access to AWS managed and customer managed applications.
# IAM Identity Center capabilities
+ Manage workforce identities: Human users who build or operate workloads in AWS are also known as workforce users, or workforce identities
    + These individuals might be developers who build your internal and customer-facing systems, or users of internal database systems and applications.
    + You can **create workforce users and groups in IAM Identity Center**, or **connect and synchronize to an existing set of users and groups in your own identity source** for use across all your AWS accounts and applications
+ Manage instances of IAM Identity Center
    + IAM Identity Center supports two types of instances: **organization instances and account instances**.
    + An organization instance is the best practice. It's the only instance that **enables you to manage access to AWS accounts** and it's recommended for all production use of applications.
    + An organization instance is **deployed in the AWS Organizations management account** and gives you a single point from which to manage user access across the AWS environment.
    + Account instances are **bound to the AWS account in which they are enabled**. Use account instances of IAM Identity Center only to support isolated deployments of select AWS managed applications
+ Manage access to multiple AWS accounts
    + With multi-account permissions, you can plan for and centrally implement permissions across multiple AWS accounts at one time without needing to configure each of your accounts manually. 
    + This optional feature is **available only for organization instances**. 
+ Manage access to applications
    + IAM Identity Center enables you to simplify application access management. With IAM Identity Center, you can grant your workforce users in IAM Identity Center **single sign-on access to applications**.
+ AWS access portal access for your users
    + The AWS access portal is a simple web portal that provides your users with seamless access to all their assigned AWS accounts and applications.
# Key concepts
+ IAM Identity Center manages access to all your AWS Organizations accounts, Identity Center enabled applications, and other business applications that support the Security Assertion Markup Language (SAML) 2.0 standard.
+ Users, groups, and provisioning
    + User name and email address uniqueness
        + When working in IAM Identity Center, users must be uniquely identifiable.
        + IAM Identity Center requires that all user names and email addresses for your users are non-NULL and unique. 
    + Groups
        + Groups are a logical combination of users that you define. 
        + You can create groups and add users to the groups.
        + IAM Identity Center does not support adding a group to a group (nested groups).
        + Groups are useful when assigning access to AWS accounts and applications.
        + Rather than assign each user individually, you give permissions to a group.
        + Later, as you add or remove users from a group, the user dynamically gets or loses access to accounts and applications that you assigned to the group.
    + User and group provisioning
        + You can create users and groups directly in IAM Identity Center, or work with users and groups you have in Active Directory or an another external identity provider.
        + Provisioning is the process of making user and group information available for use by IAM Identity Center and Identity Center enabled applications.
            + IAM Identity Center configurable Active Directory (AD) sync enables you to explicitly configure the identities in Microsoft Active Directory that are automatically synchronized into IAM Identity Center and control the synchronization process.
            + IAM Identity Center refreshes the AD-based identity data in the identity store using the following process.
            + AD sync – When you make assignments for new users and groups by using the IAM Identity Center console or related assignment API actions, IAM Identity Center searches the domain controller directly for the specified users or groups, completes the assignment, and then periodically syncs the user or group metadata into IAM Identity Center.
            + Configurable AD sync – IAM Identity Center doesn't search your domain controller directly for users and groups. Instead, you must first specify the list of users and groups to sync. You can configure this list, also known as the sync scope, in one of the following ways, depending on whether you have users and groups that are already synced into IAM Identity Center, or you have new users and groups that you are syncing for the first time by using configurable AD sync.
+ Identity Center enabled applications
    + IAM Identity Center provides support for integration by other AWS applications and services. These applications can use IAM Identity Center to perform authentication and can access information about users and groups
    + IAM Identity Center has the ability to share the user and group information with Identity Center enabled applications. This capability makes it possible to connect an identity source to IAM Identity Center once and then share identity information with multiple applications in the AWS Cloud
+ SAML federation
    + IAM Identity Center supports identity federation with SAML (Security Assertion Markup Language) 2.0. SAML 2.0 is an industry standard used for securely exchanging SAML assertions that pass information about a user between a SAML authority (called an identity provider or IdP), and a SAML consumer (called a service provider or SP).
    + IAM Identity Center uses this information to provide federated single sign-on access for those users who are authorized to use applications within the AWS access portal.
    + Users can then single sign-on into services that support SAML, including the AWS Management Console and third-party applications such as Microsoft 365, SAP Concur, and Salesforce.
+ User authentications
    + A user signs in to the AWS access portal using their user name. When they do, IAM Identity Center redirects the request to the IAM Identity Center authentication service based on the directory associated with the user email address. 
    + Once authenticated, users have single sign-on access to any of the AWS accounts and third-party software-as-a-service (SaaS) applications that show up in the portal without additional sign-in prompts.
    + Authentication sessions
        + There are two types of authentication sessions maintained by IAM Identity Center: one to represent the users’ sign in to IAM Identity Center, and another to represent the users’ access to IAM Identity Center enabled applications, such as Amazon SageMaker Studio or Amazon Managed Grafana.
        + Each time a user signs in to IAM Identity Center, a sign in session is created for the duration configured in Identity Center, which can be up to 90 days
        + Each time the user accesses an Identity Center enabled application, the IAM Identity Center sign in session is used to obtain an IAM Identity Center application session for that application. IAM Identity Center application sessions have a refreshable 1-hour lifetime – that is, IAM Identity Center application sessions are automatically refreshed every hour as long as the IAM Identity Center sign in session from which they were obtained is still valid.
        + session expiration
            | User experience Or system behavior	| Time after user is disabled or deleted |
            |:------|:------|
            | User can no longer sign in to IAM Identity Center; user cannot obtain a new IAM Identity Center sign in session	| None (effective immediately) | 
            | User can no longer start new application or IAM role sessions via IAM Identity Center	| Up to 1 hour | 
            | User can no longer access any Identity Center enabled applications (all app sessions are terminated)	| Up to 2 hours (up to 1 hour for IAM Identity Center sign in session expiry, plus up to 1 hour for IAM Identity Center app session expiry) | 
            | User can no longer access any AWS accounts through IAM Identity Center	| Up to 13 hours (up to 1 hour for IAM Identity Center sign in session expiry, plus up to 12 hours for administrator-configured IAM role session expiry per the IAM Identity Center session duration settings for the permission set) | 
+ OAuth 2.0
    + IAM Identity Center supports OAuth 2.0 based identity federation through the OpenID Connect (OIDC) web service.
    + Device authorization grant
        + an application must first register a public client with the IAM Identity Center OIDC service. Once registered, the OIDC service provides the application with a client ID and a client secret, which you can use to generate tokens using the device authorization grant
        + When the application needs to access a protected resource in the future, it sends a request to the OIDC service to initiate device authorization. 
        + This request returns a verification URL and a device code. 
        + The IAM Identity Center authenticated user needs to use this device code and explicitly grant the application access to the requested resources. 
        + Once the user has granted access, the application can exchange the device code for an access token and a refresh token.
+ Permission sets
    + A permission set is a template that you create and maintain that defines a collection of one or more IAM policies. 
    + Permission sets simplify the assignment of AWS account access for users and groups in your organization. 
    + When you assign a permission set, IAM Identity Center creates corresponding IAM Identity Center-controlled IAM roles in each account, and attaches the policies specified in the permission set to those roles. 
    + IAM Identity Center manages the role, and allows the authorized users you’ve defined to assume the role, by using the IAM Identity Center User Portal or AWS CLI.  
    + As you modify the permission set, IAM Identity Center ensures that the corresponding IAM policies and roles are updated accordingly.
# Identity sources in IAM Identity Center
+ Your identity source in IAM Identity Center defines **where your users and groups are managed** 
+ **Identity Center directory**
    + When you enable IAM Identity Center for the first time, it's automatically configured with an Identity Center directory as your default identity source.
+ **Active Directory**
    + If you're already managing users and groups in either your AWS Managed Microsoft AD directory using AWS Directory Service or your self-managed directory in Active Directory (AD), we recommend that **you connect that directory when you enable IAM Identity Center**. 
    + **Don't create** any users and groups in the default Identity Center directory.
    + IAM Identity Center uses the connection provided by the AWS Directory Service to **synchronize user, group, and membership information** from your source directory in Active Directory to the IAM Identity Center identity store.
# **External identity provider**
+ For external identity providers (IdPs) such as Okta or Microsoft Entra ID, you can use IAM Identity Center to authenticate identities from the IdPs **through the Security Assertion Markup Language (SAML) 2.0 standard**. 
+ The SAML protocol doesn't provide a way to query the IdP to learn about users and groups.
+ You make IAM Identity Center aware of those users and groups by **provisioning them into IAM Identity Center**.
+ You can **perform automatic provisioning (synchronization)** of user and group information from your IdP into IAM Identity Center using the System for Cross-domain Identity Management (SCIM) v2.0 protocol **if your IdP supports SCIM**.
+ Otherwise, you can **manually provision** your users and groups by manually entering the user names, email address, and groups into IAM Identity Center.
# IAM roles
+ IAM Identity Center **creates IAM roles to give users permissions to resources**.
+ When you assign a permission set, IAM Identity Center **creates corresponding IAM Identity Center- controlled IAM roles in each account, and attaches the policies speciﬁed in the permission set to those roles**.
+ IAM Identity Center **manages the role**, and allows the authorized users you’ve deﬁned to assume the role, by using the AWS access portal or AWS CLI. 
+ As you modify the permission set, IAM Identity Center ensures that the corresponding IAM policies and roles are updated accordingly.
# IAM Identity Center features
+ Workforce identities
    + Human users who are members of your organization are also known as workforce identities or workforce users. You can create workforce users and groups in IAM Identity Center, or connect and synchronize to an existing set of users and groups in your own identity source for use across all your AWS accounts and applications. Supported identity sources include Microsoft Active Directory Domain Services, and external identity providers such as Okta Universal Directory or Microsoft Azure AD.
+ Application assignments for SAML applications
    + With application assignments, you can grant your workforce users in IAM Identity Center single sign-on access to SAML 2.0 applications, such as Salesforce and Microsoft 365. Your users can access these applications in a single place, without the need for you to set up separate federation.
+ Identity Center enabled applications
    + AWS applications and services, such as Amazon Managed Grafana, Amazon Monitron, and Amazon SageMaker Studio Notebooks, discover and connect to IAM Identity Center automatically to receive sign-in and user directory services. This provides users with a consistent single sign-on experience to these applications with no additional configuration of the applications. Because the applications share a common view of users, groups, and group membership, users also have a consistent experience when sharing application resources with others.
+ Multi-account permissions
    + With multi-account permissions you can plan for and centrally implement IAM permissions across multiple AWS accounts at one time without needing to configure each of your accounts manually. You can create fine-grained permissions based on common job functions or define custom permissions that meet your security needs. You can then assign those permissions to workforce users to control their access over specific accounts.
+ AWS access portal
    + The AWS access portal provides your workforce users with one-click access to all their assigned AWS accounts and cloud applications through a simple web portal.
# Prerequisites and considerations
+ Active Directory or an external IdP
    + If you're already managing users and groups in Active Directory or an external IdP, we recommend that you consider connecting this identity source when you enable IAM Identity Center and choose your identity source.
+ AWS Organizations
    + Your AWS account must be managed by AWS Organizations. 
+ AM roles
    + If you've already configured IAM roles in your AWS account, we recommend that you check whether your account is approaching the quota for IAM roles.
+ Next-generation firewalls and secure web gateways
    + If you filter access to specific AWS domains or URL endpoints by using a web content filtering solution such as NGFWs or SWGs, you must add the following domains or URL endpoints to your web-content filtering solution allow-lists. Doing so enables IAM Identity Center to function correctly.
# How to setup
+ Step 1: Enable IAM Identity Center. 
    + IAM Identity Center requires AWS Organizations.
+ Step 2: Choose your identity source
    + Your identity source in IAM Identity Center defines where your users and groups are managed. You can choose one of the following as your identity source:
    + Identity Center directory – When you enable IAM Identity Center for the first time, it is automatically configured with an Identity Center directory as your default identity source. This is where you create your users and groups, and assign their level of access to your AWS accounts and applications.
    + Active Directory – Choose this option if you want to continue managing users in either your AWS Managed Microsoft AD directory using AWS Directory Service or your self-managed directory in Active Directory (AD).
        + Connect a directory in AWS Managed Microsoft AD to IAM Identity Center: 
            + Open the IAM Identity Center console.
            + Choose Settings.
            + On the Settings page, choose the Identity source tab, and then choose Actions > Change identity source.
            + Under Choose identity source, select Active Directory, and then choose Next.
            + Under Connect active directory, choose a directory in AWS Managed Microsoft AD from the list, and then choose Next.
        + Connect a self-managed directory in Active Directory to IAM Identity Center
            + Create a two-way trust relationship. AWS IAM Identity Center requires a two-way trust so that it has permissions to read user and group information from your domain to synchronize user and group metadata. IAM Identity Center uses this metadata when assigning access to permission sets or applications. The trust from AWS Directory Service for Microsoft Active Directory to your domain permits IAM Identity Center to trust your domain for authentication. The trust in the opposite direction grants AWS permissions to read user and group metadata.
            + Create an AD Connector – AD Connector is a directory gateway that can redirect directory requests to your self-managed AD without caching any information in the cloud. For more information, see Connect to a Directory in the AWS Directory Service Administration Guide.
    + External identity provider – Choose this option if you want to manage users in an external identity provider (IdP) such as Okta or Azure Active Directory.
        + When using an external IdP, you must provision all users and groups into IAM Identity Center before you can make any assignments to AWS accounts or applications.
        + Regardless of how you provision users, IAM Identity Center redirects the AWS Management Console, command line interface, and application authentication to your external IdP. IAM Identity Center then grants access to those resources based on policies you create in IAM Identity Center. 
        + How to config
            + Open the IAM Identity Center console.
            + Choose Settings.
            + On the Settings page, choose the Identity source tab, and then choose Actions > Change identity source.
            + Under Choose identity source, select External identity provider, and then choose Next.
            + Under Configure external identity provider, do the following:
            + Under Service provider metadata, choose Download metadata file to download the metadata file and save it on your system. The IAM Identity Center SAML metadata file is required by your external identity provider.
            + Under Identity provider metadata, choose Choose file, and locate the metadata file that you downloaded from your external identity provider. Then upload the file. This metadata file contains the necessary public x509 certificate used to trust messages that are sent from the IdP.
        + IAM Identity Center supports automatic provisioning (synchronization) of user and group information from your identity provider (IdP) into IAM Identity Center using the System for Cross-domain Identity Management (SCIM) v2.0 protocol.
        + Supported identity providers
            + Topics
            + Azure AD
            + CyberArk
            + Google Workspace
            + JumpCloud
            + Okta
            + OneLogin
            + Ping Identity
            + AM Identity Center implements the following standards-based protocols for identity federation:
                + SAML 2.0 for user authentication
                + SCIM for provisioning
                + Any identity provider (IdP) that implements these standard protocols is expected to interoperate successfully with IAM Identity Center, with the following special considerations
    + After you connect your directory to IAM Identity Center, you can specify a user to whom you want to grant administrative permissions, and then synchronize that user from your directory into IAM Identity Center.
    + At this point, your user doesn't have access to the management account. You will set up administrative access to this account by creating an administrative permission set and assigning the user to that permission set.
+ Step 3: Create an administrative permission set
     -Permission sets are stored in IAM Identity Center and define the level of access that users and groups have to an AWS account.
+ Step 4: Set up AWS account access for an IAM Identity Center administrative user
    + To set up AWS account access for an IAM Identity Center administrative user, you must assign the user to the AdministratorAccess permission set.
+ Step 5: Sign in to the AWS access portal with your IAM Identity Center administrative user credentials
+ Step 6: Create a permission set that applies least-privilege permissions
    + With IAM Identity Center, you can assign multiple permission sets to the same user. 
    + To follow the best practice of applying least-privilege permissions, after you create your administrative user, create a more restrictive permission set and assign it to the same user. 
    + That way, you can access your AWS account with only the permissions that you require, rather than administrative permissions.
+ Step 7: Set up AWS account access for additional users (optional)
    + Now that you've created an administrative user in IAM Identity Center and assigned an additional permission set that you can use to perform tasks with least-privileged permissions, you can add other users. You can add users by doing any of the following:
    + Creating your users in IAM Identity Center. This is the quickest way to get started with IAM Identity Center.
    + Synchronizing your users from Active Directory
    + Synchronizing your users from your external identity provider (IdP)
    + After you add other users, create permission sets for these users and assign the users to the new permission sets as needed to grant them single sign-on access to one or more AWS accounts in your organization.
+ Step 8: Set up single sign-on access to your applications (optional)
    + With IAM Identity Center, you can use AWS applications that are integrated with IAM Identity Center, cloud applications for which AWS provides preintegration, and custom SAML 2.0 applications.
    + To add and configure your application
        + Open the IAM Identity Center console.
        + Choose Applications.
        + Choose Add application.
        + Under Applications, search for an application, and select the application from the list. Choose Next.
        + Under Configure application, the Display name and Description pre-populates with the application you chose. You can edit these. Under IAM Identity Center metadata, download or copy any certificate you might need. Under Application properties, optionally fill out the fields. Under Application metadata, fill out all the fields. Then, choose Submit. You're taken to the details page of the application that you just added.
    + To add and configure a cloud application
        + Open the IAM Identity Center console.
        + Choose Applications.
        + Choose Add application.
        + Under Applications, search for an application, and select the application from the list. Choose Next.
        + Under Configure application, the Display name and Description pre-populates with the application you chose. You can edit these.
        + Under IAM Identity Center metadata, do the following:
        + Under IAM Identity Center SAML metadata file, choose Download to download the identity provider metadata.
        + Under IAM Identity Center certificate, choose Download certificate to download the identity provider certificate.
            + You will need these files later when you set up the cloud application from the service provider's website. Follow the instructions from that provider.
        + (Optional) Under Application properties, you can specify additional properties for the Application start URL, Relay state, and Session duration. For more information, see Application properties in the IAM Identity Center console.
        + Under Application metadata, do one of the following:
        + Choose Upload application SAML metadata file. Then, select Choose file to find and select the metadata file.
        + If you do not have a metadata file, choose Manually type your metadata values, and then provide the Application ACS URL and Application SAML audience values.
        + Choose Submit. You're taken to the details page of the application that you just added.
    + To add and configure a custom SAML application
        + Open the IAM Identity Center console.
        + Choose Applications.
        + Choose Add application.
        + On the Select an application page, choose Add custom SAML 2.0 application. Then, choose Next.
        + On the Configure application page, under Configure application, enter a Display name for the application, such as MyApp. Then, enter a Description.
        + Under IAM Identity Center metadata, do the following:
        + Under IAM Identity Center SAML metadata file, choose Download to download the identity provider metadata.
        + Under IAM Identity Center certificate, choose Download certificate to download the identity provider certificate.
            + You will need these files later when you set up the custom application from the service provider's website.
        + (Optional) Under Application properties, you can specify additional properties for the Application start URL, Relay State, and Session Duration. For more information, see Application properties in the IAM Identity Center console.
        + Under Application metadata, choose Manually type your metadata values. Then, provide the Application ACS URL and Application SAML audience values.
        + Choose Submit. You're taken to the details page of the application that you just added.
# Using the AWS access portal
+ Your AWS access portal provides you with single sign-on access to all your AWS accounts and most commonly used cloud applications such as Office 365, Concur, Salesforce, and many more. 
+ From here you can quickly launch multiple applications simply by choosing the AWS account or application icon in the portal.
+ By default, you can access the AWS access portal by using a URL that follows this format: d-xxxxxxxxxx.awsapps.com/start. You can customize the URL as follows: your_subdomain.awsapps.com/start. If you change the AWS access portal, you can't edit it later.
+ When you enable multi-factor authentication (MFA), users must sign in to the AWS access portal with their user name and password. This is the first factor, something they know. Users must also sign in with either a code or security key. This is the second factor, something they have or something they are. 
# Multi-account permissions
+ AWS IAM Identity Center is integrated with AWS Organizations so that you can pick multiple AWS accounts whose users need single sign-on (SSO) access to the AWS Management Console. 
+ These AWS accounts can be either the management account of the AWS Organizations or a member account. 
+ A management account is the AWS account that is used to create the organization. 
+ The rest of the accounts that belong to an organization are called member accounts.
+ To use IAM Identity Center with AWS Organizations, you must first enable IAM Identity Center, which grants IAM Identity Center the capability to create Service-linked roles in each account in your organization. 
+ Delegated administration
    + Delegated administration provides a convenient way for assigned users in a registered member account to perform most IAM Identity Center administrative tasks.
    + When you enable IAM Identity Center, your IAM Identity Center instance is created in the management account in AWS Organizations by default. 
    + Even though your IAM Identity Center instance must always reside in the management account, you can choose to delegate administration of IAM Identity Center to a member account in AWS Organizations, thereby extending the ability to manage IAM Identity Center from outside the management account.
    + To configure delegated administration, you must first register a member account in your AWS organization as a delegated administrator. 
    + Prerequisites, Before you can register an account as a delegated administrator you must first have the following environment deployed:
        + AWS Organizations must be enabled and configured with at least one member account in addition to your default management account.
        + If your identity source is set to Active Directory, the IAM Identity Center configurable AD sync feature must be enabled.
+ Attributes for access control
    + Attributes for access control is the name of the page in the IAM Identity Center console where you select user attributes that you want to use in policies to control access to resources. You can assign users to workloads in AWS based on existing attributes in the users' identity source.
+ IAM identity provider
    + When you add single sign-on access to an AWS account, IAM Identity Center creates an IAM identity provider in each AWS account.
    + An IAM identity provider helps keep your AWS account secure because you don't have to distribute or embed long-term security credentials, such as access keys, in your application.
+ Service-linked roles
    + Service-linked roles are predefined IAM permissions that allow IAM Identity Center to delegate and enforce which users have single sign-on access to specific AWS accounts in your organization in AWS Organizations. 
    + The service enables this functionality by provisioning a service-linked role in every AWS account within its organization. 
    + The service then allows other AWS services like IAM Identity Center to leverage those roles to perform service-related tasks. 
    + When you enable IAM Identity Center, IAM Identity Center creates a service-linked role in all accounts within the organization in AWS Organizations. 
    + IAM Identity Center also creates the same service-linked role in every account that is subsequently added to your organization. 
    + This role allows IAM Identity Center to access each account's resources on your behalf.
# Application assignments
+ With AWS IAM Identity Center, you can easily control who can have single sign-on access to your cloud applications. 
+ Users get one-click access to these applications after they use their directory credentials to sign in to their AWS access portal.
+ IAM Identity Center securely communicates with these applications through a trusted relationship between IAM Identity Center and the application's service provider. 
+ This trust is created when you add the application from the IAM Identity Center console and configure it with the appropriate metadata for both IAM Identity Center and the service provider.
+ After the application has been successfully added to the IAM Identity Center console, you can manage which users or groups need permissions to the application
# Resiliency design and Regional behavior
+ When you enable IAM Identity Center, it is deployed to the AWS Region that is currently selected. 
+ If you want to deploy to a specific AWS Region, change the region selection before enabling IAM Identity Center.
+ Although IAM Identity Center determines access from the Region in which you enable the service, AWS accounts are global. This means that after users sign in to IAM Identity Center, they can operate in any Region when they access AWS accounts through IAM Identity Center. 
# Set up emergency access to the AWS Management Console
+ If you use IAM Identity Center, you can use these capabilities to create the emergency access configuration described in the following sections. 
+ This configuration enables you to use IAM Identity Center as the mechanism for AWS account access.
+ If IAM Identity Center is disrupted, your emergency operations users can sign in to the AWS Management Console through direct federation, by using the same credentials that they use to access their accounts.
+ This configuration works when IAM Identity Center is unavailable, but the IAM data plane and your external identity provider (IdP) are available.
# Reference
+ [IAM Identity Center](https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html)
+ [Introduction to AWS Identity and Access Management (IAM)](https://explore.skillbuilder.aws/learn/course/120/introduction-to-aws-identity-and-access-management-iam)
+ [Deep Dive with Security: AWS Identity and Access Management (IAM)](https://explore.skillbuilder.aws/learn/course/104/deep-dive-with-security-aws-identity-and-access-management-iam)
