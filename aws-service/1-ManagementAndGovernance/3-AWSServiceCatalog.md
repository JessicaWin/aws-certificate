# Overview
+ AWS Service Catalog enables organizations to **create and manage catalogs of IT services** that are approved for AWS.
+ These IT services can include **everything from virtual machine images, servers, software, databases, and more to complete multi-tier application architectures**.
+ AWS Service Catalog allows organizations to **centrally manage commonly deployed IT services**, and helps organizations achieve **consistent governance and meet compliance requirements**.
+ AWS Service Catalog provides the following benefits: 
    + Standardization
    + Self-service discovery and launch
    + Fine-grain access control
    + Extensibility and version control
# AWS Service Catalog Concepts
## **Users**
+ **Catalog administrators (administrators)** – **Manage a catalog of products** (applications and services), organizing them into portfolios and **granting access to end users**. Catalog administrators prepare AWS CloudFormation templates, configure constraints, and manage IAM roles for products to provide for advanced resource management.
+ **End users** – **Receive AWS credentials** from their IT department or manager and use the AWS Management Console to **launch products to which they have been granted access**. Sometimes referred to as simply *users*, end users may be granted **different permissions depending on your operational requirements**.
## **Products**
+ A product is an **IT service** that you want to make available **for deployment** on AWS.
+ A product consists of one or more AWS resources
+ A product can be a single compute instance running AWS Linux, a fully configured multi-tier web application running in its own environment, or anything in between
+ You create a product by **importing an AWS CloudFormation template**
## **Provisioned Products**
+ AWS CloudFormation stacks make it easier to manage the lifecycle of your product by enabling you to provision, tag, update, and terminate your product instance as a **single unit**.
+ A *provisioned product* is a stack.
## ​​​​​​​​​​​​​​**Portfolios**
+ A portfolio is a **collection of products** that contains configuration information. 
+ Portfolios help **manage who can use specific products and how they can use them**. 
+ When you add a new *version* of a product to a portfolio, that version is automatically available to all current users.
+ Through the use of portfolios, permissions, sharing, and constraints, you can ensure that users are launching products that are configured properly for the organization’s needs and standards
## **Versioning**
+ **​​​​​​​**AWS Service Catalog allows you to manage **multiple versions of the products** in your catalog. 
+ When you create a new version of a product, the update is automatically distributed to all users who have access to the product, allowing the user to select which version of the product to use.
## **Permissions**
+ Granting a user access to a portfolio enables that user to browse the portfolio and launch the products in it. 
## **Constraints**
+ Constraints control **the ways that you can deploy specific AWS resources** for a product.
+ You can use them to apply limits to products for governance or cost control.
+ There are different types of AWS Service Catalog constraints: **launch** constraints, **notification** constraints, and **template** constraints. 
+ With launch constraints, you **specify a role for a product in a portfolio**. Use this role to provision the resources at launch, so you can restrict user permissions without impacting users' ability to provision products from the catalog.
+ Notification constraints enable you to **get notifications about stack events** using an Amazon SNS topic.
+ Template constraints **restrict the configuration parameters** that are available for the user when launching the product (for example, EC2 instance types or IP address ranges). With template constraints, you reuse generic AWS CloudFormation templates for products and apply restrictions to the templates on a **per-product or per-portfolio basis**.
# Using AppRegistry
+ Use AWS Service Catalog AppRegistry to create a repository of your applications and associated resources. 
+ An AppRegistry application consists of associated resources and attribute groups.
+ An application resource can be either an AWS Service Catalog provisioned product or an AWS CloudFormation stack.
+ You can associate a resource with only one application.
+ For every application, AppRegistry creates an application resource group.
+ An application resource group is a collection of the resources in your application. 

## Reference
[What Is AWS Service Catalog? - AWS Service Catalog](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/introduction.html)

