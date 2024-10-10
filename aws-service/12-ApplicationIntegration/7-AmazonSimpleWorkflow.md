# Overview
+ The Amazon Simple Workflow Service (Amazon SWF) makes it easy to **build applications that coordinate work** across distributed components+ Amazon SWF gives you full control over implementing tasks and coordinating them without worrying about underlying complexities such as tracking their progress and maintaining their state.
# Simple Workflow Concepts
+ The fundamental concept in Amazon SWF is the **workflow**. A workflow is a **set of activities** that carry out some objective, together with **logic that coordinates the activities**. 
    + Each workflow runs in an AWS resource called a **domain**, which controls the workflow's scope. An AWS account can have **multiple domains**, each of which can contain multiple workflows, but workflows in **different domains can't interact**.
    + When designing an Amazon SWF workflow, you precisely define each of the required activities. You then register each activity with Amazon SWF as an **activity type**. 
+ An **activity worker** is a program that receives activity tasks, performs them, and provides results back
+ An **activity task** that represents one invocation of an activity
+ Activity tasks—and the activity workers that perform them—can run synchronously or asynchronously.
+ Different activity workers can be written in **different programming languages and run on different operating systems**.
+ The **decider** directs the workflow by receiving decision tasks from Amazon SWF and responding back to Amazon SWF with decisions.
+ A **decision** represents an action or set of actions which are the **next steps in the workflow**. A typical decision would be to schedule an activity task. 
# Workflow Execution
+ Write activity workers that implement the processing steps in your workflow.
+ Write a decider to implement the coordination logic of your workflow.
+ Register your activities and workflow with Amazon SWF.
+ Start your activity workers and decider.
+ Start one or more executions of your workflow.+ View workflow executions using the AWS Management Console.
# How Amazon SWF Works
+ Workflow History
    + The progress of every workflow execution is recorded in its workflow history, which Amazon SWF maintains.
    + The workflow history is a detailed, complete, and consistent record of every event that occurred since the workflow execution started.
+ Actors can be workflow **starters, deciders, or activity workers**. 
+ A workflow starter is **any application that can initiate workflow** executions.
+ A decider is an implementation of a workflow's **coordination logic**. 
+ Deciders control the flow of activity tasks in a workflow execution.
+ Whenever a change occurs during a workflow execution, such as the completion of a task, a decision task including the entire workflow history will be passed to a decider.
+ An activity worker is a process or thread that **performs the activity tasks** that are part of your workflow.  
+ Each activity worker **polls Amazon SWF for new tasks** that are appropriate for that activity worker to perform; certain tasks can be performed only by certain activity workers.
+ Amazon SWF interacts with activity workers and deciders by providing them with work assignments known as **tasks**. There are three types of tasks in Amazon SWF: 
    + **Activity task** – An Activity task tells an activity worker to perform its function, such as to check inventory or charge a credit card. The activity task contains all the information that the activity worker needs to perform its function.
    + **Lambda task** – A Lambda task is similar to an Activity task, but executes a Lambda function instead of a traditional Amazon SWF activity.
    + **Decision task** – A Decision task tells a decider that the state of the workflow execution has changed so that the decider can determine the next activity that needs to be performed. The decision task contains the current workflow history.
+ **Task lists** provide a way of organizing the various tasks associated with a workflow. 
    + You can think of task lists as similar to dynamic queues.
    + When a task is scheduled in Amazon SWF, you can **specify a queue (task list) to put it in**.
    + Similarly, when you **poll** Amazon SWF for a task you say which queue (task list) to get the task from.
+ Deciders and activity workers communicate with Amazon SWF using **long polling**. The decider or activity worker **periodically initiates communication with Amazon SWF**, notifying Amazon SWF of its availability to accept a task, and then specifies a task list to get tasks from.
+ If a task is available on the specified task list, Amazon SWF returns it immediately in the response. 
+ If no task is available, Amazon SWF **holds the TCP connection open for up to 60 seconds** so that, if a task becomes available during that time, it can be returned in the same connection.
+ If no task becomes available within 60 seconds, it returns an empty response and closes the connection.
# Reference
+ [Amazon Simple Workflow Service](https://docs.aws.amazon.com/amazonswf/latest/developerguide/swf-welcome.html)
