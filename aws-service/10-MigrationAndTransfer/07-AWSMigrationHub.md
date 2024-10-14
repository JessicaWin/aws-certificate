# Overview
+ AWS Migration Hub (Migration Hub) provides a single place to **discover your existing servers, plan migrations, and track the status of each application migration**. 
+ Migration Hub supports migration status updates from the following tools: 
    + AWS Application Migration Service (Application Migration Service)
    + AWS Server Migration Service (AWS SMS)
    + AWS Database Migration Service (AWS DMS)
# Migration Hub home Region
+ You can specify a home Region from the Migration Hub Settings page or from the Migration Hub Home Region API Reference
+ From your Migration Hub home Region, you can **track your migration into any AWS Region**. The status of migrations for your entire portfolio appears in your selected home Region
+ All of the discovery and migration tracking data sent from AWS tools or partner migration tools is **stored and processed in your home Region, regardless of the migrating application’s target Region**.
# Discovering on-premises resources
+ AWS Migration Hub (Migration Hub) provides a single place to **discover your existing servers, plan migrations, and track the status of each application migration**.
+ Before migrating you can discover information about your on-premises server and application resources to help you build a business case for migrating or to build a migration plan.
+ To start discovery and planning, you can **deploy data collectors, such as AWS Application Discovery Agent or AWS Agentless Discovery Connector, into your data centers**.
+ These tools send data to the AWS Migration Hub service in your home Region, and the information is displayed on your home Region console.
+ Before you install your data collectors, your home Region must be set.
+ Before collecting data, you must **register your collectors in your home Region**. 
+ You get the data about your servers and applications into the AWS Migration Hub console by using the following discovery tools. 
    + **Migration Hub import** – With Migration Hub import, you can import information about your on-premises servers and applications into Migration Hub, including server specifications and utilization data.
    + **AWS Agentless Discovery Connector** – The Discovery Connector is a VMware appliance that can collect information about **VMware virtual machines** (VMs)
    + **AWS Application Discovery Agent** – The Discovery Agent is AWS software that you install on your on-premises servers and VMs to capture system configuration, system performance, running processes, and details of the network connections between systems.  Support physical on-premises servers, Amazon EC2 instances, and virtual machines.
# Migrate And Track
+ Migration Hub gives you the choice to **start migrating right away** and group servers while migration is underway, or to **first discover servers and then group them into applications**. 
# AWS Migration Hub Refactor Spaces
+ AWS Migration Hub Refactor Spaces is the starting point for **incremental application refactoring to microservices in AWS**.
+ You can use Refactor Spaces to help reduce risk when evolving applications into microservices or extending existing applications with new features written in microservices.
## Refactor Spaces concepts
+ **Environment**
    + The Refactor Spaces environment **provides a unified view of networking, applications, and services across multiple AWS accounts**.
    + A Refactor Spaces environment contains Refactor Spaces applications and services.+ The *environment owner* is the account that the Refactor Spaces environment is created in.
    + The Refactor Spaces environment **simplifies cross-account networking** by orchestrating AWS Transit Gateway, AWS Resource Access Manager, and virtual private clouds (VPCs).
+ **Applications**
    + A Refactor Spaces application **contains services and routes and provides a single external endpoint** to expose the application to external callers. 
    + The application provides a **Strangler Fig proxy for incremental application refactoring**. 
    + A Refactor Spaces application orchestrates Amazon API Gateway, Network Load Balancer, and resource-based AWS Identity and Access Management (IAM) policies so that you can **transparently add new services to an external HTTP endpoint**.
    + You can also incrementally route traffic to the new services. This **keeps underlying architecture changes transparent for your application consumers**.
+ **Services**
    + Refactor Spaces services **provide your application’s business capabilities** and are reachable through unique endpoints.
    + Service endpoints are one of two types: an **HTTP/HTTPS URL, or an AWS Lambda function.**
+ **Route**
    + A Refactor Spaces route is a **proxy matching rule that forwards a request to a service**.
    + Each request is run against the set of routes configured in the application.
    + If a rule matches, the request is sent to the target service configured for that rule.
# Reference
+ [AWS Migration Hub](https://docs.aws.amazon.com/migrationhub/latest/ug/whatishub.html)
+ [AWS Migration Hub Refactor Spaces](https://docs.aws.amazon.com/migrationhub-refactor-spaces/latest/userguide/what-is-mhub-refactor-spaces.html)
