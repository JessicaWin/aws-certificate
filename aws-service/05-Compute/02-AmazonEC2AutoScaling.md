# Overview
+ When you use Amazon EC2 Auto Scaling, your applications gain the following benefits: 
    + **Better fault tolerance**. Amazon EC2 Auto Scaling can detect when an instance is unhealthy, terminate it, and launch an instance to replace it. You can also configure Amazon EC2 Auto Scaling to **use multiple Availability Zones**. 
    + **Better availability**. Amazon EC2 Auto Scaling helps ensure that your application always has **the right amount of capacity** to handle the current traffic demand.
    + **Better cost management**.  Amazon EC2 Auto Scaling can dynamically increase and decrease capacity as needed.
+ There are no additional fees with Amazon EC2 Auto Scaling
+ Amazon EC2 Auto Scaling attempts to **distribute instances evenly between the Availability Zones** that are enabled for your Auto Scaling group. Amazon EC2 Auto Scaling does this by attempting to launch new instances in the Availability Zone with the fewest instances.
# Auto Scaling components
+ **Auto Scaling Group**
    + Your EC2 instances are organized into *groups* so that they can be treated as a logical unit for the purposes of scaling and management.
    + When you create a group, you can specify its minimum, maximum, and, desired number of EC2 instances.
+ **Configuration templates**
    + Your group uses a *launch template*, or a *launch configuration* (not recommended, offers fewer features), as a configuration template for its EC2 instances.
    + You can specify information such as the AMI ID, instance type, key pair, security groups, and block device mapping for your instances.
+ **Scaling options**
    + Amazon EC2 Auto Scaling provides several ways for you to scale your Auto Scaling groups.
# Rebalancing activities
+ Rebalancing activities fall into two categories: Availability Zone rebalancing and capacity rebalancing.
## Availability Zone rebalancing
+ After certain actions occur, your Auto Scaling group can become **unbalanced between Availability Zones**. Amazon EC2 Auto Scaling compensates by rebalancing the Availability Zones. The following actions can lead to rebalancing activity: 
    + You change the Availability Zones for your group.
    + You explicitly terminate or detach instances and the group becomes unbalanced.
    + An Availability Zone that previously had insufficient capacity recovers and has additional capacity available.
    + An Availability Zone that previously had a Spot price above your maximum price now has a Spot price below your maximum price.
## Capacity Rebalancing
+ You can enable Capacity Rebalancing for your Auto Scaling groups **when using Spot Instances**.
+ When you turn on Capacity Rebalancing, Amazon EC2 Auto Scaling attempts to launch a Spot Instance whenever Amazon EC2 notifies that a Spot Instance is at an elevated risk of interruption.
# Amazon EC2 Auto Scaling instance lifecycle
+ The EC2 instances in an Auto Scaling group have a path, or lifecycle, that differs from that of other EC2 instances. 

![amazone_ec2_auto_scaling_instance_life_cycle](./images/amazone_ec2_auto_scaling_instance_life_cycle.png)
## Scale out
+ When a scale-out event occurs, the Auto Scaling group **launches the required number of EC2 instances**, using its assigned launch configuration.These instances start in the **`Pending`** state
+ If you add a **lifecycle hook** to your Auto Scaling group, you can perform a custom action here.
+ When each instance is **fully configured and passes the Amazon EC2 health checks**, it is attached to the Auto Scaling group and it enters the `InService` state. 
## Instances in service
+ Instances remain in the `InService` state until one of the following occurs:
+ A scale-in event occurs, and Amazon EC2 Auto Scaling chooses to terminate this instance in order to reduce the size of the Auto Scaling group. 
+ You put the instance into a `Standby` state.
+ You detach the instance from the Auto Scaling group.
+ The instance fails a required number of health checks, so it is removed from the Auto Scaling group, terminated, and replaced
## Scale in
+ The following scale-in events direct the Auto Scaling group to detach EC2 instances from the group and terminate them: 
+ You manually decrease the size of the group.
+ You create a scaling policy to automatically decrease the size of the group based on a specified decrease in demand. 
+ You set up scaling by schedule to decrease the size of the group at a specific time. 
+ Instances that are in the process of detaching from the Auto Scaling group and shutting down enter the **`Terminating`** state, and can't be put back into service. If you add a **lifecycle hook** to your Auto Scaling group, you can perform a custom action here
## Attach an instance
+ You can attach a **running EC2 instance that meets certain criteria** to your Auto Scaling group.
+ After the instance is attached, it is **managed** as part of the Auto Scaling group.
## Detach an instance
+ You can detach an instance from your Auto Scaling group.
+ After the instance is detached, you can **manage it separately** from the Auto Scaling group or **attach it to a different Auto Scaling group**.
## Lifecycle hooks
+ You can add a lifecycle hook to your Auto Scaling group so that you can perform custom actions when instances **launch or terminate**.
+ If you added an **`autoscaling:EC2_INSTANCE_LAUNCHING`** lifecycle hook to your Auto Scaling group, the instances move from the **`Pending`** state to the **`Pending:Wait`** state. After you complete the lifecycle action, the instances enter the **`Pending:Proceed`** state. 
+ If you added an **`autoscaling:EC2_INSTANCE_TERMINATING`** lifecycle hook to your Auto Scaling group, the instances move from the **`Terminating`** state to the **`Terminating:Wait`** state. After you complete the lifecycle action, the instances enter the **`Terminating:Proceed`** state.
## Enter and exit standby
+ You can put any instance that is in an `InService` state into a `Standby` state. This enables you to **remove the instance from service, troubleshoot or make changes to it**, and then put it back into service.
+ Instances in a `Standby` state **continue to be managed** by the Auto Scaling group. However, they are **not an active part** of your application until you put them back into service.
# Configuration templates
## Launch templates
+ A launch template specifies instance configuration information. Included are the ID of the Amazon Machine Image (AMI), the instance type, a key pair, security groups, and the other parameters that you use to launch EC2 instances.
+ However, defining a launch template instead of a launch configuration allows you to have **multiple versions of a template**
+ A launch template lets you configure additional settings in your Auto Scaling group to **launch multiple instance types and combine On-Demand and Spot purchase options**
+ A launch template also enables you to **take advantage of newer features of Amazon EC2** such as the current generation of EBS provisioned IOPS volumes (io2), EBS volume tagging, T2 Unlimited instances, elastic inference, and Dedicated Hosts.
+ Support for Dedicated Hosts (host tenancy) is only available if you specify a host resource group. You cannot target a specific host ID or use host placement affinity.
+ A launch template lets you configure a **network type (VPC or EC2-Classic), subnet, and Availability Zone**. However, these settings are **ignored in favor of what is specified in the Auto Scaling group**.
## Launch configurations
+ A *launch configuration* is an instance configuration template that an Auto Scaling group uses to launch EC2 instances
+ You can specify your launch configuration with multiple Auto Scaling groups.
+ However, you can only **specify one launch configuration for an Auto Scaling group at a time**,
+ you **can't modify a launch configuration** after you've created it.
+  To change the launch configuration for an Auto Scaling group, carete a new one and update the Auto Scaling group to use the new launch configuration.
+ After you change the launch configuration for an Auto Scaling group, any new instances are launched using the new configuration options, but **existing instances are not affected**.
+ However, **the `host` tenancy value cannot be used with a launch configuration**. Use the `default` or `dedicated` tenancy values only.
+ you cannot create an Auto Scaling group that launches both Spot and On-Demand Instances or that specifies multiple instance types
# **Auto Scaling Group**
+ An *Auto Scaling group* contains **a collection of Amazon EC2 instances** that are treated as a logical grouping for the purposes of **automatic scaling and management**. 
+ The size of an Auto Scaling group depends on the number of instances that you set as the **desired capacity**.
+ An Auto Scaling group starts by launching enough instances to meet its desired capacity. It maintains this number of instances by performing **periodic health checks** on the instances in the group.
+ An Auto Scaling group can contain EC2 instances in **one or more Availability Zones within the same Region**. However, Auto Scaling groups cannot span multiple Regions.
+ For Auto Scaling groups **in a VPC**, the EC2 instances are launched in subnets. You can select **one or more subnets per Availability Zone**.
+ An Auto Scaling group can launch On-Demand Instances, Spot Instances, or both. You can **specify multiple purchase options** for your Auto Scaling group only when you configure the group to **use a launch template**.
+ To configure Amazon EC2 instances that are launched by your Auto Scaling group, you can specify **a launch template, a launch configuration, or an EC2 instance**. When you specify an ID of an existing instance, Amazon EC2 Auto Scaling creates a launch configuration for you and associates it with the Auto Scaling group.
+ Tagging your instances enables you to see instance cost allocation by tag in your AWS bill.
## Auto Scaling groups with multiple instance types and purchase options
+ When you configure the Auto Scaling group, you can:
+ Choose **one or more instance types** for the group (optionally overriding the instance type that is specified by the launch template). 
+ You **enhance availability** by deploying your application **across multiple instance types** running in **multiple Availability Zones**. 
+ You can use just one instance type, but it is a **best practice to use a few instance types** to allow Amazon EC2 Auto Scaling to launch another instance type in the event that there is **insufficient instance capacity** in your chosen Availability Zones
+ Define **multiple launch templates** to allow instances with different CPU architectures to launch in the same Auto Scaling group.
+ Assign each instance type an **individual weight**. Doing so might be useful, for example, if the instance types offer different vCPU, memory, storage, or network bandwidth capabilities.
+ Prioritize instance types that can benefit from Savings Plan or Reserved Instance discount pricing.
+ Specify how much On-Demand and Spot capacity to launch, and specify an optional On-Demand base portion.
+ Define how Amazon EC2 Auto Scaling should **distribute** your Spot capacity across instance types.
+ Enable Capacity Rebalancing. When you turn on Capacity Rebalancing, Amazon EC2 Auto Scaling **attempts to launch a Spot Instance** whenever the Amazon EC2 Spot service notifies that a Spot Instance is at an elevated risk of interruption. 
### Allocation strategies
+ Amazon EC2 Auto Scaling first tries to **ensure that your instances are evenly balanced across the Availability Zones** that you specified. Then, it launches instance types according to the **allocation strategy** that is specified.
+ The allocation strategy for **On-Demand Instances is `prioritized`**. Amazon EC2 Auto Scaling uses **the order of instance types in the list of launch template** overrides to determine which instance type to use first when fulfilling On-Demand capacity
+ For On-demand Instances, you choose **either the Prioritized or Lowest-price allocation strategy**
    + Launch On-Demand Instances based on the priority order of instance types you set in the Auto Scaling group overrides.
    + Launch On-Demand Instances from the lowest-priced instance pools. 
+ Amazon EC2 Auto Scaling provides the following allocation strategies that can be used for **Spot Instances**: 
    + The** `capacity-optimized`** strategy automatically launches Spot Instances into the most available pools by looking at real-time capacity data and predicting which are the most available
    + Alternatively, you can use the **`capacity-optimized-prioritized`** allocation strategy and then set the order of instance types in the list of launch template overrides from highest to lowest priority
    + The **lowest price** strategy allocates your instances from the number (N) of Spot Instance pools that you specify and from the pools with the **lowest price** per unit at the time of fulfillment.
### Controlling the proportion of On-Demand instances
+ You have full control over the proportion of instances in the Auto Scaling group that are launched as On-Demand Instances.
+ If you choose to specify a base capacity of On-Demand Instances, the Auto Scaling group ensures that this **base capacity of On-Demand Instances is launched first** when the group scales out.
+ **Anything beyond the base capacity uses the On-Demand percentage** to determine how many On-Demand Instances and Spot Instances to launch.  Example: 
    | Purchase options | Group size and number of running instances across purchase options ||||
    | -- | :-----------: | :-----------: | :-----------: | -----------: |
    | | 10 | 20 | 30 | 40 |
    | Example 1: base of 10, 50/50% On-Demand/Spot | | | | |
    | On-Demand Instances (base amount) | 10 | 10  |  10 |  10 |
    | On-Demand Instances | 0 | 5  |  10 |  15 |
    | Spot Instances | 0 | 5  |  10 |  15 |
    | Example 2: base of 0, 0/100% On-Demand/Spot | | | | |
    | On-Demand Instances (base amount) | 0 | 0  |  0 |  0 |
    | On-Demand Instances | 0 | 0  |  0 |  0 |
    | Spot Instances | 10 | 20  |  30 |  40 |
    | Example 3: base of 0, 60/40% On-Demand/Spot | | | | |
    | On-Demand Instances (base amount) | 0 | 0  |  0 |  0 |
    | On-Demand Instances | 6 | 12  |  18 |  24 |
    | Spot Instances | 4 | 8  |  12 |  16 |
    | Example 4: base of 0, 100/0% On-Demand/Spot | | | | |
    | On-Demand Instances (base amount) | 0 | 0  |  0 |  0 |
    | On-Demand Instances | 10 | 20  |  30 |  40 |
    | Spot Instances | 0 | 0  |  0 |  0 |
    | Example 5: base of 12, 0/100% On-Demand/Spot | | | | |
    | On-Demand Instances (base amount) | 10 | 12  |  12 |  12 |
    | On-Demand Instances  | 0 | 0  |  0 |  0 |
    | Spot Instances | 0 | 8  |  18 |  28 |
### Best practices for Spot Instances
+ Use the **default maximum price, which is the On-Demand price**
+ Create your Auto Scaling group **with multiple instance types**
+ Similarly, don't limit yourself to only the most popular instance types
+ We recommend that you use the **`capacity-optimized` allocation strategy**
+ If you choose the `lowest-price` allocation strategy and you run a web service, **specify a high number of Spot pools**
## Elastic Load Balancing
+ Elastic Load Balancing automatically distributes your incoming application traffic across all the EC2 instances that you are running
+ The load balancer and its target group must be **in the same Region** as your Auto Scaling group.
+ When you attach an Application Load Balancer, Network Load Balancer, or Gateway Load Balancer, **you attach a target group**. Amazon EC2 Auto Scaling adds instances to the attached target group when they are launched.
+ When you **attach** a load balancer, it enters the `Adding` state while registering the instances in the group. After all instances in the group are registered, it enters the `Added` state. After at least one registered instance passes the health checks, it enters the `InService` state. When the load balancer is in the `InService` state, Amazon EC2 Auto Scaling can terminate and replace any instances that are reported as unhealthy
+ When you **detach** a load balancer, it enters the `Removing` state while deregistering the instances in the group. The instances **remain running** after they are deregistered.
+ The default health checks for an Auto Scaling group are **EC2 status checks only**. 
+  by default, the Auto Scaling group does not consider an instance unhealthy and replace it if it fails the Elastic Load Balancing health checks.
+ To ensure that your Auto Scaling group can determine instance health based on additional load balancer tests, **configure the Auto Scaling group to use Elastic Load Balancing (`ELB`) health checks**
+ If you configure the Auto Scaling group to use Elastic Load Balancing health checks, it considers the instance unhealthy if it fails either the EC2 status checks or the Elastic Load Balancing health checks. 
## Maximum instance lifetime
+ The maximum instance lifetime specifies the maximum amount of time (in seconds) that an instance can be in service.
+ The maximum duration applies to all current and future instances in the group.
+ As an instance approaches its maximum duration, it is terminated and replaced, and cannot be used again.
+ Value of  maximum instance lifetime should be at least 86,400 seconds (1 day). To clear a previously set value, specify a new value of 0.
+ Note that instances are not guaranteed to be replaced only at the end of their maximum duration.The intention of this more aggressive behavior is to avoid replacing all instances at the same time.
## Instance refresh
+ During an instance refresh, Amazon EC2 Auto Scaling **takes a set of instances out of service**, terminates them, and then launches a set of instances with the new configuration. After that, instances are replaced on **a rolling basis**. In a rolling update, when a new instance launches, Amazon EC2 Auto Scaling waits until the instance passes a health check and completes warm-up before moving on to replace another instance. This process repeats until all instances are terminated and replaced.
+ To do a **phased replacement, you add checkpoints**, which are points in time where the instance refresh pauses.  
+ `CheckpointPercentages`: Specifies threshold values for the percentage of instances to be replaced.
+ `CheckpointDelay`: The amount of time, in seconds, to wait after a checkpoint is reached before continuing
## Merging your Auto Scaling groups into a single multi-zone group
+ To merge separate single-zone Auto Scaling groups into a single group spanning multiple Availability Zones, **rezone one of the single-zone groups into a multi-zone group**. Then, **delete the other groups**. This works for groups with or without a load balancer, as long as the new multi-zone group is in one of the same Availability Zones as the original single-zone groups.
## Delete your Auto Scaling group
+ When you delete an Auto Scaling group, its desired, minimum, and maximum values are set to 0. As a result, the instances are terminated. 
+ If you do not want to terminate one or more instances, you can **detach** them before you delete the Auto Scaling group
# **Scaling options**
## **Maintain current instance levels at all times**
+ maintain a specified number of running instances at all times.
+  achieved by setting the **same value for minimum, maximum, and desired capacity**
## Manual scaling
+ Manual scaling is the most basic way to scale your resources, where you specify only the change in the maximum, minimum, **or desired capacity** of your Auto Scaling group. Amazon EC2 Auto Scaling manages the process of creating or terminating instances to maintain the updated capacity. 
+ When you **attach** instances, the **desired capacity of the group increases** by the number of instances being attached. If the number of instances being attached plus the desired capacity exceeds the maximum size of the group, the request fails.
+ When you **detach** instances, you have the **option of decrementing the desired capacity** for the Auto Scaling group by the number of instances that you are detaching. If you choose **not to decrement** the capacity, Amazon EC2 Auto Scaling **launches new instances** to replace the ones that you detach.
## Dynamic scaling
+ A dynamic scaling policy instructs Amazon EC2 Auto Scaling to **track a specific CloudWatch metric**, and it defines what action to take when the associated CloudWatch alarm is in ALARM.
+ Amazon EC2 Auto Scaling ensures that the new capacity **never goes outside of the minimum and maximum size limits**.The exception is when you use **instance weighting**. In this case, Amazon EC2 Auto Scaling can scale out above the maximum size limit, but only by up to your maximum instance weight. 
+ Dynamic scaling policy types 
    + **Target tracking scaling**—Increase or decrease the current capacity of the group based on a target value for a specific metric.  
    + **Step scaling**—Increase or decrease the current capacity of the group based on a set of scaling adjustments, known as *step adjustments*, that vary based on the size of the alarm breach.
    + **Simple scaling**—Increase or decrease the current capacity of the group based on a single scaling adjustment.
+ For an advanced scaling configuration, your Auto Scaling group can have **more than one scaling policy**.+ When there are multiple policies in force at the same time, there's a chance that each policy could instruct the Auto Scaling group to scale out (or in) at the same time, When these situations occur, Amazon EC2 Auto Scaling **chooses the policy that provides the largest capacity for both scale out and scale in**
### Target tracking scaling policies
+ With target tracking scaling policies, you **select a scaling metric and set a target value**.
+ Amazon EC2 Auto Scaling creates and manages the CloudWatch alarms that trigger the scaling policy and **calculates the scaling adjustment based on the metric and the target value**. 
+ You can have **multiple target tracking scaling policies** for an Auto Scaling group, provided that each of them **uses a different metric**
+ You can **disable the scale-in portion** of a target tracking scaling policy.
+ The following predefined metrics are available: 
    + `ASGAverageCPUUtilization`—Average CPU utilization of the Auto Scaling group.
    + `ASGAverageNetworkIn`—Average number of bytes received on all network interfaces by the Auto Scaling group.
    + `ASGAverageNetworkOut`—Average number of bytes sent out on all network interfaces by the Auto Scaling group.
    + `ALBRequestCountPerTarget`—Number of requests completed per target in an Application Load Balancer target group.
+ To ensure a faster response to changes in the metric value, we recommend that you scale on metrics with a **1-minute frequency**.
### Step and simple scaling policies
+ With step scaling and simple scaling, you choose **scaling metrics and threshold values** for the CloudWatch alarms that invoke the scaling process 
+ Both require you to create CloudWatch alarms for the scaling policies.
+ Both require you to specify the **high and low thresholds** for the alarms.
+ Both require you to define whether to **add or remove instances**, and how many, or set the group to an exact size. 
+ When you create a step scaling policy, you specify one or more step adjustments that automatically scale the number of instances dynamically based on the size of the alarm breach. Each step adjustment specifies the following: 
    + A lower bound for the metric value
    + An upper bound for the metric value
    + The amount by which to scale, based on the scaling adjustment type
+ Amazon EC2 Auto Scaling supports the following adjustment types for step scaling and simple scaling: 
    + `ChangeInCapacity` — Increment or decrement the current capacity of the group by the specified value. A positive value increases the capacity and a negative adjustment value decreases the capacity. 
    + `ExactCapacity` — Change the current capacity of the group to the specified value. Specify a positive value with this adjustment type. 
    + `PercentChangeInCapacity` — Increment or decrement the current capacity of the group by the specified percentage.
### Scaling cooldowns
+ A scaling cooldown helps you prevent your Auto Scaling group from launching or terminating additional instances before the effects of previous activities are visible.
+ When you use simple scaling, after the Auto Scaling group scales using a simple scaling policy, it waits for a cooldown period to complete before any further scaling activities initiated by simple scaling policies can start.
+ During a cooldown period, when a scheduled action starts at the scheduled time, or when scaling activities due to target tracking or step scaling policies start, they can trigger a scaling activity **immediately** without waiting for the cooldown period to expire.
+ A default cooldown period automatically **applies to any scaling activities for simple scaling policies**, and you can optionally request to have it apply to your manual scaling activities.
### Scaling based on Amazon SQS
+ The solution is to use a *backlog per instance* metric with the target value being the *acceptable backlog per instance* to maintain. You can calculate these numbers as follows: 
+ **Backlog per instance**: To calculate your backlog per instance, start with the `ApproximateNumberOfMessages` queue attribute to determine the length of the SQS queue (number of messages available for retrieval from the queue). Divide that number by the fleet's running capacity, which for an Auto Scaling group is the number of instances in the `InService` state, to get the backlog per instance.
+ **Acceptable backlog per instance**: To calculate your target value, first determine what your application can accept in terms of latency. Then, take the acceptable latency value and divide it by the average time that an EC2 instance takes to process a message.
+ To illustrate with an example, let's say that the current `ApproximateNumberOfMessages` is 1500 and the fleet's running capacity is 10. If the average processing time is 0.1 seconds for each message and the longest acceptable latency is 10 seconds, then the acceptable backlog per instance is 10 / 0.1, which equals 100. This means that 100 is the target value for your target tracking policy. If the backlog per instance is currently at 150 (1500 / 10), your fleet scales out, and it scale out by five instances to maintain proportion to the target value.
## Scheduled scaling 
+ Scheduled scaling helps you to set up your own scaling schedule according to **predictable load changes**.
+ To use scheduled scaling, you create *scheduled actions*. Scheduled actions are **performed automatically as a function of date and time**.
+ When you create a scheduled action, you specify when the scaling activity should occur and the new desired, minimum, and maximum sizes for the scaling action. 
+ The order of execution for scheduled actions is guaranteed within the same group, but not for scheduled actions across groups.
+ The names of scheduled actions **must be unique per Auto Scaling group**.
+ A scheduled action must have **a unique time value**. 
+ You can create **a maximum of 125 scheduled actions** per Auto Scaling group.
## **Predictive scaling**
+ combine predictive scaling and dynamic scaling (proactive and reactive approaches, respectively) to scale your Amazon EC2 capacity faste
+ Predictive scaling is well suited for situations where you have: 
    + Cyclical traffic, such as high use of resources during regular business hours and low use of resources during evenings and weekends
    + Recurring on-and-off workload patterns, such as batch processing, testing, or periodic data analysis
    + Applications that take a long time to initialize, causing a noticeable latency impact on application performance during scale-out events 
+ In general, if you have **regular patterns of traffic increases and applications that take a long time to initialize**, you should consider using predictive scaling. 
+ Predictive scaling uses **machine learning** to predict capacity requirements based on historical data from CloudWatch.
+ To use predictive scaling, you first create a scaling policy with a pair of metrics and a target utilization. 
+ Predictive scaling finds patterns in CloudWatch metric data from the **previous 14 days** to create an **hourly forecast for the next 48 hours**. Forecast data is **updated daily** based on the most recent CloudWatch metric data.
+ Using the forecast, Amazon EC2 Auto Scaling scales the number of instances at the beginning of each hour: 
    + If actual capacity is less than the predicted capacity, Amazon EC2 Auto Scaling **scales out** your Auto Scaling group so that its desired capacity is equal to the predicted capacity.
    + If actual capacity is greater than the predicted capacity, Amazon EC2 Auto Scaling **doesn't scale in**capacity.
    + The values that you set for the minimum and maximum capacity of the Auto Scaling group are adhered to if the predicted capacity is outside of this range.
+ Predictive scaling requires 24 hours of metric history before it can generate forecasts.
+ You currently **cannot** use predictive scaling with Auto Scaling groups that have a mixed instances policy.
+ You currently **cannot specify your custom metrics** in a predictive scaling policy.
## Lifecycle hooks
+ Amazon EC2 Auto Scaling offers the ability to add lifecycle hooks to your Auto Scaling groups.
+ These hooks enable an Auto Scaling group to be aware of events in the Auto Scaling instance lifecycle, and then **perform a custom action** when the corresponding lifecycle event occurs.
+ A lifecycle hook provides a specified amount of time (**one hour by default**) to complete the lifecycle action before the instance transitions to the next state.
+ A popular use of lifecycle hooks is to control when instances are registered with Elastic Load Balancing.
## Warm pools 
+ A warm pool gives you the ability to decrease latency for your applications that have exceptionally long boot times
+ A warm pool is a pool of **pre-initialized EC2 instances** that sits alongside the Auto Scaling group. Whenever your application needs to scale out, the Auto Scaling group can draw on the warm pool to meet its new desired capacity. The goal of a warm pool is to ensure that instances are **ready to quickly start serving application traffic**, accelerating the response to a scale-out event.
+ You have the option of keeping instances in the warm pool in one of two states: `Stopped` or `Running`.
+ The size of the warm pool is calculated as the difference between two numbers: the Auto Scaling group's maximum capacity and its desired capacity. The exception is if you specify a value for **Max prepared capacity**, in which case the size of the warm pool is calculated as the difference between the **Max prepared capacity** and the desired capacity. 
+ You **cannot** add a warm pool to Auto Scaling groups that have **a mixed instances policy or that launch Spot Instances**.
+ You can put an instance in a `Stopped` state only if it has an Amazon EBS volume as its root device. Instances that use instance stores for the root device cannot be stopped.
+ If your warm pool is depleted when there is a scale-out event, instances will launch directly into the Auto Scaling group (a *cold start*). You could also experience cold starts if an Availability Zone is out of capacity.
+ If you try using warm pools with Amazon Elastic Container Service (Amazon ECS) or Elastic Kubernetes Service (Amazon EKS) managed node groups, there is a chance that these services will schedule jobs on an instance before it reaches the warm pool.
## Termination policies
+ Using termination policies, you can control which instances you prefer to terminate first when a scale-in event occurs.
+ The default termination policy is designed to help ensure that your instances **span Availability Zones evenly for high availability**
+ Amazon EC2 Auto Scaling supports the following termination policies: 
    + `Default`. Terminate instances according to the default termination policy.
    + `AllocationStrategy`. Terminate instances in the Auto Scaling group to align the remaining instances to the allocation strategy for the type of instance that is terminating (either a Spot Instance or an On-Demand Instance). 
    + `OldestLaunchTemplate`. Terminate instances that have the oldest launch template. 
    + `OldestLaunchConfiguration`. Terminate instances that have the oldest launch configuration. 
    + `ClosestToNextInstanceHour`. Terminate instances that are closest to the next billing hour.
    + `NewestInstance`. Terminate the newest instance in the group. 
    + `OldestInstance`. Terminate the oldest instance in the group
+ To control whether an Auto Scaling group can terminate a particular instance when scaling in, use instance scale-in protection. You can enable the instance scale-in protection setting on an Auto Scaling group or on an individual Auto Scaling instance. 
# Security
+ Amazon EC2 Auto Scaling uses service-linked roles for the permissions that it requires to call other Amazon Web Services on your behalf.
+ A service-linked role is a unique type of IAM role that is **linked directly to an AWS service**.
+ only the linked service can assume a service-linked role
+ You **cannot edit** the service-linked roles that are created for Amazon EC2 Auto Scaling. After you create a service-linked role, you cannot change the name of the role or its permissions.
# Reference
[amazon ec2 auto scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)

