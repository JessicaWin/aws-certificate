# Overview
+ Amazon Redshift is a fully managed, **petabyte-scale data warehouse service** in the cloud.
+ Regardless of the size of the data set, Amazon Redshift offers fast query performance using the same SQL-based tools and business intelligence applications that you use today
+ The Amazon Redshift service manages all of the work of setting up, operating, and scaling a data warehouse.
+ An Amazon Redshift data warehouse is an **enterprise-class relational database query and management system**.
+ Amazon Redshift achieves **efficient storage and optimum query performance** through a combination of massively parallel processing, **columnar data storage**, and very efficient, targeted data compression encoding schemes. 
# Data warehouse system architecture

![amazon_redshift](./images/amazon_redshift.png)
+ A **cluster** is composed of one or more **compute nodes**.
+ If a cluster is provisioned with two or more compute nodes, an additional **leader node** coordinates the compute nodes and handles external communication.
+ Your client application **interacts directly only with the leader node**. The compute nodes are transparent to external applications.
+ A compute node is partitioned into **slices**. Each slice is allocated a portion of the node's memory and disk space, where it processes a portion of the workload assigned to the node.
+ The leader node manages distributing data to the slices and apportions the workload for any queries or other database operations to the slices. The **slices then work in parallel** to complete the operation. 
+ When you create a table, you can optionally specify one column as the **distribution key**. When the table is loaded with data, the rows are distributed to the node slices according to the distribution key that is defined for a table. 
# Performance
+ Massively parallel processing 
    + Multiple compute nodes handle all query processing leading up to final result aggregation, with each core of each node **executing the same compiled query segments on portions of the entire data**.
    + Amazon Redshift distributes the rows of a table to the compute nodes so that the data can be processed in parallel.
+ **Columnar data storage** for database tables drastically **reduces the overall disk I/O** requirements and is an important factor in optimizing analytic query performance.+ **Data compression** reduces storage requirements, thereby reducing disk I/O, which improves query performance. 
    + The best way to enable data compression on table columns is by **allowing Amazon Redshift to apply optimal compression encodings** when you load the table with data
+ **The Amazon Redshift query execution engine** incorporates a query optimizer that is MPP-aware and also takes advantage of the columnar-oriented data storage. 
+ To reduce query execution time and improve system performance, Amazon Redshift **caches the results of certain types of queries in memory on the leader node**.
+ The leader node distributes fully optimized compiled code across all of the nodes of a cluster. 
# Amazon Redshift best practices
## best practices for designing tables
+ Choose the best sort key 
    + If recent data is queried most frequently, specify the timestamp column as the leading column for the sort key.
    + If you do frequent range filtering or equality filtering on one column, specify that column as the sort key
    + If you frequently join a table, specify the join column as both the sort key and the distribution key.
+ Choose the best distribution style 
    + Distribute the fact table and one dimension table on their common columns.
    + Choose the largest dimension based on the size of the filtered dataset.
    + Choose a column with high cardinality in the filtered result set.
    + Change some dimension tables to use ALL distribution.
+ Let COPY choose compression encodings 
    + You can specify compression encodings when you create a table, but in most cases, automatic compression produces the best results.
    + Automatic compression balances overall performance when choosing compression encodings.
+ Define primary key and foreign key constraints
+ Use the smallest possible column size
+ Use date/time data types for date columns
## best practices for loading data
+ Use a COPY command to load data
+ Use a single COPY command to load from multiple files
+ Split your load data into multiple files
+ Compress your data files
+ Verify data files before and after a load
+ If a COPY command is not an option and you require SQL inserts, use a multi-row insert whenever possible.
+ Use a bulk insert operation with a SELECT clause for high-performance data insertion
+ Load your data in sort key order to avoid needing to vacuum.
+ If you need to add a large quantity of data, load the data in sequential blocks according to sort order to eliminate the need to vacuum.
+ If your data has a fixed retention period, you can organize your data as a sequence of time-series tables. In such a sequence, each table is identical but contains data for different time ranges.You can easily remove old data simply by running a DROP TABLE command on the corresponding tables.
# Distribution styles
+ AUTO ——Amazon Redshift assigns an optimal distribution style based on the size of the table data.
+ EVEN-——The leader node distributes the rows across the slices in a round-robin fashion, regardless of the values in any particular column. 
+ KEY——The rows are distributed according to the values in one column.
+ ALL——A copy of the entire table is distributed to every node. 
# Reference
+ [Amazon Redshift](https://docs.aws.amazon.com/redshift/latest/dg/welcome.html)
+ [Getting Started with Amazon Redshift](https://explore.skillbuilder.aws/learn/course/13655/getting-started-with-amazon-redshift)
