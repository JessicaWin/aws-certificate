# Overview
+ AWS CloudFormation is a service that helps you **model and set up your AWS resources** so that you can spend less time managing those resources and more time focusing on your applications that run in AWS.
+ You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and CloudFormation takes care of **provisioning and configuring** those resources for you.
+ By using CloudFormation, you easily **manage a collection of resources as a single unit**.
# Benefits
+ Simplify infrastructure management
    + A template describes all your resources and their properties. When you use that template to create a CloudFormation stack, CloudFormation provisions the Auto Scaling group, load balancer, and database for you
+ Quickly replicate your infrastructure
    + Reuse your CloudFormation template to create your resources in a consistent and repeatable manner. To reuse your template, describe your resources once and then provision the same resources over and over in multiple regions.
+ Easily control and track changes to your infrastructure
    + When you provision your infrastructure with CloudFormation, the CloudFormation template describes exactly what resources are provisioned and their settings.
# AWS CloudFormation concepts
## Templates
+ A CloudFormation **template is a JSON or YAML formatted text file**, CloudFormation uses these templates as blueprints for building your AWS resources
+ To provision and configure your stack resources, you must understand AWS CloudFormation templates, which are formatted text files in **JSON or YAML**.
+ These templates **describe the resources** that you want to provision in your AWS CloudFormation stacks
## Stacks
+ When you use CloudFormation, you **manage related resources as a single unit called a stack**. 
+ A stack is **a collection of AWS resources that you can manage as a single unit**.
+ In other words, you can create, update, or delete a collection of resources by creating, updating, or deleting stacks.
+ All the resources in a stack are **defined by the stack's AWS CloudFormation template**.
+ **Nested stacks** are stacks created as part of other stacks. You create a nested stack within another stack by using the AWS::CloudFormation::Stack resource.
    + Nested stacks can themselves contain other nested stacks, resulting in a hierarchy of stacks, as in the diagram below.
    + Certain stack operations, such as stack updates, should be initiated from the root stack rather than performed directly on nested stacks themselves. 
    + With change sets for nested stacks you can preview the changes to your application and infrastructure resources **across the entire nested stack hierarchy** and proceed with updates when you've confirmed that all the changes are as intended
+ AWS CloudFormation **sends events to EventBridge whenever a create, update, delete, or drift-detection operation is performed on a stack**. AWS CloudFormation also sends events to EventBridge for status changes to stack sets and stack set instances. 
## StackSets
+ AWS CloudFormation StackSets extends the capability of stacks by enabling you to **create, update, or delete stacks across multiple accounts and AWS Regions with a single operation**.
+ Using an administrator account, you define and manage an AWS CloudFormation template, and use the template as the basis for provisioning stacks into selected target accounts across specified AWS Regions.
+ ![AWS-Cloudformation-StackSets](./images/AWS-Cloudformation-StackSets.png)
+ StackSets concepts
    + **An administrator account** is the AWS account in which you **create stack sets**. For stack sets with service-managed permissions, the administrator account is either the **organization's management account or a delegated administrator account**.
    + **A target account** is the account into which you create, update, or delete one or more stacks in your stack set. Before you can use a stack set to create stacks in a target account, **set up a trust relationship** between the administrator and target accounts.
    + **A stack set** lets you create stacks **in AWS accounts across regions** by using a single CloudFormation template. A stack set's CloudFormation template defines all the resources in each stack. As you create the stack set, specify the template to use, in addition to any parameters and capabilities that template requires.
    + A stack set is a **regional resource**. If you create a stack set in one AWS Region, you can only see or change it when viewing that Region.
   + A stack instance is a reference to a stack in a target account within a Region. A stack instance can exist without a stack. For example, if the stack couldn't be created for some reason, the stack instance shows the reason for stack creation failure. A stack instance associates with only one stack set.
   + Stack set operations： Create stack set， Update stack set， Delete stacks， Delete stack set
   + The following figure shows the logical relationships between stack sets, stack operations, and stacks. When you update a stack set, all associated stack instances update throughout all accounts and Regions.
   + ![AWS-Cloudformation-StackSets-Components](./images/AWS-Cloudformation-StackSets-Components.png)
## **Change sets**
+ If you need to make changes to the running resources in a stack, you update the stack.+ Before making changes to your resources, you can generate a change set, which is a summary of your proposed changes.+ Change sets allow you to see** how your changes might impact your running resources**, especially for critical resources, before implementing them.
# How does AWS CloudFormation work
+ When creating a stack, AWS CloudFormation makes underlying service calls to AWS to provision and configure your resources.+ CloudFormation can only perform actions that you have permission to do
# Continuous delivery with CodePipeline
+ Continuous delivery is a release practice in which code changes are automatically built, tested, and prepared for release to production.
+ With AWS CloudFormation and CodePipeline, you can use continuous delivery to automatically build and test changes to your AWS CloudFormation templates before promoting them to production stacks.
+ This release process lets you rapidly and reliably make changes to your AWS infrastructure.
# Working with AWS CloudFormation Git sync
+ With Git sync, you can manage your CloudFormation stacks with source control. You do this by configuring AWS CloudFormation to monitor a Git repository.
+ The repository is monitored for changes to two files:
    + A CloudFormation template file that defines a stack
    + A stack deployment file that contains parameters that configure the stack
+ Git sync is accessed through the CloudFormation console when you create a stack.
+ When you commit changes to the template or the deployment file, CloudFormation automatically updates the stack. This way, you can use pull requests and version tracking to configure, deploy, and update your CloudFormation stacks from a centralized location.
+ Git sync supports GitHub, GitHub Enterprise, GitLab, and Bitbucket repositories.
# Using the AWS CloudFormation registry
+ The CloudFormation registry lets you manage extensions, both public and private, such as resources, modules, and hooks that are available for use in your AWS account.
+ Currently, the registry offers the following extension types:
    + Resource types – model and provision custom logic as a resource, using stacks in CloudFormation.
    + Modules – package resource configurations for inclusion across stack templates, in a transparent, manageable, and repeatable way.
    + Hooks – proactively inspect the configuration of your AWS resources before provisioning.
+ Use the CloudFormation registry to manage the extensions in your account, including:
    + Viewing the available and activated extensions.
    + Registering private extensions.
    + Activating public extensions.
# Reference
+ [What is AWS CloudFormation? - AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
+ [Getting Started with AWS CloudFormation](https://explore.skillbuilder.aws/learn/course/3627/play/12382/getting-started-with-aws-cloudformation)
+ [Introduction to AWS CloudFormation](https://explore.skillbuilder.aws/learn/course/194/play/8343/introduction-to-aws-cloudformation)
+ [AWS CloudFormation Stacks - Troubleshooting](https://explore.skillbuilder.aws/learn/course/1336/play;state=%5Bobject%20Object%5D;autoplay=0)
