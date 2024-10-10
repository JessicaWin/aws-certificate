# Amazon Elastic Container Registry
+ Amazon Elastic Container Registry (Amazon ECR) is an **AWS managed container image registry service** that is secure, scalable, and reliable.
+ Amazon ECR supports **private container image repositories** with **resource-based permissions using AWS IAM**. This is so that specified users or Amazon EC2 instances can access your container repositories and images.
+ You can use your preferred CLI to push, pull, and manage Docker images, Open Container Initiative (OCI) images, and OCI compatible artifacts.
# Components of Amazon ECR
+ Registry: An Amazon ECR registry is provided to each AWS account; you can **create image repositories** in your registry and **store images** in them.
+ Authorization token: Your client must authenticate to Amazon ECR registries as an AWS user before it can push and pull images.
+ Repository: An Amazon ECR image repository **contains your Docker images**, Open Container Initiative (OCI) images, and OCI compatible artifacts.
+ Repository policy: You can **control access** to your repositories and the images within them with repository policies. 
+ Image: You can **push and pull container images to your repositories**. You can use these images locally on your development system, or you can use them in Amazon ECS task definitions and Amazon EKS pod specifications
# Features of Amazon ECR
+ Lifecycle policies help with **managing the lifecycle** of the images in your repositories. 
+ Image scanning helps in **identifying software vulnerabilities** in your container images.
+ Cross-Region and cross-account replication makes it easier for you to have your images where you need them. 
# Private registries
+ By default, **your account has read and write access** to the repositories in your private registry.
+ However, **IAM users require permissions** to make calls to the Amazon ECR APIs and to push or pull images to and from your private repositories.
+ You must **authenticate your Docker client to your private registry** so that you can use the **docker push** and **docker pull** commands to push and pull images to and from the repositories in that registry.
+ Private repositories can be controlled with both **IAM user access policies and repository policies**
+ The repositories in your private registry can be **replicated across Regions in your own private registry and across separate accounts** by configuring replication for your private registry. 
+ Amazon ECR uses **registry settings** to configure features at the registry level. The private registry settings are configured separately for each Region.
# Private repositories
+ Amazon Elastic Container Registry (Amazon ECR) provides API operations to create, monitor, and delete image repositories and set permissions that control who can access them.
+ Amazon ECR uses **resource-based permissions** to control access to repositories. Resource-based permissions let you specify which IAM users or roles have access to a repository and what actions they can perform on it. 
# Amazon Elastic Container Registry Public
+ Amazon Elastic Container Registry Public is a managed AWS container image registry service that is secure, scalable, and reliable.
+ Amazon ECR supports **public image repositories** with **resource-based permissions** using AWS IAM so that specific users can access your public repositories to push images.
## Components of Amazon ECR Public
+ Amazon ECR Public Gallery: The Amazon ECR Public Gallery is the public portal that **lists all public repositories** hosted on Amazon ECR Public.
+ Registry: A public registry is provided to each AWS account; you can create public image repositories in your public registry and store images in them. 
+ Authorization token:Your client must authenticate to a public registry as an AWS user before it can push images to a public repository. 
+ Repository: An Amazon ECR image repository contains your Docker images, Open Container Initiative (OCI) images, and OCI compatible artifacts. 
+ Repository policy:You can control access to your repositories and the images within them with repository policies. 
+ Image:You can push and pull container images to your repositories. 
## Public registry
+ Each repository you create in **your public registry is available publicly** in the Amazon ECR Public Gallery.
+  **Anyone will be able to pull images** from your public repository from the Amazon ECR Public Gallery
+ By default, your account has read and write access to the repositories in your public registry.
+ However,IAM users **require permissions** to make calls to the Amazon ECR APIs and to **push images to** your repositories.
+ Repositories can be controlled with both IAM user access policies and repository policies. 

# Reference
+ [Amazon ECR](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html)
+ [Getting Started with Amazon ECR](https://explore.skillbuilder.aws/learn/course/14289/play/63065/getting-started-with-amazon-ecr)