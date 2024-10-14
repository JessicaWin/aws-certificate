# Overview
+ AWS Auto Scaling helps you quickly and easily scale multiple resources
+ AWS Auto Scaling enables you to quickly discover all of the scalable resources underlying your application and set up application scaling in minutes using built-in scaling recommendations.
+ AWS Auto Scaling monitors your applications and automatically adjusts capacity to maintain steady, predictable performance at the lowest possible cost.
+ Using AWS Auto Scaling, it’s easy to setup application scaling for multiple resources across multiple services in minutes.
+ The service provides a simple, powerful user interface that lets you build scaling plans for resources including **Amazon EC2 instances and Spot Fleets, Amazon ECS tasks, Amazon DynamoDB tables and indexes, and Amazon Aurora Replicas**.
+ AWS Auto Scaling makes scaling simple with recommendations that allow you to **optimize performance, costs, or balance between them**
# Benefits
+ SETUP SCALING QUICKLY
+ MAKE SMART SCALING DECISIONS
+ AUTOMATICALLY MAINTAIN PERFORMANCE
+ PAY ONLY FOR WHAT YOU NEED
# How it works
+ ![AWS-Auto-Scaling](./images/AWS-Auto-Scaling.png)
# What is a scaling plan
+ Use a scaling plan to configure auto scaling for related or associated scalable resources in a matter of minutes.
## Supported resources
+ **Amazon Aurora** – Increase or decrease the number of Aurora read replicas that are provisioned for an Aurora DB cluster.
+ **Amazon EC2 Auto Scaling** – Launch or terminate EC2 instances by increasing or decreasing the desired capacity of an Auto Scaling group.
+ **Amazon Elastic Container Service** – Increase or decrease the desired task count in Amazon ECS.
+ **Amazon DynamoDB** – Increase or decrease the provisioned read and write capacity of a DynamoDB table or a global secondary index.
+ **Spot Fleet** – Launch or terminate EC2 instances by increasing or decreasing the target capacity of a Spot Fleet.
## Scaling plans provide the following features and benefits:
+ **Resource discovery** – AWS Auto Scaling provides automatic resource discovery to help find resources in your application that can be scaled.
+ **Dynamic scaling** – Scaling plans use the Amazon EC2 Auto Scaling and Application Auto Scaling services to adjust capacity of scalable resources to handle changes in traffic or workload. Dynamic scaling metrics can be standard utilization or throughput metrics, or custom metrics.
+ **Built-in scaling recommendations** – AWS Auto Scaling provides scaling strategies with recommendations that you can use to **optimize for performance, costs, or a balance between the two**.
+ **Predictive scaling** – Scaling plans also support predictive scaling for Auto Scaling groups. This helps to scale your Amazon EC2 capacity faster when there are regularly occurring spikes.
# How scaling plans work
+ AWS Auto Scaling lets you use scaling plans to configure a set of instructions for scaling your resources. 
+ After you create your scaling plan, it combines dynamic scaling and predictive scaling methods together to support your scaling strategy.
## scaling strategy?
+ The scaling strategy tells AWS Auto Scaling how to optimize the utilization of resources in your scaling plan.
+ You can **optimize for availability, for cost, or a balance of both**.
+ Alternatively, you can also create your own custom strategy, per the metrics and thresholds you define. You can set separate strategies for each resource or resource type.
## What is dynamic scaling?
+ Dynamic scaling creates **target tracking scaling policies** for the resources in your scaling plan.
+ These scaling policies adjust resource capacity in response to live changes in resource utilization.
+ The intention is to provide enough capacity to maintain utilization at the target value specified by the scaling strategy. 
## What is predictive scaling?
+ Predictive scaling uses machine learning to analyze each resource's historical workload and regularly forecasts the future load.
+ This is similar to how weather forecasts work. Using the forecast, predictive scaling generates scheduled scaling actions to make sure that **the resource capacity is available before your application needs it**.
+ Like dynamic scaling, predictive scaling works to maintain utilization at the target value specified by the scaling strategy.
+ Load forecasting: AWS Auto Scaling **analyzes up to 14 days of history for a specified load metric and forecasts the future demand for the next two days**. This data is available in one-hour intervals and is updated daily.
+ Scheduled scaling actions: AWS Auto Scaling **schedules the scaling actions** that proactively increases and decreases capacity to match the load forecast. At the scheduled time, AWS Auto Scaling **updates the minimum capacity with the value specified by the scheduled scaling action**. The intention is to maintain resource utilization at the target value specified by the scaling strategy. If your application requires more capacity than is forecast, dynamic scaling is available to add additional capacity.
+ Maximum capacity behavior: Minimum and maximum capacity limits for auto scaling apply to each resource. However, you can control whether your application can increase capacity beyond the maximum capacity when the forecast capacity is higher than the maximum capacity.
# Features
+ **Unified scaling**
    + Using AWS Auto Scaling, you can configure automatic scaling for all of the scalable resources powering your application from a **single unified interface**, including:
    + Amazon EC2: Launch or terminate Amazon EC2 instances in an Amazon EC2 Auto Scaling group.
    + Amazon EC2 Spot Fleets: Launch or terminate instances from an Amazon EC2 Spot Fleet, or automatically replace instances that get interrupted for price or capacity reasons.
    + Amazon ECS: Adjust ECS service desired count up or down to respond to load variations.
    + Amazon DynamoDB: Enable a DynamoDB table or a global secondary index to increase its provisioned read and write capacity to handle sudden increases in traffic without throttling.
    + Amazon Aurora: Dynamically adjust the number of Aurora Read Replicas provisioned for an Aurora DB cluster to handle sudden increases in active connections or workload.
+ **Automatic resource discovery**
    + AWS Auto Scaling scans your environment and automatically discovers the scalable cloud resources underlying your application, so you don’t have to manually identify these resources one by one through individual service interfaces.
+ **Built-in scaling strategies**
    + Using AWS Auto Scaling, you can select one of three predefined optimization strategies designed to optimize performance, optimize costs, or balance the two. If you prefer, you can set your own target resource utilization. Using your selected scaling strategy, AWS Auto Scaling will create the scaling policies for each of your resources for you.
+ **Predictive Scaling**
    + Predictive Scaling predicts future traffic, including regularly-occurring spikes, and provisions the right number of EC2 instances in advance of predicted changes. 
    + Predictive Scaling’s machine learning algorithms detect changes in daily and weekly patterns, automatically adjusting their forecasts. This removes the need for manual adjustment of Auto Scaling parameters over time, making Auto Scaling simpler to configure and consume.
    + Auto Scaling enhanced with Predictive Scaling delivers faster, simpler, and more accurate capacity provisioning resulting in lower cost and more responsive applications.
+ Fully-managed
    + AWS Auto Scaling automatically creates target tracking scaling policies for all of the resources in your scaling plan, using your selected scaling strategy to set the target values for each metric. AWS Auto Scaling also creates and manages the Amazon CloudWatch alarms that trigger scaling adjustments for each of your resources.
+ **Smart scaling policies**
    + AWS Auto Scaling continually calculates the appropriate scaling adjustments and immediately adds and removes capacity as needed to keep your metrics on target.
    + AWS target tracking scaling policies are self-optimizing, and learn your actual load patterns to minimize fluctuations in resource capacity.
    + This results in smoother, smarter scaling and you pay only for the resources you actually need.
# Best practices for scaling plans
+ When you create a launch template or launch configuration, **enable detailed monitoring to get CloudWatch metric data for EC2 instances at a one-minute frequency** because that ensures a faster response to load changes
+ We also recommend that you **enable Auto Scaling group metrics**. Otherwise, actual capacity data is not shown in the capacity forecast graphs that are available on completion of the Create Scaling Plan wizard.
+ Check which instance type your Auto Scaling group uses and **be wary of using a burstable performance instance type**(谨慎使用). Depending on the target utilization specified by the scaling plan, you could run the risk of exceeding the baseline and then running out of CPU credits, which limits performance.
+ Your scaling plan can contain resources from multiple services, but **each resource can be in only one scaling plan at a time**
# Reference
+ [AWS Auto Scaling Product Page](https://aws.amazon.com/autoscaling/)
+ [AWS Auto Scaling](https://docs.aws.amazon.com/autoscaling/plans/userguide/what-is-a-scaling-plan.html)
+ [Introduction to AWS Auto Scaling](https://explore.skillbuilder.aws/learn/course/124/play/12031/introduction-to-aws-auto-scaling)
# Rleates Service
+ [Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)
+ [Amazon ECS Auto Scaling](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-auto-scaling.html)
+ [Amazon Spot fleets Auto Scaling](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-fleet-automatic-scaling.html)
+ [Amazon DynamoDB Auto Scaling](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/AutoScaling.html)
+ [Amazon Aurora Auto Scaling](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Integrating.AutoScaling.html)