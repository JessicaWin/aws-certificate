# Overview
+ You can use Amazon Kinesis Data Streams to **collect and process large streams of data records in real time**. 
+ You can use Kinesis Data Streams for **rapid and continuous data intake and aggregation**.
+ Although you can use Kinesis Data Streams to solve a variety of streaming data problems, a common use is the **real-time aggregation of data followed by loading the aggregate data into a data warehouse or map-reduce cluster.**
+ Data is put into Kinesis data streams, which ensures **durability and elasticity**. + **Multiple Kinesis Data Streams applications** can consume data from a stream, so that multiple actions, like archiving and processing, can **take place concurrently and independently**. 
+ The Kinesis Client Library enables **fault-tolerant consumption** of data from streams and provides scaling support for Kinesis Data Streams applications.
# High-level architecture

![amazon_kinesis_data_stream.png](./images/amazon_kinesis_data_stream.png)
# Kinesis Data Stream
+ A *Kinesis data stream* is a **set of shards.**
+ The unit of data stored by Kinesis Data Streams is a **data record**.
+ Each shard has **a sequence of data records**.The data records in a data stream are **distributed into shards.**
+ Each data record has a sequence number that is assigned by Kinesis Data Streams.
+ Amazon Kinesis Data Streams ingests a large amount of data in real time, durably stores the data, and makes the data available for consumption.
+ When you create a stream, you specify the number of shards for the stream. The total capacity of a stream is the sum of the capacities of its shards.
+ You can increase or decrease the number of shards in a stream as needed. However, you are **charged on a per-shard basis**.
+ To determine the initial size of a stream, you need the following input values: 
    + The average size of the data record written to the stream in kilobytes (KB), rounded up to the nearest 1 KB, the data size (`average_data_size_in_KB`).
    + The number of data records written to and read from the stream per second (`records_per_second`).
    + The number of Kinesis Data Streams applications that consume data concurrently and independently from the stream, that is, the consumers (`number_of_consumers`).+ The incoming write bandwidth in KB (`incoming_write_bandwidth_in_KB`), which is equal to the `average_data_size_in_KB` multiplied by the `records_per_second`.
    + The outgoing read bandwidth in KB (`outgoing_read_bandwidth_in_KB`), which is equal to the `incoming_write_bandwidth_in_KB` multiplied by the `number_of_consumers`.
    + number_of_shards = max(incoming_write_bandwidth_in_KiB/1024, outgoing_read_bandwidth_in_KiB/2048)
# Data Record
+ A *data record* is the unit of data stored in a Kinesis data stream.
+ Data records are composed of a sequence number, a partition key, and a data blob, which is an immutable sequence of bytes.
+ Kinesis Data Streams does not inspect, interpret, or change the data in the blob in any way.
+ A data blob can be **up to 1 MB**.
# Retention Period
+ The *retention period* is **the length of time that data records are accessible** after they are added to the stream.
+ A stream’s retention period is set to a default of **24 hours** after creation. You can increase the retention period up to **8760 hours (365 days)**
+ **Additional charges** apply for streams with a retention period set to more than 24 hours. 
# Producer
+ A *producer* puts data records into Amazon Kinesis data streams.
+ To put data into the stream, you must specify **the name of the stream, a partition key, and the data blob** to be added to the stream. 
+ The partition key is used to **determine which shard** in the stream the data record is added to.
+ The number of partition keys should typically be much greater than the number of shards.
+ If you have enough partition keys, the data can be evenly distributed across the shards in a stream.
+ Each data record has a *sequence number* that is unique per partition-key within its shard.
# Consumer
+ *Consumers* get records from Amazon Kinesis Data Streams and process them.
+ These consumers are known as Amazon Kinesis Data Streams Application.
+ A consumer, known as an *Amazon Kinesis Data Streams application*, is an application that you build to read and process data records from Kinesis data streams.
+ If you want to send stream records directly to services such as **Amazon Simple Storage Service (Amazon S3), Amazon Redshift, Amazon OpenSearch Service (OpenSearch Service), or Splunk** you can use a **Kinesis Data Firehose delivery stream** instead of creating a consumer application.
+ When you build a consumer, you can deploy it to an Amazon EC2 instance by adding to one of your Amazon Machine Images (AMIs). You can **scale the consumer by running it on multiple Amazon EC2 instances under an Auto Scaling group**.
# Amazon Kinesis Data Streams Application
+ An *Amazon Kinesis Data Streams application* is a consumer of a stream that commonly runs on a fleet of EC2 instances.
+ There are two types of consumers that you can develop: shared fan-out consumers and enhanced fan-out consumers. 
+ The output of a Kinesis Data Streams application can be input for another stream, enabling you to create complex topologies that process data in real time.
+ An application can also send data to a variety of other AWS services. **There can be multiple applications for one stream, and each application can consume data from the stream independently and concurrently.**
# Shard
+ A *shard* is a uniquely identified sequence of data records in a stream.
+ A stream is composed of one or more shards, each of which provides a fixed unit of capacity.
+ The data capacity of your stream is a function of the number of shards that you specify for the stream. The total capacity of the stream is the sum of the capacities of its shards.
+ If your data rate increases, you can increase or decrease the number of shards allocated to your stream.
+ The default shard quota is 500 shards per AWS account for the following AWS regions: US East (N. Virginia), US West (Oregon), and Europe (Ireland). For all other regions, the default shard quota is 200 shards per AWS account.
+ A single shard can ingest up to **1 MB of data per second** (including partition keys) or **1,000 records per second** for writes. The maximum size of the data payload of a record before base64-encoding is **up to 1 MB**.
+ Each shard can support up to a maximum total data read rate of **2 MB per second via GetRecords**
+ Each call to `GetRecords` is counted as **one read transaction**.
+ Each shard can support up to **five read transactions per second.**
+ Each read transaction can provide up to **10,000 records with an upper quota of 10 MB per transaction**.
# Partition Key
+ A *partition key* is used to group data by shard within a stream.
+ Kinesis Data Streams segregates the data records belonging to a stream into multiple shards. It uses the partition key that is associated with each data record to determine which shard a given data record belongs to.
+ When an application puts data into a stream, it must specify a partition key.
# Sequence Number
+ Each data record has a *sequence number* that is unique per partition-key within its shard. Kinesis Data Streams assigns the sequence number after you write to the stream with `client.putRecords` or `client.putRecord`.
+ Sequence numbers for the same partition key generally increase over time. The longer the time period between write requests, the larger the sequence numbers become.
# Kinesis Client Library
+ The Kinesis Client Library is compiled into your application to enable fault-tolerant consumption of data from the stream.
+ The Kinesis Client Library ensures that for every shard there is a record processor running and processing that shard.
+ The library also simplifies reading data from the stream.
+ The Kinesis Client Library uses an Amazon DynamoDB table to store control data. It creates one table per application that is processing data.
# Application Name
+ The name of an Amazon Kinesis Data Streams application identifies the application.
+ Each of your applications must have **a unique name that is scoped to the AWS account and Region** used by the application.
+ This name is used as a name for the control table in Amazon DynamoDB and the namespace for Amazon CloudWatch metrics.
# Server-Side Encryption
+ Amazon Kinesis Data Streams can automatically **encrypt sensitive data as a producer enters it into a stream**.
+ Kinesis Data Streams uses AWS KMS master keys for encryption.
# Writing Data to Amazon Kinesis Data Streams
+ Using the KPL
    + The KPL is an easy-to-use, highly configurable library that helps you write to a Kinesis data stream. It acts as an intermediary between your producer application code and the Kinesis Data Streams API actions. 
    + The Kinesis Producer Library (KPL) simplifies producer application development, allowing developers to achieve high write throughput to a Kinesis data stream.
    + The KPL performs the following primary tasks: 
        + Writes to one or more Kinesis data streams with an automatic and configurable retry mechanism
        + Collects records and uses `PutRecords` to write multiple records to multiple shards per request
        + Aggregates user records to increase payload size and improve throughput
        + Integrates seamlessly with the Kinesis Client Library (KCL) to de-aggregate batched records on the consumer
        + Submits Amazon CloudWatch metrics on your behalf to provide visibility into producer performance
+ Using the Amazon Kinesis Data Streams API+ Using Kinesis Agent 
    + Kinesis Agent is a **stand-alone Java software application** that offers an easy way to collect and send data to Kinesis Data Streams.
    + The agent continuously **monitors a set of files and sends new data to your stream**. 
    + By default, records are parsed from each file based on the newline (`'\n'`) character, However, the agent can also be configured to parse multi-line records
# Reading Data from Amazon Kinesis Data Streams
+ use an AWS Lambda function
+ You can use an Amazon Kinesis Data Analytics application to process and analyze data in a Kinesis stream using SQL, Java, or Scala.
+ You can use a Kinesis Data Firehose to read and process records from a Kinesis stream. 
    + Kinesis Data Firehose is a fully managed service for **delivering real-time streaming data to destinations such as Amazon S3, Amazon Redshift, Amazon OpenSearch Service, and Splunk**.
    + Kinesis Data Firehose also supports any custom HTTP endpoint or HTTP endpoints owned by supported third-party service providers, including Datadog, MongoDB, and New Relic.
+ use the Kinesis Client Library (KCL) 
    + KCL helps you consume and process data from a Kinesis data stream by taking care of many of the complex tasks associated with distributed computing. These include load balancing across multiple consumer application instances, responding to consumer application instance failures, checkpointing processed records, and reacting to resharding+ The KCL performs the following tasks: 
        + Connects to the data stream
        + Enumerates the shards within the data stream
        + Uses leases to coordinates shard associations with its workers
        + Instantiates a record processor for every shard it manages
        + Pulls data records from the data stream
        + Pushes the records to the corresponding record processor
        + Checkpoints processed records
        + Balances shard-worker associations (leases) when the worker instance count changes or when the data stream is resharded (shards are split or merged)
+ Developing Custom Consumers with Dedicated Throughput (Enhanced Fan-Out)
+ Developing Custom Consumers with Shared Throughput
# Reference
[Amazon Kinesis Data Streams](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)

