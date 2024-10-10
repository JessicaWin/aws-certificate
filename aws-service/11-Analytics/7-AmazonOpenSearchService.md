# Overview
+ Amazon OpenSearch Service (successor to Amazon Elasticsearch Service) is a managed service that makes it easy to deploy, operate, and scale OpenSearch clusters in the AWS Cloud. Amazon OpenSearch Service supports OpenSearch and legacy Elasticsearch OSS.
+ *OpenSearch* is a fully **open-source search and analytics engine** for use cases such as **log analytics, real-time application monitoring, and clickstream analysis**
+ *OpenSearch Service* provisions all the resources for your cluster and launches it. It also **automatically detects and replaces failed OpenSearch Service nodes,** reducing the overhead associated with self-managed infrastructures.
+ You can **scale your cluster** with a single API call or a few clicks in the console.
+ For OpenSearch Service, you pay for each hour of use of an EC2 instance and for the cumulative size of any EBS storage volumes attached to your instances.
# Creating and managing domains
+ Domains are clusters with the settings, instance types, instance counts, and storage resources that you specify.
+ Amazon OpenSearch Service uses a **blue/green deployment process** when updating domains. Blue/green typically refers to the practice of running two production environments, one live and one idle, and switching the two as you make software changes.
+ **To prevent data loss and minimize Amazon OpenSearch Service cluster downtime** in the event of a service disruption, you can distribute nodes across two or three *Availability Zones* in the same Region, a configuration known as **Multi-AZ**. 
+ If you enable Multi-AZ, you should create **at least one replica for each index** in your cluster. Without replicas, OpenSearch Service can't distribute copies of your data to other Availability Zones, which largely defeats the purpose of Multi-AZ.
+ For domains that run production workloads, we recommend the following configuration: 
    + Choose a Region that **supports three Availability Zones** with OpenSearch Service.
    + Deploy the domain **across three zones**.
    + Choose **current-generation instance types** for dedicated master nodes and data nodes.
    + Use **three dedicated master nodes and at least three data nodes**.
    + Create **at least one replica for each index** in your cluster.
    + recommend that you choose an instance count that is **a multiple of three** if you plan to have two or more replicas per index
+ Even if you select two Availability Zones when configuring your domain, OpenSearch Service automatically distributes dedicated master nodes across three Availability Zones

![amazon_opensearch](./images/amazon_opensearch.png)
+ Snapshots in Amazon OpenSearch Service are **backups of a cluster's indices and state**. *State* includes cluster settings, node information, index settings, and shard allocation. 
+ **Automated snapshots** are **only for cluster recovery**. You can use them to restore your domain in the event of red cluster status or data loss.
+ **Manual snapshots** are for **cluster recovery** or for **moving data from one cluster to another**.
+ Creating a custom endpoint for your Amazon OpenSearch Service domain makes it easier for you to refer to your OpenSearch and OpenSearch Dashboards URLs 
+ If you ever need to switch to a new domain, just update your DNS to point to the new URL and continue using the same endpoint as before.
# Indexing data
+ You can load streaming data into your Amazon OpenSearch Service domain from many different sources.
+ Some sources, like Amazon Kinesis Data Firehose and Amazon CloudWatch Logs, have built-in support for OpenSearch Service. 
+ Kinesis Data Firehose supports OpenSearch Service as a **delivery destination**.
+ You can load streaming data from CloudWatch Logs to your OpenSearch Service domain by using a **CloudWatch Logs subscription**.
+ Others, like Amazon S3, Amazon Kinesis Data Streams, and Amazon DynamoDB, use **AWS Lambda functions as event handlers**. The Lambda functions respond to new data by processing it and streaming it to your domain.
# Searching data
+ There are several common methods for searching documents in Amazon OpenSearch Service, including **URI searches and request body searches**.
+ You can **use SQL to query your Amazon OpenSearch Service**, rather than using the JSON-based OpenSearch query DSL
+ Piped Processing Language (PPL) is a query language that lets you use pipe (`|`) syntax to query data stored in Amazon OpenSearch Service. 
    + PPL requires either OpenSearch or Elasticsearch 7.9 or later.
+ Cross-cluster search in Amazon OpenSearch Service lets you **perform queries and aggregations across multiple connected domains**. It often makes more sense to use multiple smaller domains instead of a single large domain, especially when you're running different types of workloads.workload-specific domains enable you to perform the following tasks: 
    + Optimize each domain by choosing instance types for specific workloads.
    + Establish fault-isolation boundaries across workloads. This means that if one of your workloads fails, the fault is contained within that specific domain and doesn't impact your other workloads.
    + Scale more easily across domains.
+ **Learning to Rank** is an open-source OpenSearch plugin that lets you use **machine learning and behavioral data** to tune the relevance of documents. 
    + Learning to Rank requires OpenSearch or Elasticsearch 7.7 or later. 
+ With **asynchronous search** for Amazon OpenSearch Service you can submit a search query that gets **executed in the background**, monitor the progress of the request, and retrieve results at a later stage. You can **retrieve partial results** as they become available before the search has completed. After the search finishes, save the results for later retrieval and analysis. 
    + Asynchronous search requires OpenSearch 1.0 or later, or Elasticsearch 7.10 or later. 
# Managing indices
+ **UltraWarm** provides a **cost-effective way to store large amounts of read-only data** on Amazon OpenSearch Service.  
    + Rather than attached storage, UltraWarm nodes use **Amazon S3 and a sophisticated caching solution** to improve performance. 
    + UltraWarm is best-suited to **immutable data**, such as logs
+ **Cold storage** lets you store any amount of **infrequently accessed or historical data** on your Amazon OpenSearch Service domain and analyze it on demand, at a lower cost than other storage tiers. 
    + Cold storage is appropriate if you need to do **periodic research or forensic analysis on your older data**.
    + Similar to UltraWarm storage, cold storage is backed by Amazon S3
+ **Index State Management** (ISM) in Amazon OpenSearch Service lets you define custom management policies to automate routine tasks and apply them to indices and index patterns. 
    + A typical use case is to periodically delete old indices after a certain period of time.
+ **Index rollups** in Amazon OpenSearch Service let you **reduce storage costs by periodically rolling up old data into summarized indices**. 
    + You pick the fields that interest you and use an index rollup to create a new index with only those fields aggregated into coarser time buckets
+ **transform jobs** let you create a **different, summarized view of your data centered around certain fields**, so you can visualize or analyze the data in different ways.
+ **Cross-cluster replication** in Amazon OpenSearch Service lets you **replicate indices, mappings, and metadata from one OpenSearch Service domain to another**.  
    + Cross-cluster replication ensures **high availability** in the event of an outage,
    + and allows you to replicate data **across geographically** distant data centers to **reduce latency**.
+ **Remote reindex** lets you **copy indices from one Amazon OpenSearch Service cluster to another**. You can migrate indices from any OpenSearch Service domains or self-managed OpenSearch and Elasticsearch clusters.
# Monitoring data
+ Proactively monitor your data in Amazon OpenSearch Service with **alerting and anomaly detection**.
+ Set up alerts to receive notifications when your data exceeds certain thresholds.
+ Anomaly detection uses machine learning to automatically detect any outliers in your streaming data.
+ You can pair anomaly detection with alerting to ensure you're notified as soon as an anomaly is detected.
+ The default installation of OpenSearch Dashboard for Amazon OpenSearch Service includes the **Trace Analytics plugin**, which you can use to **analyze trace data from distributed applications**.
# Amazon OpenSearch Serverless
+ OpenSearch Service also offers a serverless option to help you run search and analytics workloads without having to worry about infrastructure.
+ With OpenSearch Serverless, you can run intermittent or unpredictable workloads. You do not have to think about cluster sizing, monitoring, and tuning.
+ Storage and compute are decoupled in OpenSearch Serverless, so each layer can scale independently.
+ The service monitors and manages compute resources such as CPU, disk utilization, memory, and hot shard state.
+ If these thresholds are breached, the service adjusts capacity without requiring you to perform any manual scaling.
# Reference
+ [Amazon OpenSearch Service](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/what-is.html)
+ [Getting Started with Amazon OpenSearch Service](https://explore.skillbuilder.aws/learn/course/15779/play/77664/getting-started-with-amazon-opensearch-service)
