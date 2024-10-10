# Overview
+ Amazon MQ is a **managed message broker service** that makes it easy to migrate to a message broker in the cloud. 
+ ​Amazon SQS and Amazon SNS are queue and topic services that are highly scalable, simple to use, and don't require you to set up message brokers. 
+ A message broker allows software applications and components to communicate using various programming languages, operating systems, and formal messaging protocols.
+ Currently, Amazon MQ supports **Apache ActiveMQ and RabbitMQ** engine type
# ActiveMQ engine
+ A **broker** is a message broker environment running on Amazon MQ. It is the basic building block of Amazon MQ. 
+ A *single-instance broker* is comprised of one broker in one Availability Zone.The broker communicates with your application and with an **Amazon EBS or Amazon EFS** storage volume.
+ An *active/standby broker* is comprised of two brokers in two different Availability Zones, configured in a *redundant pair*.These brokers communicate synchronously with your application, and with **Amazon EFS**.
+ A **configuration** contains all of the settings for your ActiveMQ broker, in XML format (similar to ActiveMQ's `activemq.xml` file). 
    + You can create a configuration before creating any brokers. You can then apply the configuration to one or more brokers.
+ An ActiveMQ **user** is a person or an application that can access the queues and topics of an ActiveMQ broker. You can configure users to have specific permissions.
+ Amazon MQ for ActiveMQ supports Amazon Elastic File System (EFS) and Amazon Elastic Block Store (EBS).
# RabbitMQ engine
+ A **broker** is a message broker environment running on Amazon MQ.  
+ A **single-instance broker** is comprised of one broker in one Availability Zone behind a Network Load Balancer (NLB) The broker communicates with your application and with an Amazon EBS storage volume.
+ A **cluster deployment** is a logical grouping of three RabbitMQ broker nodes behind a Network Load Balancer, each sharing users, queues, and a distributed state across multiple Availability Zones (AZ).
+ Every AMQP 0-9-1 client connection has an associated user which **must be authenticated**. 
+ Each client connection also targets **a virtual host (vhost) for which the user must have a set of permissions**.
+ A user may have permission to **configure**, **write** to, and **read** from queues and exchanges in a vhost.
# Reference
+ [Amazon MQ](https://docs.aws.amazon.com/amazon-mq/latest/developer-guide/welcome.html)
