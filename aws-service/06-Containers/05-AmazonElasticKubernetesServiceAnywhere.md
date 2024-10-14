# Overview
+ EKS Anywhere is container management software built by AWS that makes it easier to **run and manage Kubernetes clusters on-premises and at the edge**. 
+ EKS Anywhere is **built on EKS Distro** , which is the same reliable and secure Kubernetes distribution used by Amazon Elastic Kubernetes Service (EKS) in AWS Cloud.
+ EKS Anywhere **simplifies Kubernetes cluster management** through the automation of undifferentiated heavy lifting such as infrastructure setup and Kubernetes cluster lifecycle operations.
+ Unlike Amazon EKS in AWS Cloud, EKS Anywhere is a **user-managed product that runs on user-managed infrastructure**. You are responsible for cluster lifecycle operations and maintenance of your EKS Anywhere clusters. EKS Anywhere is open source and free to use at no cost. 
+ Amazon EKS Anywhere helps you create and operate on-premises Kubernetes clusters running directly on **bare-metal servers or using VMware vSphere**.
+ Amazon EKS Anywhere also offers integrations with AWS Cloud services, such as Amazon Elastic Container Registry (Amazon ECR) and Amazon Simple Storage Service (Amazon S3), to help you use AWS services for your on-premises workloads.
# Why EKS Anywhere?
+ Simplify and automate Kubernetes management on-premises
+ Unify Kubernetes distribution and support across on-premises, edge, and cloud environments
+ Adopt modern operational practices and tools on-premises
+ Build on open source standards
# Common Use Cases
+ Modernize on-premises applications from virtual machines to containers
+ Internal development platforms to standardize how teams consume Kubernetes across the organization
+ Telco 5G Radio Access Networks (RAN) and Core workloads
+ Regulated services in private data centers on-premises
# How to setup Amazon EKS Anywhere prerequisites
+ Step 1: Download the eksctl CLI tool
+ Step 2: Install the Amazon EKS Anywhere plugin
+ Step 3: Install the Docker provider
# Create an Amazon EKS Anywhere Cluster
+ Step 1: Define the cluster configuration
    + You can generate a cluster configuration template by using the eksctl anywhere CLI tool you installed earlier. 
    + Set the name of your cluster as an environment variable, which can then be used to generate the config file with the same name. 
    + eksctl anywhere generate clusterconfig $CLUSTER_NAME --provider docker > $CLUSTER_NAME.yaml
+ Step 2: Create the cluster
    + eksctl anywhere create cluster -f $CLUSTER_NAME.yaml
+ Step 3: Access the cluster
# Deploy an Application to an Amazon EKS Anywhere Cluster
+ kubectl apply -f "https://anywhere.eks.amazonaws.com/manifests/hello-eks-a.yaml"


# Reference
+ [Amazon EKS Anywhere](https://anywhere.eks.amazonaws.com/docs/overview/)
+ [Getting Started with Amazon EKS Anywhere](https://explore.skillbuilder.aws/learn/course/14268/getting-started-with-amazon-eks-anywhere)