# Overview
+ MemoryDB for Redis is a durable, in-memory database service that delivers **ultra-fast performance**. It is purpose-built for modern applications with **microservices architectures**.
+ MemoryDB is compatible with **Redis**
+ With MemoryDB, all of your data is stored in memory, which enables you to achieve **microsecond read and single-digit millisecond write latency and high throughput**.
+ MemoryDB also **stores data durably across multiple Availability Zones (AZs) using a Multi-AZ transactional log** to enable fast failover, database recovery, and node restarts.
+ Delivering both in-memory performance and Multi-AZ durability, MemoryDB can be used as a **high-performance primary database** for your microservices applications, **eliminating the need to separately manage both a cache and durable database**.
# Features of MemoryDB
+ **Strong consistency** for primary nodes and guaranteed eventual consistency for replica nodes.
+ **Microsecond read and single-digit millisecond write latencies** with up to **160 million TPS** per cluster.
+ **Flexible and friendly Redis data structures and APIs**. Easily build new applications or migrate existing Redis applications with almost no modification.
+ **Data durability using a Multi-AZ transactional log** providing fast database recovery and restart.
+ Multi-AZ availability with **automatic failover**, and detection of and recovery from node failures.
+ Easily **scale horizontally** by adding and removing nodes or vertically by moving to larger or smaller node types. You can **scale write throughput by adding shards and scale read throughput by adding replicas**.
+ **Read-after-write consistency** for primary nodes and guaranteed eventual consistency for replica nodes.
+ MemoryDB supports **encryption in transit, encryption at rest and authentication of users** via Authenticating users with Access Control Lists (ACLs).
+ **Automatic snapshots** in Amazon S3 with **retention for up to 35 days**.
+ Support for up to **500 nodes and more than 100 TB of storage** per cluster (with 1 replica per shard).
+ Encryption in-transit with TLS and encryption at-rest with AWS KMS keys.
+ User authentication and authorization with Redis Authenticating users with Access Control Lists (ACLs).
+ Support for AWS Graviton2 instance types.
+ Integration with other AWS services such as CloudWatch, Amazon VPC, CloudTrail, and Amazon SNS for monitoring, security, and notifications.
+ Fully-managed software patching and upgrades.
+ AWS Identity and Access Management (IAM) integration and tag-based access control for management APIs.
# MemoryDB core components
## Clusters
+ A cluster is **a collection of one or more nodes** serving a single dataset.
+ A MemoryDB dataset is **partitioned into shards**, and each shard has **a primary node and up to 5 optional replica nodes**.
+ A **primary node serves read and write requests**, while a **replica only serves read requests**.
+ A primary node can **failover to a replica node**, promoting that replica to the new primary node for that shard.
+ MemoryDB runs **Redis as its database engine**, and when you create a cluster, you specify the Redis version for your cluster. 
+ The computation and memory capacity of a cluster is determined by its node type. If your needs change over time, you can change node types. 
+ You run a cluster **on a virtual private cloud (VPC)** using the Amazon Virtual Private Cloud (Amazon VPC) service
## Nodes
+ A node is the **smallest building block of a MemoryDB deployment** and runs using an Amazon EC2 instance.
+ Each node runs the Redis version that was chosen when you created your cluster.
+ A node belongs to a shard which belongs to a cluster.+ If necessary, you can scale the nodes in a cluster up or down to a different type
+ Every node within a cluster is the **same node type**.
## Shards
+ A shard is a grouping of **one to 6 nodes**, with one serving as the primary write node and the other 5 serving as read replicas.
+ A MemoryDB cluster always has **at least one shard**.
+ MemoryDB clusters can have **up to 500 shards**, with your data partitioned across the shards. 
## Parameter groups
+ Parameter groups are an easy way to manage runtime settings for Redis on your cluster.
+ Parameters are used to control memory usage, item sizes, and more.
+ A MemoryDB parameter group is **a named collection of engine-specific parameters that you can apply to a cluster,** and all of the nodes in that cluster are configured in exactly the same way.
## Subnet Groups
+ A subnet group is a collection of subnets (typically private) that you can designate for your clusters running in an Amazon Virtual Private Cloud (VPC) environment.
## Access Control Lists
+ An Access control list is **a collection of one or more users**.
+ Access strings follow the Redis ACL rules to authorize user access to Redis commands and data.
## Users
+ A user has a user name and password, and is used to access data and issue commands on your MemoryDB cluster.
+ A user is a member of an Access Control List (ACL), which you can use to determine permissions for that user on MemoryDB clusters
# MemoryDB for Redis or ElastiCache for Redis
+ MemoryDB for Redis is **a durable, in-memory database** for workloads that require an ultra-fast, **primary database**
    + You should consider using MemoryDB if your workload requires a durable database that provides ultra-fast performance (microsecond read and single-digit millisecond write latency).
    + MemoryDB may also be a good fit for your use case if you want to build an application using Redis data structures and APIs with a primary, durable database. 
    + Finally, you should consider using MemoryDB to simplify your application architecture and lower costs by replacing usage of a database with a cache for durability and performance.
+ ElastiCache for Redis is a service that is commonly used to **cache data from other databases and data stores using Redis**.
    + You should consider ElastiCache for Redis for caching workloads where you want to **accelerate data access with your existing primary database or data store** (microsecond read and write performance).
    + You should also consider ElastiCache for Redis for use cases where you want to use the Redis data structures and APIs to access data stored in a primary database or data store.
# Accessing MemoryDB
+ Each MemoryDB cluster endpoint contains an address and a port.
+ This cluster endpoint supports the Redis Cluster protocol to allow clients to discover the specific roles, ip addresses and slots for each node in the cluster. 
+ You need to connect to the cluster endpoint to **discover node endpoints** using **cluster nodes or cluster slots** command. After discovering the right node for a key, you can connect directly to the node for read/write requests. A Redis client can use the cluster endpoint to automatically connect to the correct node.
# MemoryDB security
+ To control who can perform management actions on MemoryDB clusters and nodes, you use **AWS Identity and Access Management (IAM)** 
+ To control access levels to clusters, you create users with specified permissions and assign them to the **Access Control Lists (ACL)**. The ACL, in turn, is then associated with one or more clusters.
+ MemoryDB clusters must be created in a virtual private cloud (VPC) based on the Amazon VPC service. To control which devices and Amazon EC2 instances can open connections to the endpoint and port of the node for MemoryDB clusters in a VPC, you use **a VPC security group**. In addition, **firewall rules** at your company can control whether devices running at your company can open connections to a MemoryDB cluster.
# Scaling MemoryDB clusters
## Offline resharding and shard rebalancing for MemoryDB
+ The main advantage you get from offline shard reconfiguration is that you can do more than merely add or remove shards from your cluster.
+ When you reshard offline, in addition to changing the number of shards in your cluster, you can do the following:
    + Change the node type of your cluster.
    + Upgrade to a newer engine version.
+ To reconfigure your shards MemoryDB cluster offline
    + Create a manual snapshot of your existing MemoryDB cluster.
    + Create a new cluster by restoring from the snapshot.
    + Update the endpoints in your application to the new cluster's endpoints. 
## Online resharding and shard rebalancing for MemoryDB
+ By using online resharding and shard rebalancing with MemoryDB, you can scale your MemoryDB dynamically with no downtime. This approach means that your cluster can continue to serve requests even while scaling or rebalancing is in process.
+ You can do the following:
    + **Scale out** – Increase read and write capacity by **adding shards** to your MemoryDB cluster.
        + If you add one or more shards to your cluster, the number of nodes in each new shard is the same as the number of nodes in the smallest of the existing shards.
    + **Scale in** – Reduce read and write capacity, and thereby costs, by **removing shards** from your MemoryDB cluster.
## Online vertical scaling by modifying node type
+ By using online vertical scaling with MemoryDB, you can scale your cluster dynamically with minimal downtime. This allows your cluster to serve requests even while scaling.
+ **Scale up** – Increase read and write capacity by **adjusting the node type** of your MemoryDB cluster to use a larger node type.
    + MemoryDB **dynamically resizes your cluster while remaining online** and serving requests.
+ **Scale down** – Reduce read and write capacity by **adjusting the node type down** to use a smaller node. Again, MemoryDB dynamically resizes your cluster while remaining online and serving requests. In this case, you reduce costs by downsizing the node.
# What are the benefits of MemoryDB?
+ Redis compatible
+ Ultrafast performance
+ Fully managed
+ Scalable
+ Durability and high availability
# How much does MemoryDB cost?
+ You are charged for the **instance-hours per node** (primary nodes and replicas), **snapshot storage, and volume of data** written to your cluster in gigabytes (GB). 
# What are typical use cases for MemoryDB?
+ Use MemoryDB as a distributed database to store and retrieve data with low latency and high throughput for key-value use cases.
+ Store and retrieve in-memory data structures durably using key-value access and flexible Redis commands.
+ Use MemoryDB as a key-value database to run high-performance online transaction processing (OLTP) workloads.  
+ Use Redis hash to model entities into object structures.
+ Use flexible Redis commands to modify and retrieve your data with ultrafast performance.
+ **data streaming**: Use MemoryDB to ingest events asynchronously from your applications. The events are stored durably and consistently. Use the Redis Streams data structure to capture high-velocity events, and scale reads using consumer groups. 
+ Use MemoryDB as an in-memory key-value store with appropriate key expiration strategies to durably store and manage **session data** for microsecond read responses.
+ **Leaderboards** need low latency and high concurrency data stores to process changing scores and to update ranks in real time. Use MemoryDB as an in-memory database with unique data structures to manage ranking with low latency. 
+ Use MemoryDB as an **in-memory message queue** with Redis Lists
# How can you deploy MemoryDB with CloudFormation?
+ AWS::MemoryDB::Cluster
+ AWS::MemoryDB::ParameterGroup
+ AWS::MemoryDB::SubnetGroup
+ AWS::MemoryDB::User
+ AWS::MemoryDB::ACL
# Reference
+ [Amazon MemoryDB for Redis](https://docs.aws.amazon.com/memorydb/latest/devguide/what-is-memorydb-for-redis.html)
+ [Getting Started with Amazon MemoryDB for Redis](https://explore.skillbuilder.aws/learn/course/10067/getting-started-with-amazon-memorydb-for-redis)
+ [Build with Amazon MemoryDB for Redis](https://explore.skillbuilder.aws/learn/course/14997/build-with-amazon-memorydb-for-redis)