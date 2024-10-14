# Amazon Kinesis Data Analytics for SQL Applications
+ With Amazon Kinesis Data Analytics for SQL Applications, you can **process and analyze streaming data using standard SQL**.
+ The service enables you to quickly author and run powerful SQL code against streaming sources to perform **time series analytics, feed real-time dashboards, and create real-time metrics**.
+ Kinesis Data Analytics supports Amazon Kinesis Data Firehose (Amazon S3, Amazon Redshift, Amazon OpenSearch Service, and Splunk), AWS Lambda, and Amazon Kinesis Data Streams as destinations.
+ Following are some of example scenarios for using Kinesis Data Analytics: 
    + **Generate time-series analytics** – You can calculate metrics over time windows, and then stream values to Amazon S3 or Amazon Redshift through a Kinesis data delivery stream.
    + **Feed real-time dashboards** – You can send aggregated and processed streaming data results downstream to feed real-time dashboards.
    + **Create real-time metrics** – You can create custom metrics and triggers for use in real-time monitoring, notifications, and alarms.
## Application architecture

![amazon_kinesis_data_analytics](./images/amazon_kinesis_data_analytics.png)
+ Each application has a **name, description, version ID, and status**.
+ Amazon Kinesis Data Analytics assigns a **version ID** when you first create an application. This version ID is updated when you update any application configuration.+ **Input** – The streaming source for your application. 
    + You can select **either a Kinesis data stream or a Kinesis Data Firehose data delivery stream** as the streaming source.
    + Kinesis Data Analytics **continuously polls the streaming source for new data** and ingests it in in-application streams according to the input configuration.
    + In the **input configuration**, you **map the streaming source to an in-application input stream**.
    + The in-application stream is like a continuously updating table upon which you can perform the `SELECT` and `INSERT SQL` operations.
    + In your application code, you can create **additional in-application streams to store intermediate query results**.
    + You can optionally **partition a single streaming source in multiple in-application input streams** to improve the throughput.
    + You can optionally **configure a reference data source** to enrich your input data stream within the application. It results in an in-application reference table. You **must store your reference data as an object in your S3 bucket**. 
+ **Application code** – A series of SQL statements that process input and produce output. 
    + You can write SQL statements against **in-application streams and reference tables**.
    + You can also write **JOIN queries** to combine data from both of these sources.
+ **Output** – In application code, query results go to in-application streams. 
    + In your application code, you can create one or more in-application streams to hold intermediate results.
    + You can then optionally configure the application output to persist data in the in-application streams that hold your application output (also referred to as in-application output streams) to external destinations.
    + External destinations can be a Kinesis Data Firehose delivery stream or/and a Kinesis data stream
    + Kinesis Data Analytics automatically provides an **in-application error stream** for each application. If your application has issues while processing certain records (for example, because of a type mismatch or late arrival), that record is written to the error stream. You can configure application output to direct Kinesis Data Analytics to persist the error stream data to an external destination for further evaluation
# Amazon Kinesis Data Analytics for Apache Flink
+ Kinesis Data Analytics for Apache Flink is **a fully managed Amazon service** that enables you to **use an Apache Flink application to process streaming data**.
+ With Amazon Kinesis Data Analytics for Apache Flink, you can use **Java, Scala, or SQL** to process and analyze streaming data. 
+ The service enables you to author and run code against streaming sources to perform time-series analytics, feed real-time dashboards, and create real-time metrics.
+ You can build Java and Scala applications in Kinesis Data Analytics using open-source libraries based on Apache Flink. Apache Flink is a popular framework and engine for processing data streams.
+ Kinesis Data Analytics **provides the underlying infrastructure for your Apache Flink applications**. It handles core capabilities like provisioning compute resources, parallel computation, automatic scaling, and application backups (implemented as checkpoints and snapshots)
+ Kinesis Data Analytics application hosts your Apache Flink application and provides it with the following settings: 
    + **Runtime Properties:** Parameters that you can provide to your application. You can change these parameters without recompiling your application code.
    + **Fault Tolerance**: How your application recovers from interrupts and restarts.+ **Logging and Monitoring**: How your application logs events to CloudWatch Logs.+ **Scaling**: How your application provisions computing resources.
# Reference
+ [Amazon Kinesis Data Analytics for SQL Applications Developer Guide](https://docs.aws.amazon.com/kinesisanalytics/latest/dev/what-is.html)
+ [Amazon Kinesis Data Analytics](https://docs.aws.amazon.com/kinesisanalytics/latest/java/what-is.html)  
