# Overview
+ AWS OpsWorks is a **configuration management service** that helps you configure and operate applications in a cloud enterprise by **using Puppet or Chef**.
+ **AWS OpsWorks Stacks and AWS OpsWorks for Chef Automate** let you use Chef cookbooks and solutions for configuration management
+ **AWS OpsWorks for Puppet Enterprise** lets you configure a Puppet Enterprise master server in AWS.
# AWS OpsWorks for Puppet Enterprise
+ OpsWorks for Puppet Enterprise lets you **launch a Puppet Enterprise master in minutes**, and **lets AWS OpsWorks handle its operations, backups, restorations, and software upgrades**. 
+ OpsWorks for Puppet Enterprise lets you **create AWS-managed Puppet master servers**.
+ An OpsWorks for Puppet Enterprise master **runs on an Amazon Elastic Compute Cloud instance**.
+ A Puppet master server **manages nodes in your infrastructure, stores facts about those nodes, and serves as a central repository for your Puppet modules**. 
+ Modules are reusable, shareable units of Puppet code that contain instructions about how your infrastructure should be configured.
+ OpsWorks for Puppet Enterprise lets you use Puppet to **automate how nodes are configured, deployed, and managed**, whether they are Amazon EC2 instances or on-premises devices. 
+ An OpsWorks for Puppet Enterprise master provides **full-stack automation** by handling tasks such as software and operating system configurations, package installations, database setups, change management, policy enforcement, monitoring, and quality assurance.
# AWS OpsWorks for Chef Automate
+ Node, CookBook, Recipe
+ AWS OpsWorks for Chef Automate lets you **create AWS-managed Chef servers** that include Chef Automate premium features, and use the Chef DK and other Chef tooling to manage them. 
+ A Chef server **manages nodes in your environment, stores information about those nodes, and serves as a central repository for your Chef cookbooks**. 
+ Chef Automate is an **included server software package** that provides **automated workflow for continuous deployment and compliance checks**.
# AWS OpsWorks Stacks
+ AWS OpsWorks for Chef Automate lets you provision a Chef server within minutes, and let AWS OpsWorks for Chef Automate handle its operations, backups, restorations, and software upgrades.
+ Cloud-based computing usually involves **groups of AWS resources**, such as EC2 instances and Amazon Relational Database Service (RDS) instances. This group of instances is typically called a *stack*.
+ AWS OpsWorks Stacks, the original service, **provides a simple and flexible way to create and manage stacks and applications**.
+ AWS OpsWorks Stacks lets you deploy and monitor applications in your stacks. 
+ You can create stacks that help you manage cloud resources in specialized groups called **layers**. 
+ A layer represents **a set of EC2 instances that serve a particular purpose**, such as serving applications or hosting a database server. 
+ Layers depend on **Chef recipes** to handle tasks such as installing packages on instances, deploying apps, and running scripts.
+ AWS OpsWorks Stacks **monitors instance health, and provisions new instances** for you, when necessary, by using **Auto Healing and Auto Scaling**.
# Reference
+ [What Is AWS OpsWorks? - AWS OpsWorks](https://docs.aws.amazon.com/opsworks/latest/userguide/welcome.html)
+ [Introduction to AWS OpsWorks Stacks](https://explore.skillbuilder.aws/learn/course/221/play/3842/course-feedback)
+ [Introduction to AWS OpsWorks for Chef Automate](https://explore.skillbuilder.aws/learn/course/200/play/25346/introduction-to-aws-opsworks-for-chef-automate)