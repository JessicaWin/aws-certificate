# Overview
+ AWS Compute Optimizer is a service that **analyzes the configuration and utilization metrics of your AWS resources**.
+ It reports whether your resources are optimal, and generates optimization recommendations to reduce the cost and improve the performance of your workloads.
# Supported resources and requirements
+ Compute Optimizer generates recommendations for the following resources:
+ Amazon Elastic Compute Cloud (Amazon EC2) instances
+ Amazon EC2 Auto Scaling groups
+ Amazon Elastic Block Store (Amazon EBS) volumes
+ AWS Lambda functions
+ ECS services on Fargate
# Opting in
+ You must opt in to have Compute Optimizer analyze your AWS resources.
+ The service supports standalone AWS accounts, member accounts of an organization, and the management account of an organization. 
# Analyzing metrics
+ After you opt in, Compute Optimizer begins analyzing the specifications and the utilization metrics of your resources from Amazon CloudWatch for the last 14 days.
# Enhancing recommendations
+ After you opt in, you can enhance your recommendations by activating recommendation preferences, such as the enhanced infrastructure metrics paid feature.
+ It extends the metrics analysis look-back period for EC2 instances, including instances in Auto Scaling groups, to **three months** (compared to the 14-day default)
+ To generate recommendations, Compute Optimizer requires **at least 30 consecutive hours of CloudWatch metric data** from your resource. 
+ Compute Optimizer generates recommendations for instance types in the C, D, H, I, M, R, T, X, and z instance families
+ Compute Optimizer generates recommendations for Auto Scaling groups that run instance types from the supported instance families, Additionally, the Auto Scaling groups must Be configured to run a single instance type (i.e., no mixed instance types)
+ Have the same values for desired, minimum, and maximum capacity (i.e., an Auto Scaling group with a fixed number of instances)
+ Not have a scaling policy attached
+ Not have overrides configured
+ Compute Optimizer generates recommendations for General Purpose SSD (`gp2` and `gp3`), and Provisioned IOPS SSD (`io1` and `io2`) EBS volume types that are attached to an instance.
+ Compute Optimizer generates memory size recommendations only for Lambda functions that have configured memory less than or equal to 1,792 MB, and that have been invoked at least 50 times in the last 14 days. 
# Viewing findings and recommendations
+ Optimization findings for your resources are displayed on the **Compute Optimizer dashboard**. 
# Reference
[What is AWS Compute Optimizer? - AWS Compute Optimizer](https://docs.aws.amazon.com/compute-optimizer/latest/ug/what-is-compute-optimizer.html)
