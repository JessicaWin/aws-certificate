# Overview
+ Amazon AppFlow is a fully-managed integration service that enables you to **securely exchange data between software as a service (SaaS) applications, such as Salesforce, and AWS services, such as Amazon Simple Storage Service (Amazon S3) and Amazon Redshift.**
+ Amazon AppFlow enables you to do the following: 
    + **Get started quickly** — Create data flows to transfer data between a source and destination in minutes, without writing any code.
    + **Keep your data in sync** — Run flows on demand or on a schedule to keep data in sync across your SaaS applications and AWS services.
    + **Bring your data together** — Aggregate data from multiple sources so that you can train your analytics tools more effectively and save money.
    + **Keep track of your data** — Use Amazon AppFlow flow management tools to monitor what data has moved where and when.
    + **Keep your data secure** — Security is a top priority. We encrypt your data at rest and in transit
     **Transfer data privately** — Amazon AppFlow integrates with AWS PrivateLink to provide private data transfer over AWS infrastructure instead of public data transfer over the internet.
# SaaS applications supported by Amazon AppFlow
+ Amazon S3
+ Amazon Redshift
+ Amazon EventBridge
+ Amazon Honeycode
+ Amazon Lookout for Metrics
+ Amplitude
+ Datadog
+ Dynatrace
+ Google Analytics
+ Infor Nexus
+ Marketo
+ Salesforce
+ Salesforce Pardot
+ SAP OData
+ ServiceNow
+ Singular
+ Slack
+ Snowflake
+ Trend Micro
+ Upsolver
+ Veeva
+ Zendesk
# Flow triggers
+ A *trigger* determines how a flow runs. The following are the supported flow trigger types: 
    + **Run on demand** — Users manually run the flow as needed.
    + **Run on event** — Amazon AppFlow runs the flow in response to an event from an SaaS application
    + **Run on schedule** — Amazon AppFlow runs the flow on a recurring schedule.
# Private Amazon AppFlow flows
+ With Amazon AppFlow, you can create private flows between AWS services and supported software as a service (SaaS) applications.
+ Private flows use **AWS PrivateLink** to route data over AWS infrastructure **without exposing it to the public internet**.
+ The following SaaS applications are integrated with AWS PrivateLink: 
    + Salesforce
    + Singular
    + Snowflake
    + Trend Micro

[amazon_app_flow](./images/amazon_app_flow.png)
# Reference
+ [Amazon AppFlow](https://docs.aws.amazon.com/appflow/latest/userguide/what-is-appflow.html) 
