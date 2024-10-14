# Overview
+ Amazon Simple Notification Service (Amazon SNS) is a managed service that provides **message delivery from publishers to subscribers** (also known as *producers* and *consumers*).
+ Publishers communicate **asynchronously with subscribers by sending messages to a topic**, which is a logical access point and communication channel.
+ Clients can subscribe to the SNS topic and receive published messages using a supported endpoint type, such as Amazon Kinesis Data Firehose, Amazon SQS, AWS Lambda, HTTP, email, mobile push notifications, and mobile text messages (SMS).
# Features and capabilities
+ **Application-to-application messaging**
    + Application-to-application messaging supports subscribers such as Amazon Kinesis Data Firehose delivery streams, Lambda functions, Amazon SQS queues, HTTP/S endpoints, and AWS Event Fork Pipelines. 
+ **Application-to-person notifications**
    + Application-to-person notifications provide user notifications to subscribers such as mobile applications, mobile phone numbers, and email addresses.
+ **Standard and FIFO topics**
    + Use a **FIFO topic** to ensure **strict message ordering**, to define message groups, and to prevent message duplication. 
    + Only Amazon SQS FIFO queues can subscribe to a FIFO topic.
    + Use a standard topic when message delivery order and possible message duplication are not critical.
+ **Message durability**
    + Amazon SNS uses a number of strategies that work together to provide message durability: 
    + Published messages are stored across multiple, geographically separated servers and data centers.
    + If a subscribed endpoint isn't available, Amazon SNS runs a delivery retry policy.
    + To preserve any messages that aren't delivered before the delivery retry policy ends, you can create a dead-letter queue.
+ **Message archiving and analytics**
    + You can subscribe Kinesis Data Firehose delivery streams to SNS topics, which allow you to send notifications to additional archiving and analytics endpoints such as Amazon Simple Storage Service (Amazon S3) buckets, Amazon Redshift tables, and more.
+ **Message attributes**
    + Message attributes let you provide any arbitrary metadata about the message. Amazon SNS message attributes.
+ **Message filtering**
    + By default, each subscriber receives every message published to the topic.
    + To receive a subset of the messages, a subscriber must assign a filter policy to the topic subscription. 
+ **Message security**
    + Server-side encryption protects the contents of messages that are stored in Amazon SNS topics, using encryption keys provided by AWS KMS. 
    + You can also establish a private connection between Amazon SNS and your virtual private cloud (VPC).
# Amazon SNS event sources and destinations
+ Amazon SNS can receive event-driven notifications from many AWS sources and fan out notifications to application-to-application (A2A) and application-to-person (A2P) destinations. 
# Message ordering and deduplication (FIFO topics)
+ **Message grouping**: Messages that belong to the same group are processed one by one, in a strict order relative to the group.
+ There is no limit to the number of group IDs in SNS FIFO topics or SQS FIFO queues.
+ To preserve strict message ordering, Amazon SNS restricts the set of supported delivery protocols for Amazon SNS FIFO topics. 
+ Currently, the endpoint protocol must be Amazon SQS, with an Amazon SQS FIFO queue's Amazon Resource Name (ARN) as the endpoint.
+ SNS FIFO topics can't deliver messages to customer managed endpoints
+ When you subscribe an Amazon SQS FIFO queue to an SNS FIFO topic, you can use message **filtering** to specify that the subscriber receives a subset of messages, rather than all of them. 
+ If a message with a particular **deduplication** ID is successfully published to an SNS FIFO topic, any message published with the same deduplication ID, within the **five-minute deduplication interval**, is accepted but not delivered.
+ If the message body is guaranteed to be unique for each published message, you can enable **content-based deduplication** for an Amazon SNS FIFO topic and the subscribed SQS FIFO queues. 
# Amazon SNS message archiving and analytics
+ Amazon SNS provides message archiving and analytics through **Amazon Kinesis Data Firehose.** You can fan out notifications to Kinesis Data Firehose delivery streams, which allows you to send notifications to storage and analytics destinations that Kinesis Data Firehose supports, including Amazon Simple Storage Service (Amazon S3), Amazon Redshift
# Application-to-application (A2A) messaging
+ Fanout to Kinesis Data Firehose delivery streams
+ Fanout to Lambda functions
+ Fanout to Amazon SQS queues
+ Fanout to HTTP/S endpoints
+ Fanout to AWS Event Fork Pipelines
# Using Amazon SNS for application-to-person (A2P) messaging
+ Mobile text messaging (SMS)
+ Mobile push notifications
+ Email notifications
# Reference
+ [Amazon Simple Notification Service](https://docs.aws.amazon.com/sns/latest/dg/welcome.html)
