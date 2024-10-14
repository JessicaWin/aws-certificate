
# Overview
+ AWS Proton is Automated infrastructure provisioning and deployment of **serverless and container-based applications**
+ The AWS Proton service is a **two-pronged automation framework**.
+ **Administrators create versioned service templates** that define standardized infrastructure and deployment tooling for serverless and container-based applications.
+ Then, you can **select from the available service templates to automate your application or service deployments**.
+ Standardized infrastructure 
    + Platform teams can use AWS Proton and versioned infrastructure-as-code templates to define and manage standard application stacks that contain the architecture, infrastructure resources and the CI/CD software deployment pipeline.
+ Deployments integrated with CI/CD 
    + AWS Proton automatically provisions the resources, configures the CI/CD pipeline and deploys the code into the defined infrastructure.
# AWS Proton concepts
![./images/AWS-Proton.png](./images/AWS-Proton.png)
+ As an **Administrator**, you create and register an **Environment Template** with AWS Proton, which defines the shared resources.
+ AWS Proton deploys one or more **Environments**, based on an **Environment Template**.
+ As an **Administrator**, you create and register a **Service Template** with AWS Proton, which defines the related infrastructure, monitoring and CI/CD resources along with compatible **Environment Templates**.
+ As a **Developer**, you select a registered **Service Template** and provide a link to your **Source code** repository.
+ AWS Proton deploys the **Service** with a **CI/CD Pipeline** for your **Service instances**.
+ AWS Proton deploys and manages the **Service** and the **Service Instances** that are running the **Source code** as was defined in the selected **Service Template**. A **Service Instance** is an instantiation of the selected **Service Template** in an **Environment** for a single stage of a **Pipeline** (for example Prod).
# Reference
[What is AWS Proton? - AWS Proton](https://docs.aws.amazon.com/proton/latest/userguide/Welcome.html)
