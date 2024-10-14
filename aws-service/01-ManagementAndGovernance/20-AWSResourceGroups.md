# Overview
+ AWS Resource Groups is the service that lets you **manage and automate tasks on large numbers of resources at one time**.
+ You can use *resource groups* to **organize your AWS resources.**
+ A *resource group* is a collection of AWS resources that are **all in the same AWS Region**, and that match the criteria specified in the group's query.
+ In Resource Groups, there are two types of queries you can use to build a group 
    + Tag-based queries include lists of resources and tags. 
    + AWS CloudFormation stack-based
+ Resource groups **can be nested**; a resource group can contain existing resource groups in the same region.
# Use cases for resource groups
+ By default, the AWS Management Console is **organized by AWS service.**
+ But with Resource Groups, you can create a custom console that organizes and consolidates information **based on criteria specified in tags, or the resources in an AWS CloudFormation stack**. 
# AWS Resource Groups and permissions
+ Resource Groups feature permissions are at the **account level**.
+ As long as users who are sharing your account have the correct IAM permissions, they can work with resource groups that you create.
# Reference
[What are resource groups? - AWS Resource Groups and Tags](https://docs.aws.amazon.com/ARG/latest/userguide/resource-groups.html)
