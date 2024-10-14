## Amazon Lightsail


+ Amazon Lightsail is the** easiest way to get started with Amazon Web Services** (AWS) for developers who need to build websites or web applications.+ It includes everything you need to launch your project quickly - instances (virtual private servers), container services, managed databases, content delivery network (CDN) distributions, load balancers, SSD-based block storage, static IP addresses, DNS management of registered domains, and resource snapshots (backups) - for a low, predictable monthly price.

##  AWS ParallelCluster


+ AWS ParallelCluster is an AWS supported open source **cluster management tool** that helps you to deploy and manage** high performance computing (HPC) clusters** in the AWS Cloud.+ Built on the open source CfnCluster project, AWS ParallelCluster enables you to** quickly build an HPC compute environment** in AWS.+ It automatically sets up the required compute resources and shared filesystem.+ You can use AWS ParallelCluster with batch schedulers, such as AWS Batch and Slurm.+ AWS ParallelCluster facilitates quick start proof of concept deployments and production deployments.+ You can also build higher level workflows, such as a genomics portal that automates an entire DNA sequencing workflow, on top of AWS ParallelCluster.


## AWS App Runner


+ AWS App Runner is an AWS service that provides a fast, simple, and cost-effective way to **deploy from source code or a container image directly to a scalable and secure web application** in the AWS Cloud.+ App Runner connects directly to your code or image repository. It provides an automatic integration and delivery pipeline with fully managed operations, high performance, scalability, and security.


### App Runner concepts


+ *App Runner service* – An AWS resource that App Runner uses to **deploy and manage your application** based on its source code repository or container image. An App Runner service is **a running version of your application**. + *Source type* – The type of source repository that you provide for deploying your App Runner service: [source code](https://docs.aws.amazon.com/apprunner/latest/dg/service-source-code.html) or [source image](https://docs.aws.amazon.com/apprunner/latest/dg/service-source-image.html).+ *Repository provider* – The repository service that contains your application source (for example, [GitHub](https://docs.aws.amazon.com/apprunner/latest/dg/service-source-code.html#service-source-code.providers.github) or [Amazon ECR](https://docs.aws.amazon.com/apprunner/latest/dg/service-source-image.html#service-source-image.providers.ecr)).+ *App Runner connection* – An AWS resource that lets App Runner access a repository provider account (for example, a GitHub account or organization).+ *Runtime* – A base image for deploying a source code repository. App Runner provides a variety of *managed runtimes* for different programming environments. + *Deployment* – An action that applies a version of your source repository (code or image) to an App Runner service.+ *Custom domain* – A domain that you associate with your App Runner service. Users of your web application can use this domain to access your web service instead of the default App Runner subdomain.+ *Maintenance* – An activity that App Runner occasionally performs on the infrastructure that runs your App Runner service. When maintenance is in progress, service status temporarily changes to `OPERATION_IN_PROGRESS `for a few minutes. Actions on your service (for example, deployment, configuration update, pause/resume, or deletion) are blocked during this time. Try the action again a few minutes later, when the service status returns to `RUNNING`.


