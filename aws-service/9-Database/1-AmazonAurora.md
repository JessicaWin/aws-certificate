# Overview
+ Amazon Aurora (Aurora) is a fully managed relational database engine that's compatible with **MySQL and PostgreSQL**.
+ With some workloads, Aurora can **deliver up to five times the throughput of MySQL and up to three times the throughput of PostgreSQL** without requiring changes to most of your existing applications.
+ Aurora includes a **high-performance storage subsystem**.The underlying storage **grows automatically** as needed. Aurora also **automates and standardizes database clustering and replication**
# Amazon Aurora DB clusters
+ An Amazon Aurora *DB cluster* consists of **one or more DB instances and a cluster volume** that manages the data for those DB instances. 
+ An Aurora *cluster volume* is a **virtual database storage volume** that **spans multiple Availability Zones**, with each Availability Zone having a copy of the DB cluster data. 
+ Two types of DB instances make up an Aurora DB cluster: 
    + **Primary DB instance** – Supports read and write operations, and **performs all of the data modifications to the cluster volume**. Each Aurora DB cluster has one primary DB instance.
    + **Aurora Replica** – Connects to the same storage volume as the primary DB instance and **supports only read operations**. 
+ Each Aurora DB cluster can have **up to 15 Aurora Replicas** in addition to the primary DB instance.
+ Maintain high availability by locating Aurora Replicas in **separate Availability Zones**.
+ Aurora Replicas can also **offload read workloads from the primary DB instance**

![amazon_aurora](./images/amazon_aurora.png)
+ Each Aurora DB cluster hosts copies of its storage in **three separate AZs** 
+ Every DB instance in the cluster **must be in one of these three AZs**
+ If an AWS Region has fewer than three AZs, Aurora isn't available in that Region.
# Amazon Aurora connection management
+ An endpoint is represented as an Aurora-specific URL that **contains a host address and a port**. 
+ When you connect to an Aurora cluster, the host name and port that you specify point to an intermediate handler called an *endpoint*.
+ Aurora uses the endpoint mechanism to abstract these connections.
+ **Cluster endpoint**
    + A *cluster endpoint* (or *writer endpoint*) for an Aurora DB cluster **connects to the current primary DB instance** for that DB cluster.
    + This endpoint is the only one that can **perform write operations** such as DDL statements. 
    + Each Aurora DB cluster has **one cluster endpoint and one primary DB instance**.
    + You use the cluster endpoint **for all write operations** on the DB cluster, including inserts, updates, deletes, and DDL changes. You can also use the cluster endpoint for read operations, such as queries.
    + If the current primary DB instance of a DB cluster fails, Aurora automatically fails over to a new primary DB instance. During a failover, the DB cluster continues to serve connection requests to the cluster endpoint from the new primary DB instance, with minimal interruption of service.
+ **Reader endpoint**
    + A *reader endpoint* for an Aurora DB cluster **provides load-balancing support** for **read-only connections** to the DB cluster. 
    + The reader endpoint load-balances connections to available Aurora Replicas in an Aurora DB cluster.
    + It doesn't load-balance individual queries.
    + If you want to load-balance each query to distribute the read workload for a DB cluster, open a new connection to the reader endpoint for each query.
    + Use the reader endpoint for read operations, such as queries.
    + Each Aurora DB cluster has **one reader endpoint**.
    + If the cluster only contains a primary instance and no Aurora Replicas, the reader endpoint connects to the primary instance.
+ **Custom endpoint**
    + A *custom endpoint* for an Aurora cluster represents a set of DB instances that you choose.
    + When you connect to the endpoint, Aurora performs load balancing and chooses one of the instances in the group to handle the connection.
    + You define which instances this endpoint refers to, and you decide what purpose the endpoint serves.
    + An Aurora DB cluster has no custom endpoints until you create one. You can create up to five custom endpoints for each provisioned Aurora cluster. You **can't use custom endpoints for Aurora Serverless clusters**.
    + With custom endpoints, you can predict the capacity of the DB instance used for each connection. When you use custom endpoints, you typically don't use the reader endpoint for that cluster.
+ **Instance endpoint**
    + An *instance endpoint* connects to **a specific DB instance** within an Aurora cluster.
    + Each DB instance in a DB cluster has its own unique instance endpoint. 
    + The instance endpoint provides direct control over connections to the DB cluster, for scenarios where using the cluster endpoint or reader endpoint might not be appropriate.
# Aurora DB instance classes
+ The DB instance class determines the computation and memory capacity of an Amazon Aurora DB instance. The DB instance class that you need depends on your processing power and memory requirements.
+ Aurora Serverless v2
+ Memory-optimized
+ Burstable-performance
+ Optimized Reads
# Amazon Aurora storage and reliability
+ Aurora data is stored in the *cluster volume*, which is a single, virtual volume that uses solid state drives (SSDs).
+ A cluster volume consists of copies of the data **across three Availability Zones** in a single AWS Region.
+ The Aurora cluster volume contains all your user data, schema objects, and internal metadata such as the system tables and the binary log
+ The Aurora shared storage architecture **makes your data independent from the DB instances** in the cluster.
+ Aurora cluster volumes automatically grow as the amount of data in your database increases. The maximum size for an Aurora cluster volume is **128 tebibytes (TiB) or 64 TiB**, depending on the DB engine version. 
+ Aurora is designed to be reliable, durable, and fault tolerant. 
+ Storage auto-repair： Aurora automatically detects failures in the disk volumes that make up the cluster volume. When a segment of a disk volume fails, Aurora immediately repairs the segment. As a result, Aurora avoids data loss and **reduces the need to perform a point-in-time restore** to recover from a disk failure
+ Survivable cache warming： Aurora "warms" the buffer pool cache when a database starts up after it has been shut down or restarted after a failure. That is, Aurora preloads the buffer pool with the pages for known common queries that are stored in an in-memory page cache. 
+ Crash recovery：Aurora is designed to recover from a crash almost instantaneously and continue to serve your application data without the binary log. 
+ The amount of binary log data affects recovery time. If there is more data logged in the binary logs, the DB instance must process more data during recovery, which increases recovery time.
+ If you don't need the binary log for external replication (or an external binary log stream), we recommend that you set the `binlog_format` parameter to `OFF` to disable binary logging.
## Storage configurations for Amazon Aurora DB clusters
+ Aurora I/O-Optimized – Improved price performance and predictability for I/O-intensive applications. You pay only for the usage and storage of your DB clusters, with no additional charges for read and write I/O operations.
    + Aurora I/O-Optimized is the best choice when your I/O spending is 25% or more of your total Aurora database spending.
    + You can choose Aurora I/O-Optimized when you create or modify a DB cluster with a DB engine version that supports the Aurora I/O-Optimized cluster configuration. You can switch from Aurora I/O-Optimized to Aurora Standard at any time.
+ Aurora Standard – Cost-effective pricing for many applications with moderate I/O usage. In addition to the usage and storage of your DB clusters, you also pay a standard rate per 1 million requests for I/O operations.
    + Aurora Standard is the best choice when your I/O spending is less than 25% of your total Aurora database spending.
    + You can switch from Aurora Standard to Aurora I/O-Optimized once every 30 days.
# High availability for Amazon Aurora
+ High availability for **Aurora data**：When data is written to the primary DB instance, Aurora **synchronously replicates the data across Availability Zones to six storage nodes associated with your cluster volume**. Doing so provides data redundancy, eliminates I/O freezes, and minimizes latency spikes during system backups. 
+ High availability for **Aurora DB instances**： For a cluster using single-master replication, after you create the primary instance, you can create up to **15 read-only Aurora Replicas**. 
+ High availability **across AWS Regions with Aurora global databases**：Each Aurora global database **spans multiple AWS Regions**, enabling low latency global reads and disaster recovery from outages across an AWS Region. Aurora automatically handles replicating all data and updates from the primary AWS Region to each of the secondary Regions
+ Fault tolerance for an Aurora DB cluster：The cluster volume spans multiple Availability Zones in a single AWS Region, and each Availability Zone contains a copy of the cluster volume data. This functionality means that your DB cluster can tolerate a failure of an Availability Zone without any loss of data and only a brief interruption of service.
+ With **RDS Proxy**, you can build applications that can transparently tolerate database failures without needing to write complex failure handling code. The proxy automatically routes traffic to a new database instance while preserving application connections. It also bypasses Domain Name System (DNS) caches to reduce failover times by up to 66% for Aurora Multi-AZ databases.
# Replication with Amazon Aurora
+ Each Aurora DB cluster has built-in replication between multiple DB instances in the same cluster.
+ You can also set up replication with your Aurora cluster as the source or the target.
## Aurora Replicas
+ When you create a second, third, and so on DB instance in an Aurora provisioned DB cluster, Aurora **automatically sets up replication from the writer DB instance to all the other DB instances**. These other DB instances are read-only and are **known as Aurora Replicas**. 
+ Aurora Replicas have two main purposes.
    + You can issue queries to them to **scale the read operations for your applicatio**n. You typically do so by connecting to the reader endpoint of the cluster. That way, Aurora can spread the load for read-only connections across as many Aurora Replicas as you have in the cluster.
    + Aurora Replicas also help to **increase availability**. If the writer instance in a cluster becomes unavailable, Aurora automatically promotes one of the reader instances to take its place as the new writer.
+ An Aurora DB cluster can contain up to **15 Aurora Replicas**. The Aurora Replicas can be distributed across the Availability Zones that a DB cluster spans within an AWS Region.
+ To increase availability, you can use Aurora Replicas as **failover targets**. That is, if the primary instance fails, an Aurora Replica is promoted to the primary instance. 
    + Promoting an Aurora Replica by failover is **much faster than recreating the primary instance**. 
+ For high-availability scenarios, we recommend that you create one or more Aurora Replicas. These should be of the **same DB instance class as the primary instance and in different Availability Zones for your Aurora DB cluster**.
## Replication with Aurora MySQL
+ Aurora MySQL DB clusters in different AWS Regions.
    + You can replicate data across multiple Regions by using an Aurora global database. 
    + You can create an Aurora read replica of an Aurora MySQL DB cluster in a different AWS Region, by using MySQL binary log (binlog) replication. Each cluster can have up to five read replicas created this way, each in a different Region.
+ Two Aurora MySQL DB clusters in the same Region, by using MySQL binary log (binlog) replication.
+ An RDS for MySQL DB instance as the source of data and an Aurora MySQL DB cluster, by creating an Aurora read replica of an RDS for MySQL DB instance. Typically, you use this approach for migration to Aurora MySQL, rather than for ongoing replication.
## Replication with Aurora PostgreSQL
+ An Aurora primary DB cluster in one Region and up to five read-only secondary DB clusters in different Regions by using an Aurora global database. **Aurora PostgreSQL doesn't support cross-Region Aurora Replicas**. However, you can use Aurora global database to scale your Aurora PostgreSQL DB cluster's read capabilities to more than one AWS Region and to meet availability goals.
+ Two Aurora PostgreSQL DB clusters in the same Region, by using PostgreSQL's logical replication feature.
+ An RDS for PostgreSQL DB instance as the source of data and an Aurora PostgreSQL DB cluster, by creating an Aurora read replica of an RDS for PostgreSQL DB instance. Typically, you use this approach for migration to Aurora PostgreSQL, rather than for ongoing replication.
+ Logical replication with Aurora ： Aurora supports logical replication to **publish changes to other PostgreSQL databases or replication clients** starting with version 10.6 and later. 
    + Logical replication works for replicating changes from PostgreSQL instances running on premises or self managed on Amazon Elastic Compute Cloud (Amazon EC2). It also works for upgrades in PostgreSQL versions.
# DB instance billing for Aurora
+ DB instance hours (per hour)
+ Storage (per GiB per month)
+ Input/output (I/O) requests (per 1 million requests)
+ Backup storage (per GiB per month)
+ Data transfer (per GB)
# Configuring your Amazon Aurora DB cluster
+ You can only create an Amazon Aurora DB cluster in a virtual private cloud (VPC) based on the Amazon VPC service, in an AWS Region that has **at least two Availability Zones**.
##  Using Amazon Aurora global databases
+ Amazon Aurora global databases **span multiple AWS Regions,** enabling low latency global reads and providing fast recovery from the rare outage that might affect an entire AWS Region.
+ An Aurora global database has **a primary DB cluster in one Region**, and **up to five secondary DB clusters in different Regions**.
+ You issue **write operations directly to the primary DB cluster** in the primary AWS Region. Aurora replicates data to the secondary AWS Regions using dedicated infrastructure, **with latency typically under a second**.

![amazon_aurora_global_database](./images/amazon_aurora_global_database.png)
+ You can **scale up each secondary cluster independently**, by adding one or more Aurora Replicas (read-only Aurora DB instances) to serve read-only workloads.
+ Aurora global database uses the **cluster storage volume** and not the database engine **for replication**
+ By using Aurora global databases, you can get the following advantages: 
    + Global reads with local latency
    + Scalable secondary Aurora DB clusters
    + Fast replication from primary to secondary Aurora DB clusters
    + Recovery from Region-wide outages
# Managing an Amazon Aurora DB cluster
+ Stop a cluster 
    + You can't stop a cluster that's part of an Aurora global database, or a multi-master cluster.
    + You can't stop a DB cluster that acts as the replication target for data from another DB cluster, or acts as the replication master and transmits data to another cluster.
    + You can't stop an Aurora serverless cluster.+ You can't stop an individual Aurora DB instance.
+ Adding Aurora Replicas 
    + You can't create an Aurora Replica for an Aurora Serverless v1 DB cluster. 
    + You can't create Aurora Replicas for an Aurora multi-master cluster. By design, an Aurora multi-master cluster has read-write DB instances only.
    + Aurora **PostgreSQL–based DB clusters can have only one Aurora Replica**
    + Aurora PostgreSQL–based DB clusters can't have Aurora Replicas in different AWS Regions. In other words, Aurora PostgreSQL doesn't support cross-region Aurora Replicas.
+ By using Aurora cloning, you can **quickly and cost-effectively create a new cluster** that **uses the same Aurora cluster volume** and has the same data as the original. 
    + Aurora cloning works at the storage layer of an Aurora DB cluster.
    + It uses a **copy-on-write protocol** that's both fast and space-efficient in terms of the underlying durable media supporting the Aurora storage volume.
    + **Avoid using clones for long-term purposes**, especially those involving many writes by the source Aurora DB cluster and the clone.
    + By using AWS Resource Access Manager (AWS RAM) with Amazon Aurora, you can share Aurora DB clusters and clones that belong to your AWS account **with another AWS account or organization**. 
    + To **allow other AWS accounts to clone a cluster that you own**, use AWS RAM to set the sharing permission.
+ To meet your connectivity and workload requirements, **Aurora Auto Scaling** dynamically adjusts the number of Aurora Replicas provisioned for an Aurora DB cluster using single-master replication.  
    +  target-tracking scaling policy
# Backing up and restoring an Amazon Aurora DB cluster
+ Aurora **backs up your cluster volume automatically** and retains restore data for the length of the **backup retention period**. 
+ You can specify a backup retention period, from **1 to 35 days**
+  Aurora backups are stored in **Amazon S3**.
+ Automated backups occur daily during the preferred **backup window**. 
+ Aurora backups are **continuous and incremental**, but the backup window is used to create a daily system backup that is preserved within the backup retention period. You can **copy it to preserve it outside of the retention period**.
+ You can recover your data by creating a new Aurora DB cluster **from the backup data** that Aurora retains, or **from a DB cluster snapshot** that you have saved. 
# Best practices with Amazon Aurora
+ Monitor your memory, CPU, and storage usage. 
+ If your client application is caching the Domain Name Service (DNS) data of your DB instances, set a time-to-live (TTL) value of less than 30 seconds. 
+ Test failover for your DB cluster to understand how long the process takes for your use case.
+ We recommend that you try out DB parameter group and DB cluster parameter group changes on a test DB cluster before applying parameter group changes to your production DB cluster. 
# Amazon Aurora security
+ To control who can **perform Amazon RDS management actions** on Aurora DB clusters and DB instances, you use **AWS Identity and Access Management (IAM)**. 
+ Aurora DB clusters must be created in a virtual private cloud (VPC) based on the Amazon VPC service. To control which devices and Amazon EC2 instances can open connections to the endpoint and port of the DB instance for Aurora DB clusters in a VPC, you use a **VPC security group**.  You can make these endpoint and port connections using **Transport Layer Security (TLS)/Secure Sockets Layer (SSL)**. In addition, **firewall rules** at your company can control whether devices running at your company can open connections to a DB instance. 
+ To authenticate logins and permissions for an Amazon Aurora DB cluster, you can take either of the following approaches, or a combination of them.
    + You can take the same approach as with a stand-alone DB instance of MySQL or PostgreSQL.
    + You can use IAM database authentication.
    + You can use Kerberos authentication for Aurora PostgreSQL and Aurora MySQL.
+ Amazon Aurora DB clusters support **Secure Sockets Layer (SSL) connections** from applications using the same process and public key as Amazon RDS DB instances.
# Monitoring metrics in an Amazon Aurora cluster
+ Viewing and responding to **Amazon Aurora recommendations**
+ Viewing metrics in the **Amazon RDS console**
+ Viewing combined metrics in the **Amazon RDS console**
+ Monitoring Amazon Aurora metrics with **Amazon CloudWatch**
+ Monitoring DB load with **Performance Insights on Amazon Aurora**
+ Analyzing performance anomalies with **Amazon DevOps Guru for Amazon RDS**
+ Monitoring threats with **Amazon GuardDuty RDS Protection**
+ Monitoring OS metrics with **Enhanced Monitoring**
# Monitoring events, logs, and streams in an Amazon Aurora DB cluster
+ Viewing logs, events, and streams in the Amazon RDS console
+ Monitoring Amazon Aurora events: Event Bridge
+ Monitoring Amazon Aurora log files
+ Monitoring Amazon Aurora API calls in AWS CloudTrail
+ Monitoring Amazon Aurora with Database Activity Streams
# Working with Amazon Aurora MySQL
## Working with parallel query for Amazon Aurora MySQL
+ **Aurora MySQL parallel query** is an optimization that parallelizes some of the I/O and computation involved in processing data-intensive queries.
    + This feature uses a special processing path for certain **data-intensive queries**, taking advantage of the Aurora shared storage architecture.
    + Parallel query works best with Aurora MySQL DB clusters that have **tables with millions of rows and analytic queries that take minutes or hours to complete**.
+ Benefits of parallel query include the following:
    + **Improved I/O performance**, due to parallelizing physical read requests across multiple storage nodes.
    + **Reduced network traffic**. Aurora doesn't transmit entire data pages from storage nodes to the head node and then filter out unnecessary rows and columns afterward. Instead, Aurora **transmits compact tuples containing only the column values needed for the result set**.
    + **Reduced CPU usage** on the head node, due to pushing down function processing, row filtering, and column projection for the WHERE clause.
    + **Reduced memory pressure on the buffer pool**. The pages processed by the parallel query aren't added to the buffer pool. This approach reduces the chance of a data-intensive scan evicting frequently used data from the buffer pool.
    + **Potentially reduced data duplication** in your extract, transform, load (ETL) pipeline, by making it practical to perform long-running analytic queries on existing data.
## Using Advanced Auditing with an Amazon Aurora MySQL DB cluster
+ You can use the high-performance Advanced Auditing feature in Amazon Aurora MySQL to audit database activity.
+ To do so, you enable the collection of audit logs by setting several DB cluster parameters.
+ When Advanced Auditing is enabled, you can use it to log any combination of supported events.
# Using Amazon Aurora global databases
+ Amazon Aurora global databases **span multiple AWS Regions**, enabling low latency global reads and providing fast recovery from the rare outage that might affect an entire AWS Region.
+ An Aurora global database has **a primary DB cluster in one Region, and up to five secondary DB clusters in different Regions**.

![amazon_aurora_global_databases_conceptual_illo](./images/amazon_aurora_global_databases_conceptual_illo.png)
+ You can **scale up each secondary cluster independently**, by adding one or more Aurora Replicas (read-only Aurora DB instances) to serve read-only workloads.
+ **Only the primary cluster performs write operations**. Clients that perform write operations connect to the DB cluster endpoint of the primary DB cluster.
+ Aurora global databases are designed for **applications with a worldwide footprint**. The read-only secondary DB clusters (AWS Regions) allow you to **support read operations closer to application users**.
+ By using the **write forwarding feature**, you can also configure an Aurora global database so that **secondary clusters send data to the primary**.
    + You can reduce the number of endpoints that you need to manage for applications running on your Aurora global database, by using write forwarding. With write forwarding enabled, **secondary clusters in an Aurora global database forward SQL statements that perform write operations to the primary cluster**. The primary cluster updates the source and then propagates resulting changes back to all secondary AWS Regions.
+ An Aurora global database supports two different operations for **changing the Region of your primary DB cluster**, depending on the scenario: **global database switchover and global database failover**.
    + For planned operational procedures such as Regional rotation, use global database **switchover** (previously called "managed planned failover"). With this feature, you can relocate the primary cluster of a healthy Aurora global database to one of its secondary Regions **with no data loss**.
    + To recover your Aurora global database after an outage in the primary Region, use global database failover. With this feature, you fail over your primary DB cluster to another Region (cross-Region failover). 
## Advantages of Amazon Aurora global databases
+ **Global reads with local latency** – If you have offices around the world, you can use an Aurora global database to keep your main sources of information updated in the primary AWS Region. Offices in your other Regions can access the information in their own Region, with local latency.
+ **Scalable secondary Aurora DB clusters** – You can scale your secondary clusters by adding more read-only instances (Aurora Replicas) to a secondary AWS Region. The secondary cluster is read-only, so it can support up to 16 read-only Aurora Replica instances rather than the usual limit of 15 for a single Aurora cluster.
+ **Fast replication from primary to secondary Aurora DB clusters** – The replication performed by an Aurora global database has little performance impact on the primary DB cluster. The resources of the DB instances are fully devoted to serve application read and write workloads.
+ **Recovery from Region-wide outages** – The secondary clusters allow you to make an Aurora global database available in a new primary AWS Region more quickly (lower RTO) and with less data loss (lower RPO) than traditional replication solutions.
# Using Amazon RDS Proxy for Aurora
+ By using **Amazon RDS Proxy**, you can allow your applications to **pool and share database connections** to improve their ability to scale.
+ RDS Proxy makes applications more resilient to database failures by **automatically connecting to a standby DB instance while preserving application connections**.
+ By using RDS Proxy, you can also enforce AWS Identity and Access Management (IAM) authentication for databases, and securely store credentials in AWS
+ Using RDS Proxy, you can **handle unpredictable surges in database traffic**. Otherwise, these surges might cause issues due to oversubscribing connections or new connections being created at a fast rate
+ RDS Proxy establishes a **database connection pool and reuses connections** in this pool. This approach avoids the memory and CPU overhead of opening a new database connection each time.
+ To protect a database against oversubscription, you can **control the number of database connections that are created**.
+ RDS Proxy **queues or throttles application connections** that can't be served immediately from the connection pool. Although latencies might increase, your application can continue to scale without abruptly failing or overwhelming the database.
+ If connection requests exceed the limits you specify, RDS Proxy **rejects application connections (that is, it sheds load)**.
## Quotas and limitations for RDS Proxy
+ You can have up to **20 proxies for each AWS account ID**.
+ Each proxy can have up to 200 associated Secrets Manager secrets. Thus, **each proxy can connect to with up to 200 different user accounts** at any given time.
+ Each proxy has a default endpoint. You can also add **up to 20 proxy endpoints** for each proxy. You can create, view, modify, and delete these endpoints.
+ In an Aurora cluster, all of the connections using the **default proxy endpoint are handled by the Aurora writer instance**. To perform load balancing for read-intensive workloads, you can **create a read-only endpoint for a proxy**. That endpoint passes connections to the reader endpoint of the cluster. That way, your proxy connections can take advantage of Aurora read scalability.
+ You can use RDS Proxy with Aurora Serverless v2 clusters, but not with Aurora Serverless v1 clusters.
+ Your RDS Proxy must be in the same virtual private cloud (VPC) as the database. The proxy can't be publicly accessible, although the database can be.
+ You can't use RDS Proxy with a VPC that has its tenancy set to dedicated.
+ If you use RDS Proxy with an Aurora DB cluster that has IAM authentication enabled, check user authentication. Users who connect through a proxy must **authenticate through sign-in credentials**.
+ You can't use RDS Proxy with custom DNS when using SSL hostname validation.
+ Each proxy can be **associated with a single target DB cluster**. However, you can **associate multiple proxies with the same DB cluster**.
+ Any statement with a text size greater than 16 KB causes the proxy to pin the session to the current connection.
+ Certain Regions have Availability-Zone (AZ) restrictions to consider while creating your proxy. US East (N. Virginia) Region does not support RDS Proxy in the use1-az3 Availability Zone. US West (N. California) Region does not support RDS Proxy in the usw1-az2 Availability Zone. When selecting subnets while creating your proxy, make sure that you don't select subnets in the Availability Zones mentioned above.
## Planning where to use RDS Proxy
+ Any DB cluster that encounters "too many connections" errors is a good candidate for associating with a proxy. 
+ For DB clusters that use smaller AWS instance classes, such as T2 or T3, using a proxy can help avoid out-of-memory conditions. 
+ You can monitor certain Amazon CloudWatch metrics to determine whether a DB cluster is approaching certain types of limit. These limits are for the number of connections and the memory associated with connection management.
+ AWS Lambda functions can also be good candidates for using a proxy. 
+ Applications that typically open and close large numbers of database connections and don't have built-in connection pooling mechanisms are good candidates for using a proxy.
+ Applications that keep a large number of connections open for long periods are typically good candidates for using a proxy.
## RDS Proxy security
+ You store the database credentials used by RDS Proxy in **AWS Secrets Manager**.
+ Each database user for the Aurora DB cluster accessed by a proxy must have a corresponding secret in Secrets Manager.
+ You can also **set up IAM authentication for users of RDS Proxy**. By doing so, you can enforce IAM authentication for database access even if the databases use native password authentication. 
# Using RDS Data API
+ By using **RDS Data API (Data API)**, you can work with a **web-services interface to your Aurora DB cluster**.
+ Data API **doesn't require a persistent connection** to the DB cluster. Instead, it provides **a secure HTTP endpoint and integration with AWS SDKs**. You can use the endpoint to run SQL statements **without managing connections**.
+ All calls to Data API are **synchronous**. By default, a call **times out** if it's not finished processing **within 45 seconds**. However, you can continue running a SQL statement if the call times out by using the **continueAfterTimeout** parameter. 
+ Users **don't need to pass credentials** with calls to Data API, because Data API **uses database credentials stored in AWS Secrets Manager**. To store credentials in Secrets Manager, users must be **granted the appropriate permissions to use Secrets Manager, and also Data API**. 
+ You can also use Data API to integrate Amazon Aurora with other AWS applications such as AWS Lambda, AWS AppSync, and AWS Cloud9. 
+ You can enable Data API when you create the Aurora DB cluster. You can also modify the configuration later.
+ RDS Data API (Data API) is **integrated with AWS CloudTrail**, a service that provides a record of actions taken by a user, role, or an AWS service in Data API. CloudTrail captures all API calls for Data API as events, including calls from the Amazon RDS console and from code calls to Data API operations. 
# Reference
+ [Amazon Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html)
+ [Amazon Aurora MySQL Basics](https://explore.skillbuilder.aws/learn/course/86/amazon-aurora-mysql-basics)
+ [Amazon Aurora Service Primer](https://explore.skillbuilder.aws/learn/course/394/amazon-aurora-service-primer)
+ [Amazon Aurora MySQL Migration](https://explore.skillbuilder.aws/learn/course/438/amazon-aurora-mysql-migration)
+ [Amazon Aurora PostgreSQL and Amazon RDS PostgreSQL](https://explore.skillbuilder.aws/learn/course/7872/amazon-aurora-postgresql-and-amazon-rds-postgresql)
+ [Amazon Aurora MySQL and Amazon RDS MySQL](https://explore.skillbuilder.aws/learn/course/8033/amazon-aurora-mysql-and-amazon-rds-mysql)
