# Overview
+ Amazon Neptune is a fast, reliable, fully managed **graph database service** that makes it easy to build and run applications that work with highly connected datasets.
+ The core of Neptune is a purpose-built, high-performance graph database engine. This engine is optimized for **storing billions of relationships and querying the graph with milliseconds latency**.
+ Neptune supports the popular property-graph query languages **Apache TinkerPop Gremlin and Neo4j's openCypher, and the W3C's RDF query language, SPARQL**.
+ Neptune powers graph use cases such as **recommendation engines, fraud detection, knowledge graphs, drug discovery, and network security**.
+ The Neptune database is highly available, **with read replicas, point-in-time recovery, continuous backup to Amazon S3, and replication across Availability Zones**.
# Neptune Analytics
+ Neptune Analytics; is an **analytics database engine** that complements Neptune database and that can quickly **analyze large amounts of graph data in memory to get insights and find trends**.
+ Neptune Analaytics is a solution for **quickly analyzing existing graph databases** or graph datasets stored in a data lake. It uses popular graph analytic algorithms and low-latency analytic queries.
# Key Service Components
+** Primary DB instance** – Supports **read and write** operations, and performs all of the data modifications to the cluster volume. **Each Neptune DB cluster has one primary DB instance** that is responsible for writing (that is, loading or modifying) graph database contents.
+ **Neptune replica** – Connects to the same storage volume as the primary DB instance and supports **only read** operations. Each Neptune DB cluster can have **up to 15 Neptune Replicas** in addition to the primary DB instance. This provides high availability by locating Neptune Replicas in separate Availability Zones and distribution load from reading clients.
+ **Cluster volume** – Neptune data is stored in the cluster volume, which is designed for reliability and high availability. A cluster volume consists of **copies of the data across multiple Availability Zones in a single AWS Region**. Because your data is **automatically replicated across Availability Zones**, it is highly durable, and there is little possibility of data loss.
# What exactly is a graph database?
+ Graph databases are optimized to **store and query the relationships between data items**.
+ **They store data items themselves as vertices of the graph, and the relationships between them as edges**.
+ Each edge has a type, and is directed from one vertex (the start) to another (the end).
+ Relationships can be called predicates as well as edges, and vertices are also sometimes referred to as nodes. In so-called property graphs, both vertices and edges can have additional properties associated with them too.
+ A graph consists of two primary constructs:
    + A vertex, or node
    + A relationship, or an edge
# Why use a graph database?
+ Whenever connections or relationships between entities are at the core of the data that you're trying to model, a graph database is your natural choice.
# What can you do with a graph database?
+ Knowledge graphs
+ Identity graphs
+ Fraud graphs
+ Social networking
+ Driving directions
+ Logistics   –   Graphs can help identify the most efficient way to use available shipping and distribution resources to meet customer requirements.
+ Diagnostics   –   Graphs can represent complex diagnostic trees that can be queried to identify the source of observed problems and failures.
+ Scientific research   –   With a graph database, you can build applications that store and navigate scientific data and even sensitive medical information using encryption at rest. 
+ Regulatory rules   –   You can store complex regulatory requirements as graphs, and query them to detect situations where they might apply to your day-to-day business operations.
+ Network topology and events
# Neptune DB instance type
+ Amazon Neptune offers a number of different instance sizes and families that offer different capabilities suited to different graph workloads.
+ The **Neptune Serverless** feature can **scale instance size dynamically** based on a workload's resource needs. Instead of calculating how many vCPUs are needed for your application, **Neptune Serverless** lets you set lower and upper limits on compute capacity (measured in Neptune Capacity Units) for the instances in your DB cluster. Workloads with varying utilization can be cost-optimized by using serverless rather than provsioned instances.
+ You can set up both provisioned and serverless instances in the same DB cluster to achieve an optimal cost-performance configuration.
# storage type for your Neptune DB cluster
+ Standard storage   –   Standard storage provides cost-effective database storage for applications with moderate to low I/O usage.
+ I/O–Optimized storage   –   With I/O–Optimized storage, you pay only for the storage and instances you are using. 
# Securing your data in Amazon Neptune
+ Using IAM policies to restrict access to a Neptune DB cluster
+ Using VPC security groups to restrict access to a Neptune DB cluster
+ Using IAM authentication to restrict access to a Neptune DB cluster
    + If you enable AWS Identity and Access Management (IAM) authentication in a Neptune DB cluster, anyone accessing the DB cluster must first be authenticated
# accessing your Neptune graph
+ Once you have created a Neptune DB cluster and set up connection to it, the next step is to communicate with it so as to load data, make queries and so forth. To do this, most people use the **curl or awscurl** command-line tools.
# Monitoring Amazon Neptune
+ Amazon CloudWatch – Amazon Neptune automatically sends metrics to CloudWatch and also supports CloudWatch Alarms.
+ AWS CloudTrail – Amazon Neptune supports API logging using CloudTrail.
+ Tagging – Use tags to add metadata to your Neptune resources and track usage based on tags. For more information, see Tagging Amazon Neptune Resources.
+ Audit log files – View, download, or watch database log files using the Neptune console.
+ Instance status – Check the health of a Neptune instance's graph database engine, find out what version of the engine is installed, and obtain other engine status information using the instance status API.
# Creating a Neptune global database
+ An Amazon Neptune **global database spans multiple AWS Regions**, enabling low-latency global reads and providing fast recovery in the rare case where an outage affects an entire AWS Region.
+ A Neptune global database consists of a primary DB cluster in one region, and **up to five secondary DB clusters in different regions**.
+ Writes can only occur in the primary region. **Secondary regions only support reads**. Each secondary region can have up to **16 reader instances**.
# When to use Neptune Analytics and when to use Neptune Database
+ Amazon Neptune makes it easy to work with graph data in the AWS Cloud. Amazon Neptune includes both Neptune Database and Neptune Analytics.
+ Neptune Database is **a serverless graph database** designed for optimal scalability and availability. It provides a solution for graph database workloads that need to scale to 100,000 queries per second, Multi-AZ high availability, and multi-Region deployments. You can use Neptune Database for social networking, fraud alerting, and Customer 360 applications.
+ Neptune Analytics is an **analytics database engine** that can quickly analyze large amounts of graph data in memory to get insights and find trends. Neptune Analytics is a solution for **quickly analyzing existing graph databases or graph datasets stored in a data lake**. It uses popular graph analytic algorithms and low-latency analytic queries.
+ You can use Neptune Analytics to analyze and query graphs in data science workflows that build targeted content recommendations, assist with fraud investigations, and detect network threats.
# Neptune lookup cache
+ The Neptune lookup cache can accelerate read queries
+ Amazon Neptune implements a lookup cache that uses the R5d instance's NVMe-based SSD to improve read performance for queries with frequent, repetitive lookups of property values or RDF literals.
+ The lookup cache temporarily stores these values in the NVMe SSD volume where they can be accessed rapidly.
+ The lookup cache is only available on an **R5d instance type**, where it is **automatically enabled by default**. 
# Managing Your Amazon Neptune Database
+ Using the Neptune **Blue/Green solution** to perform blue-green updates
+ You manage your database configuration in Amazon Neptune by using parameters in a parameter group. **Parameter groups** act as a container for engine configuration values that are applied to one or more DB instances.
    + DB parameter groups apply at the instance level and generally are associated with settings for the Neptune graph engine, such as the neptune_query_timeout parameter.
    + DB cluster parameter groups apply to every instance in the cluster and generally have broader settings. Every Neptune cluster is associated with a DB cluster parameter group. Every DB instance within that cluster inherits the engine configuration values contained in the DB cluster parameter group.
# Neptune streams
+ Neptune Streams logs every change to your graph as it happens, in the order that it is made, in a fully managed way. Once you enable Streams, Neptune takes care of availability, backup, security and expiry.
+ Neptune streams guarantees
    + Changes made by a transaction are immediately available for reading from both writer and readers as soon as the transaction is complete (aside from any normal replication lag in readers).
    + Change records appear strictly sequentially, in the order in which they occurred (this includes the changes made within a transaction).
    + The changes streams contain no duplicates. Each change is logged only once.
    + The changes streams are complete. No changes are lost or omitted.
    + The changes streams contain all the information needed to determine the complete state of the database itself at any point in time, provided that the starting state is known.
    + Streams can be turned on or off at any time.
# Full text search in Amazon Neptune
+ Neptune integrates with **Amazon OpenSearch Service** (OpenSearch Service) to support full-text search in both Gremlin and SPARQL queries.
+ You can use Neptune with an existing OpenSearch Service cluster that has been populated according to the Neptune data model for OpenSearch data. Or, you can create an OpenSearch Service domain linked with Neptune using an AWS CloudFormation stack.
# Amazon Neptune ML for machine learning on graphs
+ The Neptune ML feature makes it possible to build and train useful machine learning models on large graphs in hours instead of weeks.
+ To accomplish this, Neptune ML uses graph neural network (GNN) technology powered by Amazon SageMaker and the Deep Graph Library (DGL) (which is open-source)
# Neptune Data Model
+ S – Subject – source vertex (or edge identifier with regards to properties in LPG)
+ P – Predicate – property or edge label
+ O – Object – literal value for properties or target vertex for edges
+ G – Graph – named graph in RDF or edge ID in LPG
# What are the benefits of Neptune?
+ High performance
+ Open standards
+ Reliable and durable
+ Integration with AWS products
+ Milliseconds latency
+ Support for standards
+ Scalability
+ Fully managed
+ Highly secure
## Indices
+ Note that the OSGP index is not turned on by default because it is unnecessary for a majority of workloads, and it will add significant overhead to your Neptune cluster.
# Reference
+ [Amazon Neptune](https://docs.aws.amazon.com/neptune/latest/userguide/intro.html)
+ [Neptune Analytics](https://docs.aws.amazon.com/neptune-analytics/latest/userguide/what-is-neptune-analytics.html)
+ [Getting Started with Amazon Neptune](https://explore.skillbuilder.aws/learn/course/14165/getting-started-with-amazon-neptune)
+ [Data Modeling for Amazon Neptune](https://explore.skillbuilder.aws/learn/course/16133/data-modeling-for-amazon-neptune)
+ [Build with Amazon Neptune](https://explore.skillbuilder.aws/learn/course/16559/play/83759/build-with-amazon-neptune)
