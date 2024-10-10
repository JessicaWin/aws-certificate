# Overview
+ Step Functions is a serverless orchestration service that lets you combine AWS Lambda functions and other AWS services to build business-critical applications.
+ Step Functions is based on **state machines and tasks**.
+ A state machine is a workflow.
+ A task is a state in a workflow that represents a single unit of work that another AWS service performs.
+ Each step in a workflow is a state.
# Use cases
+ Data processing 
    + Step Functions provides the scalability, reliability, and availability needed to successfully **manage your data processing workflows**.
    + You can manage **millions of concurrent executions** with Step Functions as it **scales horizontally and provides fault-tolerant workflows**.
    + Process data faster using **parallel executions** like Step Functions’ Parallel state type, or dynamic parallelism using its Map state type.
    + Examples of the types of data processing workflows that customers use Step Functions to accomplish include: 
        + **File, video, and image processing**
        + **Coordinate extract, transform and load (ETL) jobs**
        + **Batch processing and High Performance Computing (HPC) workloads**
+ Machine learning 
    + Machine learning enables organizations to quickly analyze collected data to identify patterns, then make decisions with minimal human intervention. 
# Concepts
## Standard vs. Express Workflows
+ When you create a state machine, you can select a **Type** of either **Standard** (default) or **Express**. 
+ The **Type** you choose cannot be changed after your state machine has been created.+ **Standard Workflows** are ideal for **long-running, durable, and auditable workflows.** They can run for up to a year and you can retrieve the full execution history using the Step Functions API, up to 90 days after your execution completes. 
    + Exactly-once workflow execution
+ **Express Workflows** are ideal for **high-volume, event-processing workloads** such as IoT data ingestion, streaming data processing and transformation, and mobile application backends. 
    + They can run for **up to five minutes**.
    + Express Workflows employ an **at-least-once** model, where there is a possibility that an execution **might be run more than once**.
    + **Asynchronous Express Workflows** return confirmation that the workflow was started, but **do not wait** for the workflow to complete.  
    + At-least-once workflow execution
+ **Synchronous Express Workflows** start a workflow, wait until it completes, then return the result.  
    + At-most-once workflow execution
## States
+ Individual states can make decisions based on their input, perform actions, and pass output to other states.
+ A state is referred to by its *name*, which can be any string, but which must be unique within the scope of the entire state machine.
+ States can perform a variety of functions in your state machine: 
    + Do some work in your state machine (a Task state)
    + Make a choice between branches of execution (a Choice state)
    + Stop an execution with a failure or success (a Fail or Succeed state)
    + Simply pass its input to its output or inject some fixed data (a Pass state)
    + Provide a delay for a certain amount of time or until a specified time/date (a Wait state)
    + Begin parallel branches of execution (a Parallel state)
    + Dynamically iterate steps (a Map state)
# Reference
+ [AWS Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)
