# Overview
+ Amazon CloudWatch **monitors your Amazon Web Services (AWS) resources and the applications** you run on AWS in real time.
+ You can use CloudWatch to **collect and track metrics**, which are variables you can measure for your resources and applications.
+ The CloudWatch home page automatically displays metrics about every AWS service you use. You can additionally **create custom dashboards** to display metrics about your custom applications, and display custom collections of metrics that you choose.
+ You can **create alarms** that watch metrics and send notifications or automatically make changes to the resources you are monitoring when a threshold is breached.
+ With CloudWatch, you gain **system-wide visibility into resource utilization, application performance, and operational health**
# **​​​​​​​**How Amazon CloudWatch works
+ Amazon CloudWatch is basically **a metrics repository**.
+ An AWS service—such as Amazon EC2—puts metrics into the repository, and you retrieve statistics based on those metrics.
+ If you put your own custom metrics into the repository, you can retrieve statistics on these metrics as well.
+ Metrics are **stored separately in Regions**, but you can use CloudWatch **cross-Region functionality to aggregate statistics from different Regions**. 
# Amazon CloudWatch concepts
+ **Namespaces**
    + A *namespace* is a **container for CloudWatch metrics**.
    + Metrics in different namespaces are **isolated from each other**, so that metrics from different applications are not mistakenly aggregated into the same statistics.
    + There is no default namespace. You must specify a namespace for each data point you publish to CloudWatch.
+ **Metrics**
    + *Metrics* are the fundamental concept in CloudWatch.
    + A metric represents a **time-ordered set of data points** that are published to CloudWatch.
    + Think of a metric as a variable to monitor, and the data points as representing the values of that variable over time.
    + Metrics exist only in the Region in which they are created.
    + Metrics cannot be deleted, but they **automatically expire after 15 months** if no new data is published to them.
    + Metrics are uniquely **defined by a name, a namespace, and zero or more dimensions**. Each data point in a metric has a time stamp, and (optionally) a unit of measure.
+ **Time stamps**
    + Each **metric data point must be associated with a time stamp**.
    + The time stamp can be **up to two weeks in the past and up to two hours into the future**.
    + If you do not provide a time stamp, CloudWatch creates a time stamp for you based on **the time the data point was received**.
+ **Metrics retention**
    + Data points with a period of less than 60 seconds are available for 3 hours. These data points are high-resolution custom metrics.
    + Data points with a period of 60 seconds (1 minute) are available for 15 days
    + Data points with a period of 300 seconds (5 minute) are available for 63 days
    + Data points with a period of 3600 seconds (1 hour) are available for 455 days (15 months)
    + Data points that are **initially published with a shorter period are aggregated together for long-term storage**. For example, if you collect data using a period of 1 minute, the data remains available for 15 days with 1-minute resolution. After 15 days this data is still available, but is aggregated and is retrievable only with a resolution of 5 minutes. After 63 days, the data is further aggregated and is available with a resolution of 1 hour.
+ **Dimensions**
    + A *dimension* is a name/value pair that is **part of the identity of a metric**.
    + You can assign up to 10 dimensions to a metric.
    + AWS services that send data to CloudWatch attach dimensions to each metric. You can **use dimensions to filter the results** that CloudWatch returns. For example, you can get statistics for a specific EC2 instance by specifying the `InstanceId` dimension when you search for metrics.
    + For metrics produced by certain AWS services, such as Amazon EC2, CloudWatch can **aggregate data across dimensions**. 
+ **Dimension combinations**
    + CloudWatch treats each unique combination of dimensions as a separate metric, even if the metrics have the same metric name.
    + You can only retrieve statistics using combinations of dimensions that you specifically published.
    + When you retrieve statistics, specify the same values for the namespace, metric name, and dimension parameters that were used when the metrics were created.
    + You can also specify the start and end times for CloudWatch to use for aggregation.
+ **Resolution**
    + Each metric is one of the following: 
    + **Standard** resolution, with data having a one-minute granularity, default is 5 minutes, need to enable detail monitorining if need to have one-minute granularity
    + **High** resolution, with data at a granularity of one second
    + Metrics produced by AWS services are standard resolution by default. When you publish a custom metric, you can define it as either standard resolution or high resolution.
+ **Statistics**
    + *Statistics* are **metric data aggregations over specified periods of time**. 
    + Aggregations are made using the **namespace, metric name, dimensions, and the data point unit of measure**, within the time period you specify.
+ **Units**
    + Each statistic has **a unit of measure**.
    + Example units include **`Bytes`, `Seconds`, `Count`, and `Percent`**.
+ **Periods**
    + A *period* is **the length of time** associated with a specific Amazon CloudWatch statistic. 
    + Each statistic represents **an aggregation of the metrics data collected for a specified period of time**.
    + Periods are defined in numbers of seconds, and valid values for period are 1, 5, 10, 30, or any multiple of 60. 
    + When you retrieve statistics, you can specify **a period, start time, and end time**. 
+ **Aggregation**
    + Amazon CloudWatch **aggregates statistics according to the period length** that you specify when retrieving statistics.
    + You can publish as many data points as you want with the same or similar time stamps.
    + CloudWatch aggregates them according to the specified period length.
    + CloudWatch does not automatically aggregate data across Regions, but you can use metric math to aggregate metrics from different Regions.
+ **Alarms**
    + You can use an *alarm* to automatically initiate actions on your behalf.
    + An alarm **watches a single metric over a specified time period,** and performs one or more specified actions, based on the value of the metric relative to a threshold over time.
    + The action is a notification **sent to an Amazon SNS topic or an Auto Scaling policy**
# Amazon CloudWatch Logs
+ Log Group
+ Log Stream
## How to send log data to CloudWatch Logs
+ Install the configure the CloudWatch Logs agent to send your logs to the CloudWatch Logs service
+ Create metrice filters to automatically monitor the logs sent to CloudWatch Logs
+ View the log data you have sent and stored in CloudWatch Logs
# Infrastructure monitoring
## Using Container Insights
+ Use CloudWatch Container Insights to collect, aggregate, and summarize metrics and logs from your containerized applications and microservices.
+ Container Insights is available for Amazon Elastic Container Service (Amazon ECS), Amazon Elastic Kubernetes Service (Amazon EKS), and Kubernetes platforms on Amazon EC2. 
+ Container Insights supports collecting metrics from clusters deployed on AWS Fargate for both Amazon ECS and Amazon EKS.
+ CloudWatch automatically collects metrics for many resources, such as CPU, memory, disk, and network. Container Insights also provides diagnostic information, such as container restart failures, to help you isolate issues and resolve them quickly. You can also set CloudWatch alarms on metrics that Container Insights collects.
+ Container Insights collects data as performance log events using embedded metric format.
+ When you deploy Container Insights, it automatically creates a log group for the performance log events. You don't need to create this log group yourself.
+ Container Insights is available for Amazon Elastic Container Service, Amazon Elastic Kubernetes Service, and Kubernetes platforms on Amazon EC2 instances.
    + For Amazon ECS, Container Insights collects metrics at the cluster, task, and service levels on both Linux and Windows Server instances. It can collect metrics at the instance level only on Linux instances.
    + For Amazon ECS, network metrics are available only for containers in bridge network mode and awsvpc network mode. They are not available for containers in host network mode.
    + For Amazon Elastic Kubernetes Service, and Kubernetes platforms on Amazon EC2 instances, Container Insights is supported only on Linux instances.
## Using Lambda Insights
+ CloudWatch Lambda Insights is a monitoring and troubleshooting solution for serverless applications running on AWS Lambda.
+ The solution collects, aggregates, and summarizes system-level metrics including CPU time, memory, disk, and network.
+ It also collects, aggregates, and summarizes diagnostic information such as cold starts and Lambda worker shutdowns to help you isolate issues with your Lambda functions and resolve them quickly.
+ Lambda Insights uses a new CloudWatch Lambda extension, which is provided as a Lambda layer.
+ When you install this extension on a Lambda function, it collects system-level metrics and emits a single performance log event for every invocation of that Lambda function. 
+ CloudWatch uses embedded metric formatting to extract metrics from the log events.
+ To enable Lambda Insights on a Lambda function, you can use a one-click toggle in the Lambda console. Alternatively, you can use the AWS CLI, AWS CloudFormation, the AWS Serverless Application Model CLI, or the AWS Cloud Development Kit (AWS CDK)
## Using Contributor Insights to analyze high-cardinality data
+ Contributor Insights allows you to create realtime Top N time series reports by analyzing CloudWatch Logs based on rules you define.
+ The rule matches log events and reports the top Contributors, where a "Contributor" is a unique combination of the fields defined in the rule.
+ All rules analyze incoming data in real time.
+ If you are signed in to an account that is set up as a monitoring account in CloudWatch cross-account observability, you can create Contributor Insights rules in that monitoring account that analyze log groups in source accounts and in the monitoring account. You can also **create a single rule that analyzes log groups in multiple accounts**.
## Amazon CloudWatch Application Insights
+ Amazon CloudWatch Application Insights facilitates observability for your applications and underlying AWS resources.
+ It helps you set up the best monitors for your application resources to continuously analyze data for signs of problems with your applications.
+ Application Insights, which is powered by SageMaker and other AWS technologies, provides automated dashboards that show potential problems with monitored applications, which help you to quickly isolate ongoing issues with your applications and infrastructure. 
+ CloudWatch Application Insights helps you monitor your applications that use Amazon EC2 instances along with other application resources. It identifies and sets up key metrics, logs, and alarms across your application resources and technology stack
+ It **continuously monitors metrics and logs to detect and correlate anomalies and errors**.
+ When errors and anomalies are detected, Application Insights **generates CloudWatch Events** that you can use to set up notifications or take actions.
+ To assist with troubleshooting, it **creates automated dashboards for detected problems**, which include correlated metric anomalies and log errors, along with additional insights to point you to a potential root cause.
+ CloudWatch Application Insights integrates with AWS Launch Wizard to provide a one-click monitoring setup experience for deploying SQL Server HA workloads on AWS.
+ Application Insights provides the following features.
    + **Automatic set up of monitors for application resources**
        + CloudWatch Application Insights reduces the time it takes to set up monitoring for your applications.
        + It does this by scanning your application resources, providing a customizable list of recommended metrics and logs, and setting them up on CloudWatch to provide necessary visibility into your application resources, such as Amazon EC2 and Elastic Load Balancers (ELB).
        + It also sets up dynamic alarms on monitored metrics. The alarms are automatically updated based on anomalies detected in the previous two weeks.
+ **Problem detection and notification**
    + CloudWatch Application Insights detects signs of potential problems with your application, such as metric anomalies and log errors.
    + It correlates these observations to surface potential problems with your application.
    + It then generates CloudWatch Events, which can be configured to receive notifications or take actions. This eliminates the need for you to create individual alarms on metrics or log errors.
+ **Troubleshooting**
    + CloudWatch Application Insights **creates CloudWatch automatic dashboards** for problems that are detected.
    + The dashboards show details about the problem, including the associated metric anomalies and log errors to help you with troubleshooting.
    + They also provide additional insights that point to potential root causes of the anomalies and errors.
## Using the resource health view in the CloudWatch console
+ You can use the resource health view to automatically discover, manage, and visualize the health and performance of hosts across their applications in a single view.
+ You can visualize the health of their hosts by a performance dimension such as CPU or memory, and slice and dice hundreds of hosts in a single view using filters.
+ You can filter by tags or by use cases, such as hosts in the same Auto Scaling group or hosts that use the same load balancer,
# **​​​​​​​​​​​​​​Reference**
+ [What is Amazon CloudWatch? - Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
+ [Introduction to Amazon CloudWatch](https://explore.skillbuilder.aws/learn/course/203/play/25345/introduction-to-amazon-cloudwatch)
+ [Introduction to Amazon CloudWatch Logs](https://explore.skillbuilder.aws/learn/course/191/play/25428/introduction-to-amazon-cloudwatch-logs)
