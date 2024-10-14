# Overview
+ Amazon EventBridge is a **serverless event bus service** that you can use to connect your applications with data from a variety of sources.
+ EventBridge **delivers a stream of real-time data** from your applications, software as a service (SaaS) applications, and AWS services to targets such as AWS Lambda functions, HTTP invocation endpoints using API destinations, or event buses in other AWS accounts.
+ EventBridge receives an *event*, an indicator of a change in environment, and applies a rule to route the event to a target. Rules match events to targets based on either the structure of the event, called an *event pattern*, or on a schedule. 
# Event Bus
+ An event bus is a pipeline that receives events.
+ Rules associated with the event bus evaluate events as they arrive.
+ Each rule checks whether an event matches the rule's criteria.
+ You **associate a rule with a specific event bus**, so the rule only applies to events received by that event bus.
+ To manage permissions for an event bus, you can configure a resource-based policy for it. A **resource-based policy** specifies which events to allow, and which entities have permission to create or modify rules or targets for an event. 
+ You can configure **up to 300 rules for each event bus**. If you have more than 300 rules in your environment, you can create custom event buses in your account and then associate an additional 300 rules with each event bus.
+ The most common event buses are: 
    + The default event bus in each account receives events from AWS services.
    + A custom event bus sends events to or receives events from a different account.
    + A custom event bus sends events to or receives events from a different Region to aggregate events in a single location.
    + A partner event bus receives events from a SaaS partner.
# Events
+ An *event* indicates a change in an environment such as an AWS environment, a SaaS partner service or application, or one of your applications or services. The following are examples of events: 
    + Amazon EC2 generates an event when the state of an instance changes from pending to running.
    + Amazon EC2 Auto Scaling generates events when it launches or terminates instances.
    + AWS CloudTrail publishes events when you make API calls.
+ The following fields appear in an event: 
    + version
    + id
    + detail-type
    + source
    + account
    + time
    + region
    + resources
    + detail
# Event patterns
+ Event patterns have the **same structure as the events** they match.
+ To create an event pattern, you specify the fields of an event that you want the event pattern to match.
+ For an event pattern to match an event, the event must **contain all the field names listed in the event pattern**. The field names must also appear in the event **with the same nesting structure**.
+ For strings, EventBridge uses exact character-by-character matching without case-folding or any other string normalization.
+ For numbers, EventBridge uses string representation.
+ With content filtering, you can write complex event patterns that only match events under very specific conditions 
    + Prefix matching
    + Anything-but matching
    + Numeric matching
    + IP address matching
    + Exists matching
    + Complex example with multiple matching
+ The **`PutEvents`** action sends multiple events to EventBridge in a single request.
# Rule
+ A rule **matches incoming events and sends them to targets for processing**. 
+ A single rule can **send an event to multiple targets**, which then run in parallel.
+ Rules are based either on an **event pattern or a schedule.**
+ Sometimes an event isn't successfully delivered to the target specified in a rule. 
+ When an event isn't successfully delivered to a target because of retriable errors, EventBridge retries sending the event. 
    + You set the length of time it tries, and number of retry attempts in the **Retry policy** settings for the target.
    + By default, EventBridge retries sending the event for 24 hours and up to 185 times
    + To avoid losing events after they fail to be delivered to a target, you can configure a **dead-letter queue (DLQ) and send all failed events to it for processing later**.
# Targets
+ A *target* is a **resource or endpoint that EventBridge sends an event to** when the event matches the event pattern defined for a rule.
+ To deliver event data to a target, EventBridge **needs permission to access the target** resource.
+ You can define **up to five targets** for each rule.
+ Amazon EventBridge **API destinations** are **HTTP endpoints** that you can invoke as the target of a rule
+ When you create an API destination, you specify a connection to use for it.
+ A *connection* specifies the **authorization type and parameters** to use to authorize with the API destination endpoint.
+ You can choose an existing connection from your account or create a connection when you create an API destination. EventBridge supports Basic, OAuth, and API Key authorization.
+ Amazon EventBridge supports sending events to an **API Gateway REST endpoint.**
+ You can **customize the text from an event** before EventBridge passes the event to the target of a rule. 
# Archive and replay
+ In EventBridge, you can create an archive of events so that you can easily replay them at a later time.
+ When you create an archive in EventBridge, you can **determine which events are sent to the archive by specifying an event pattern**.
+ EventBridge sends events that match the event pattern to the archive.
+ You also **set the retention period** to store events in the archive before they are discarded.
+ After you create an archive, you can then replay events from the archive. 
+ When you replay events, you can specify **which archive to replay events from**, **the start and end time for the event to replay, the event bus, or one or more rules to replay the events to**.
+ Events aren't necessarily replayed in the same order that they were added to the archive.
# Schemas
+ A schema defines **the structure of events** that are sent to EventBridge.
+ **Schema registries** are containers for schemas. Schema registries collect and organize schemas so that your schemas are in logical groups.
# Using Amazon EventBridge with Interface VPC Endpoints
+ If you use Amazon Virtual Private Cloud (Amazon VPC) to host your AWS resources, you can establish a private connection between your VPC and EventBridge.
+ To connect your VPC to EventBridge, you define an **interface VPC endpoint**for EventBridge. The endpoint provides reliable, scalable connectivity to EventBridge **without** requiring an internet gateway, network address translation (NAT) instance, or VPN connection.
+ Interface VPC endpoints are powered by **AWS PrivateLink**, which enables private communication between AWS services using **an elastic network interface with private IP addresses**.
# Integration with AWS X-Ray
+ You can use **AWS X-Ray** to trace events that pass through EventBridge. EventBridge passes the original trace header to the target so that target services can track, analyze, and debug.
+ EventBridge can pass a trace header for an event only if the **event came from a `PutEvents` request that passed the trace context**.
+ X-Ray **doesn't trace** events that originate from third-party partners, scheduled events, or AWS services, and these event sources don't appear on your X-Ray service map.
# Reference
+ [Amazon EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
