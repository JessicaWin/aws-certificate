# Overview
+ Amazon Managed Streaming for Apache Kafka (Amazon MSK) is a fully managed service that enables you to build and run applications that use Apache Kafka to process streaming data.
# Components
+ **Broker nodes** — When creating an Amazon MSK cluster, you specify how many broker nodes you want Amazon MSK to **create in each Availability Zone**. In the example cluster shown in this diagram, there's one broker per Availability Zone. Each Availability Zone has its own virtual private cloud (VPC) subnet.
+ **ZooKeeper nodes** — Amazon MSK also creates the Apache ZooKeeper nodes for you. Apache ZooKeeper is an open-source server that enables highly reliable distributed coordination.
+ **Producers, consumers, and topic creators** — Amazon MSK lets you use Apache Kafka data-plane operations to create topics and to produce and consume data.
+ **Cluster Operations** You can use the AWS Management Console, the AWS Command Line Interface (AWS CLI), or the APIs in the SDK to perform control-plane operations.

![amazon_msk](./images/amazon_msk.png)
 + Amazon MSK **detects and automatically recovers** from the most common failure scenarios for clusters so that your producer and consumer applications can continue their write and read operations with minimal impact.
#  Reference
[Amazon Managed Streaming for Apache Kafka](https://docs.aws.amazon.com/msk/latest/developerguide/what-is-msk.html)
