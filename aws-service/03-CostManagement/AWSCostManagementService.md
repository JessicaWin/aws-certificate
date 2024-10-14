# AWS Budgets
+ You can use AWS Budgets to **track and take action on your AWS cost and usage**.
+ You can use AWS Budgets to **monitor your aggregate utilization and coverage metrics for your Reserved Instances (RIs) or Savings Plans**.
+ AWS Budgets information is **updated up to three times a day**. Updates typically occur 8–12 hours after the previous update.
+ You can create the following types of budgets: 
    + **Cost budgets** – Plan how much you want to spend on a service.
    + **Usage budgets** – Plan how much you want to use one or more services.
    + **RI utilization budgets** – Define a utilization threshold and receive alerts when your RI usage falls below that threshold. This lets you see if your RIs are unused or under-utilized.
    + **RI coverage budgets** – Define a coverage threshold and receive alerts when the number of your instance hours that are covered by RIs fall below that threshold. This lets you see how much of your instance usage is covered by a reservation.
    + **Savings Plans utilization budgets** – Define a utilization threshold and receive alerts when the usage of your Savings Plans falls below that threshold. This lets you see if your Savings Plans are unused or under-utilized.
    + **Savings Plans coverage budgets** – Define a coverage threshold and receive alerts when your Savings Plans eligible usage that is covered by Savings Plans fall below that threshold. This lets you see how much of your instance usage is covered by Savings Plans.
+ You can **set up optional notifications** that warn you if you exceed, or are forecasted to exceed, your budgeted amount for cost or usage budgets or fall below your target utilization and coverage for RI or Savings Plans budgets.
+ A budget is only visible to users with access to the account that created the budget, and with access to the budget itself
+ You can use AWS Budgets to **run an action on your behalf when a budget exceeds a certain cost or usage threshold**. 
+ Your available actions include **applying an IAM policy or a service control policy (SCP)**
+ AWS Budgets information is updated up to three times a day. Updates typically occur 8–12 hours after the previous update. Budgets can track your unblended, amortized, and blended costs. Budgets can include or exclude charges such as discounts, refunds, support fees, and taxes.
+ 5 weeks of historical usage data is needed by AWS Budgets before it can begin to generate a budget forecast?
## Managing your costs with AWS Budgets
+ You can use AWS Budgets to enable simple-to-complex cost and usage tracking. Some examples include:
+ Setting a monthly cost budget with a fixed target amount to track all costs associated with your account. You can choose to be alerted for both actual (after accruing) and forecasted (before accruing) spends.
+ Setting a monthly cost budget with a variable target amount, with each subsequent month growing the budget target by 5 percent. Then, you can configure your notifications for 80 percent of your budgeted amount and apply an action. For example, you could automatically apply a custom IAM policy that denies you the ability to provision additional resources within an account.
+ Setting a monthly usage budget with a fixed usage amount and forecasted notifications to help ensure that you are staying within the service limits for a specific service. You can also be sure you are staying under a specific AWS Free Tier offering.
+ Setting a daily utilization or coverage budget to track your RI or Savings Plans. You can choose to be notified through email and Amazon SNS topics when your utilization drops below 80 percent for a given day.
## Best practices for controlling access to AWS Budgets
+ To allow users to create budgets in the AWS Billing and Cost Management console, you must also allow users to do the following:
+ View your billing information
+ Create Amazon CloudWatch alarms
+ Create Amazon Simple Notification Service (Amazon SNS) notifications
## Best practices for budget actions
+ Using managed policies
+ Using Amazon EC2 Auto Scaling
## Best practices for setting budget alerts
+ Budget alerts can be sent to up to 10 email addresses and one Amazon SNS topic per alert. You can set budgets to alert against either actual values or forecasted values.
+ Actual alerts are **only sent out once per budget, per budget period**, when a budget **first reached the actual alert threshold**.
+ Forecast-based budget alerts are sent out on **a per-budget, per-budget period basis**. They might **alert more than once** in a budgeted period if the forecasted values exceed, dip below, and then exceed the alert threshold again during the budgeted period.
# AWS Budgets Reports
+ With AWS Budgets, you can **configure a report** to monitor the performance of your existing budgets on a daily, weekly, or monthly cadence and deliver that report to up to 50 email addresses.
# AWS Cost and Usage Reports
+ The AWS Cost and Usage Reports (AWS CUR) **contains the most comprehensive set of cost and usage data available**
+ You can use Cost and Usage Reports to publish your AWS billing reports to an Amazon Simple Storage Service (**Amazon S3**) bucket that you own.
+ You can download your report from the Amazon S3 console, query the report using Amazon Athena, or upload the report into Amazon Redshift or Amazon QuickSight.
+ You can receive reports that **break down your costs** by the hour, day, or month, by product or product resource, or by tags that you define yourself.
+ AWS updates the report in your bucket once a day in comma-separated value (CSV) format.
+ AWS Cost and Usage Reports tracks your AWS usage and provides estimated charges associated with your account. 
+ You can customize the AWS Cost and Usage Reports to aggregate the information either by the hour, day, or month.
+ AWS Cost and Usage Reports can do the following: 
    + Deliver report files to your Amazon S3 bucket
    + Update the report up to three times a day
    + Create, retrieve, and delete your reports using the AWS CUR API Reference
# Savings Plans
+ Savings Plans offer **a flexible pricing model that provides savings** on AWS usage.
+ You can save **up to 72 percent** on your AWS compute workloads.
+ Savings Plans provide savings beyond On-Demand rates in exchange for **a commitment of using a specified amount of compute power (measured per hour) for a one or three year period**.
+ When you sign up for Savings Plans, the prices you'll pay for usage **stays the same through the plan term.**
+ You can pay for your commitment using **All Upfront**, **Partial upfront**, or **No upfront** payment options.
+ Plan types
    + **Compute Savings Plans** provide the most flexibility and prices that are up to 66 percent off of On-Demand rates. 
        + These plans automatically apply to your EC2 instance usage, regardless of instance family, instance sizes, Region, operating system, or tenancy.
        + They also apply to your Fargate and Lambda usage.
    + **EC2 Instance Savings Plans** provide savings up to 72 percent off On-Demand, in exchange for a commitment to **a specific instance family in a chosen AWS Region** 
    + **SageMaker Savings Plans** provide savings up to 64 percent off of On-Demand rates. 
        + These plans automatically apply to your **SageMaker instance** usage regardless of instance family, instance sizes, Region, and component
+ Savings Plans provide savings beyond On-Demand rates in exchange for a commitment of using a specified amount of compute power (measured per hour) for a one or three year period.
    + One year: A year is defined as 365 days (31,536,000 seconds).
    + Three years: Three years is defined as 1,095 days (94,608,000 seconds).
# AWS Cost Explorer
+ AWS Cost Explorer is a tool that enables you to **view and analyze your costs and usage.**
+ You can explore your usage and costs using the main graph, the Cost Explorer cost and usage reports, or the Cost Explorer RI reports.
+ You can **view data for up to the last 12 months**, **forecast how much you're likely to spend for the next 12 months**, and **get recommendations for what Reserved Instances to purchase**.
+ You can enable Cost Explorer for your account by opening Cost Explorer for **the first time in the AWS Cost Management console**.
+ As part of the process of enabling Cost Explorer, AWS automatically configures Cost Anomaly Detection for your account. Cost Anomaly Detection is an AWS Cost Management feature. This feature uses machine learning models to detect and alert on anomalous spend patterns in your deployed AWS services. 
+ You can't enable Cost Explorer using the API.
+ After you enable Cost Explorer, AWS prepares the data about your costs for the current month and the previous 13 months, and then calculates the forecast for the next 12 months. The current month's data is available for viewing in about 24 hours. The rest of your data takes a few days longer. Cost Explorer updates your cost data at least once every 24 hours.
+ Cost Explorer provides **default reports**, but also enables you to change the filters and constraints used to create the reports.
+ Cost Explorer also provides you ways to save the reports that you made.
+ You can save them as a bookmark, download the CSV file, or save them as a report.
## Multi-year data at monthly granularity
+ While you can use the default 14-month historical data to perform cost analysis at quarterly or monthly level, you should enable multi-year data in Cost Explorer if you want to evaluate your year-over-year cost or identify long-term cost trends.
+ You can enable **up to 38 months of multi-year data at monthly granularity** for your entire organization. Using multi-year data to perform cost analysis over a longer duration, you can track changes in your AWS costs as your business or applications mature, or after implementing infrastructure optimizations.
+ Once enabled, multi-year data is available within 48 hours. Note that this data is only available in Cost Explorer, as Savings Plans and Reservations utilization and coverage reports don’t support this data.
## Granular data
+ Cost Explorer provides hourly and resource-level granularity through three features:
+ Resource-level data at daily granularity
+ Cost and usage data for all AWS services at hourly granularity (without resource-level data)
    + By default, Cost Explorer provides **up to 14 months of data at daily and monthly granularity**. However, you can opt in to **hourly granularity for the past 14 days**.
+ EC2-Instances (Elastic Compute Cloud) resource-level data at hourly granularity
## Using Cost Explorer reports
+ Cost Explorer provides default reports, but also enables you to change the filters and constraints used to create the reports.
+ Cost Explorer also provides you ways to save the reports that you made.
+ You can save them as a bookmark, download the CSV file, or save them as a report.
# AWS Billing
+ AWS Billing and Cost Management **provides a suite of features to help you set up your billing, retrieve and pay invoices, and analyze, organize, plan, and optimize your costs**.
+ You can allocate your costs to teams, applications, or environments by using cost categories or cost allocation tags, or using AWS Cost Explorer. 
## Features of AWS Billing and Cost Management
+ Billing and payments: Understand your monthly charges, view and pay invoices, and manage preferences for billing, invoices, tax, and payments.
+ Cost analysis
    + Analyze your costs, export detailed cost and usage data, and forecast your spending.
    + AWS Cost Explorer – Analyze your cost and usage data with visuals, filtering, and grouping. You can forecast your costs and create custom reports.
    + Data exports – Create custom data exports from Billing and Cost Management datasets.
    + Cost Anomaly Detection – Set up automated alerts when AWS detects a cost anomaly to reduce unexpected costs.
    + AWS Free Tier – Monitor current and forecasted usage of free tier services to avoid unexpected costs.
    + Split cost allocation data – Enable detailed cost and usage data for shared Amazon Elastic Container Service (Amazon ECS) resources.
    + Cost Management preferences – Manage what data that member accounts can view, change account data granularity, and configure cost optimization preferences.
+ Cost organization
    + Organize your costs across teams, applications, or end customers.
    + Cost categories – Map costs to teams, applications, or environments, and then view costs along these dimensions in Cost Explorer and data exports. Define split charge rules to allocate shared costs.
    + Cost allocation tags – Use resource tags to organize, and then view costs by cost allocation tag in Cost Explorer and data exports.
+ Budgeting and planning
    + Estimate the cost of a planned workload, and create budgets to track and control costs.
    + Budgets – Set custom budgets for cost and usage to govern costs across your organization and receive alerts when costs exceed your defined thresholds.
+ Savings and commitments
    + Optimize resource usage and use flexible pricing models to lower your bill.
    + AWS Cost Optimization Hub – Identify savings opportunities with tailored recommendations including deleting unused resources, rightsizing, Savings Plans, and reservations.
    + Savings Plans – Reduce your bill compared to on-demand prices with flexible pricing models. Manage your Savings Plans inventory, review purchase recommendations, and analyze Savings Plan utilization and coverage.
    + Reservations – Reserve capacity at discounted rates for Amazon Elastic Compute Cloud (Amazon EC2), Amazon Relational Database Service (Amazon RDS), Amazon Redshift, Amazon DynamoDB, and more.
## Viewing your bill
+ Viewing your monthly charges
+ Using the Bills page to understand your monthly charges and invoice
+ Downloading a PDF of your invoice
+ Getting an invoice emailed to you
+ Downloading a monthly report
+ Viewing your monthly charge
## Using the Billing preferences page
+ Invoice delivery preferences
+ Alert preferences
+ Credit sharing preferences
+ Reserved Instances and Savings Plans discount sharing preferences
+ Detailed billing reports (legacy)
## Managing your payments
+ Making payments, checking unapplied funds, and viewing your payment history
+ Managing your credit card payment verification
+ Managing credit card and ACH payment methods
+ Managing your Advance Pay
+ Managing your AWS payments in CNY
+ Managing your PIX payment method in Brazil
+ Managing your payments in India
+ Managing your payments in AWS Europe
+ Managing your payment profiles
+ Managing your AWS payment preferences
## Managing your purchase orders
+ Setting up purchase order configurations
+ Adding a purchase order
+ Editing your purchase orders
+ Deleting your purchase orders
+ Viewing your purchase orders
+ Reading your purchase order details page
+ Enabling purchase order notifications
+ Use tags to manage access to purchase orders
## Managing your costs with AWS Cost Categories
+ Creating cost categories
+ Tagging cost categories
+ Viewing cost categories
+ Editing cost categories
+ Deleting cost categories
+ Splitting charges within cost categories
## Using AWS cost allocation tags
+ AWS generated cost allocation tags
+ User-defined cost allocation tags
+ Monthly cost allocation report
+ Understanding dates for cost allocation tags
## Consolidated billing for AWS Organizations
+ You can use the **consolidated billing feature in AWS Organizations** to consolidate billing and payment for multiple AWS accounts or multiple Amazon Internet Services Pvt. Ltd (AISPL) accounts.
+ Every organization in AWS Organizations has a **management account that pays the charges of all the member accounts**.
+ Consolidated billing has the following benefits: 
    + One bill – You get one bill for multiple accounts. 
        + For billing purposes, the consolidated billing feature of AWS Organizations **treats all the accounts in the organization as one account**.
        + This means that **all accounts in the organization can receive the hourly cost benefit of Reserved Instances that are purchased by any other account**.
        + With consolidated billing, AWS combines the usage from all accounts to determine which **volume pricing tiers **to apply, giving you a lower overall price whenever possible.
    + Easy tracking – You can track the charges across multiple accounts and download the combined cost and usage data.
    + Combined usage – You can combine the usage across all accounts in the organization to share the volume pricing discounts, Reserved Instance discounts, and Savings Plans. This can result in a lower charge for your project, department, or company than with individual standalone accounts.
    + No extra fee – Consolidated billing is offered at no additional cost.
+ If you manage an organization in AWS Organizations, you can use consolidated billing to **view aggregated usage costs for accounts** in the organization. Consolidated billing can also help you **reduce those costs.**
# Cost Optimization Hub
+ Cost Optimization Hub is an AWS Billing and Cost Management feature that helps you consolidate and prioritize cost optimization recommendations across your AWS accounts and AWS Regions, so that you can get the most out of your AWS spend.
+ You can use Cost Optimization Hub to identify, filter, and aggregate AWS cost optimization recommendations across your AWS accounts and AWS Regions.
+ It makes recommendations on resource rightsizing, idle resource deletion, Savings Plans, and Reserved Instances. With a single dashboard, you avoid having to go to multiple AWS products to identify cost optimization opportunities.
+ After you enable Cost Optimization Hub, you can see estimated monthly savings in AWS Compute Optimizer, consistent with the savings estimates in Cost Optimization Hub.
+ Cost Optimization Hub provides the following main benefits:
    + Automatically identify and consolidate your AWS cost optimization opportunities.
    + Quantify estimated savings that incorporate your AWS pricing and discounts.
    + Aggregate and deduplicate savings across related cost optimization opportunities.
    + Prioritize your cost optimization recommendations with filtering, sorting, and grouping.
    + Measure and benchmark your cost efficiency.
# AWS Cost Categories
+ You can use AWS Cost Categories to map your AWS costs and usage into meaningful categories.
+ With cost categories, you can organize your costs using a rule-based engine.
+ The rules that you configure organize your costs into categories.
+ Companies commonly have multiple perspectives on their business. These can include projects, cost centers, and applications. You can create cost categories to match these perspectives.
# AWS Cost Allocation Tags
+ You can use tags to organize your resources, and **cost allocation tags to track your AWS costs on a detailed level**.
+ After you activate cost allocation tags, AWS uses the cost allocation tags to **organize your resource costs on your cost allocation report**, to make it easier for you to **categorize and track your AWS costs**. 
+ AWS provides two types of cost allocation tags, an *AWS generated tags* and *user-defined tags*. You must activate both types of tags separately before they can appear in Cost Explorer or on a cost allocation report.
# AWS Cost Anomaly Detection
+ AWS Cost Anomaly Detection is an AWS Cost Management feature that **uses machine learning** to continuously monitor your cost and usage **to detect unusual spends**.
+ Using AWS Cost Anomaly Detection includes the following benefits: 
    + Receive alerts individually in aggregated reports. You can receive alerts in an email or an Amazon SNS topic.
    + Evaluate your spend patterns using machine learning methods to minimize false positive alerts. 
    + Analyze and determine the root cause of the anomaly, such as account, service, Region, or usage type that is driving the cost increase.
    + Configure how you need to evaluate your costs. You can choose whether you want to analyze all of your AWS services independently, or by member accounts, cost allocation tags, or cost categories.
# Reserved Instance Recommendations
+ If you **enable Cost Explorer, you automatically** get Amazon EC2, Amazon RDS, ElastiCache, OpenSearch Service, and Amazon Redshift Reserved Instance (RI) **purchase recommendations** that could help you reduce your costs.
+ Cost Explorer recommendations are based on a single account or organization usage of the past seven, 30, or 60 days. 
+ Cost Explorer updates your recommendations at least once every 24 hours.
# Rightsizing Recommendations
+ Rightsizing recommendations **analyze your Amazon EC2 resources and usage** to show opportunities for how you can lower your spending.
+ You can see all of your underutilized Amazon EC2 instances across member accounts in a single view to immediately identify how much you can save
+ Cost Explorer provides a couple of tools to help you **understand where your greatest RI costs are and how you can potentially lower your costs**.
+ Cost Explorer does this by providing you with an overview of your current reservations, showing your RI utilization and coverage, and calculating recommended RIs that could save you money if you purchase them.
+ You can use the **RI reports** page in the Cost Explorer console to see how many reservations you have, how much your reservations are saving you compared to similar usage of On-Demand Instances, and how many of your reservations are expiring this month.
# AWS Pricing Calculator
+ AWS Pricing Calculator lets you explore AWS services and **create an estimate for the cost of your use cases on AWS**.
+ You can **model your solutions** before building them, explore the price points and calculations behind your estimate, and find the available instance types and contract terms that meet your needs.
+ This enables you to make informed decisions about using AWS. 
+ AWS Pricing Calculator is free for use.
+ To generate an estimate, create an estimate and add services or groups and services to your estimate. 
+ You can **save each estimate's unique link** to share or revisit directly through your browser.
+ You can export your AWS Pricing Calculator estimate as a CSV file. 
# AWS Application Cost Profiler
+ AWS Application Cost Profiler is a service that helps you separate your AWS billing and costs by the tenants of your service. 
+ A *tenant* can be a user, a group of users, or a project.
+ You integrate your services with Application Cost Profiler in three steps: 
    + Enable and configure a report – This step defines what you want your final output to look like.
    + Send tenant usage data to Application Cost Profiler – This step requires code in your service to create usage data that associates tenants with the time they use your resources, and then send that usage data to Application Cost Profiler.
    + Get reports – Application Cost Profiler provides reports at the cadence that you specified in your report configuration. The reports show the cost associated with each tenant's usage, giving you a granular view of your billing.

# Summary
+ AWS Cost Explorer and AWS Cost and Usage Reports can help you establish visibility into your cloud spending, while AWS Budgets and AWS Cost Anomaly Detection can help avoid spending more than intended.


# Reference
+ [What is AWS Billing? - AWS Billing](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-what-is.html)
+ [What is AWS Cost Management? - AWS Cost Management](https://docs.aws.amazon.com/cost-management/latest/userguide/what-is-costmanagement.html)
+ [What is AWS Pricing Calculator? - AWS Pricing Calculator](https://docs.aws.amazon.com/pricing-calculator/latest/userguide/what-is-pricing-calculator.html)
+ [What are Savings Plans? - Savings Plans](https://docs.aws.amazon.com/savingsplans/latest/userguide/what-is-savings-plans.html)
+ [What is AWS Application Cost Profiler? - Application Cost Profiler](https://docs.aws.amazon.com/application-cost-profiler/latest/userguide/introduction.html)
+ [AWS Cost Categories](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/manage-cost-categories.html) 
+ [AWS Cost Allocation Tags](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html)  
+ [AWS Cost Explorer](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/ce-what-is.html)  
+ [AWS Cost and Usage Reports](https://docs.aws.amazon.com/cur/latest/userguide/what-is-cur.html)
+ [AWS Consolidated Billing](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/consolidated-billing.html) 
+ [AWS Purchase Order Management](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/manage-purchaseorders.html) 
+ [AWS Credits](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/useconsolidatedbilling-credits.html)  
Control Establish effective governance mechanisms with the right guardrails in place. 
+ [AWS Cost Anomaly Detection](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/manage-ad.html)
+ [AWS Budgets](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/budgets-managing-costs.html) 
+ [AWS Budgets Actions](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/budgets-controls.html)
+ [Savings Plans](https://docs.aws.amazon.com/savingsplans/latest/userguide/what-is-savings-plans.html) 
+ [AWS Reserved Instances](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/ri-recommendations.html)  
+ [AWS Free Tier](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-free-tier.html)
+ [Rightsizing Recommendations](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/ri-recommendations.html)