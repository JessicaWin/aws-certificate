# AWS Batch
+ As a fully managed service, AWS Batch helps you to **run batch computing workloads of any scale** on the AWS Cloud.
+ AWS Batch **automatically provisions compute resources** and optimizes the workload distribution based on the quantity and scale of the workloads
.+ With AWS Batch, there's **no need to install or manage batch computing software**, so you can focus your time on analyzing results and solving problems.
# Jobs
+ A unit of work (such as a shell script, a Linux executable, or a Docker container image) that you submit to AWS Batch.
+ It has a name, and runs as a containerized application on AWS Fargate or Amazon EC2 resources in your compute environment, using parameters that you specify in a job definition.
+ Jobs can reference other jobs by name or by ID, and can be dependent on the successful completion of other jobs.
# Job Definitions
+ A job definition specifies **how jobs are to be run**. You can think of a job definition as a blueprint for the resources in your job.
+ You can **supply your job with an IAM role** to provide access to other AWS resources.
+ You also specify both memory and CPU requirements.
+ The job definition can also control container properties, environment variables, and mount points for persistent storage.
+ Many of the specifications in a job definition can be overridden by specifying new values when submitting individual Jobs. 
# Job Queues
+ When you submit an AWS Batch job, you **submit it to a particular job queue**, where the job resides until it's scheduled onto a compute environment.
+ You associate one or more compute environments with a job queue.
+ You can also assign priority values for these compute environments and even across job queues themselves. For example, you can have a high priority queue that you submit time-sensitive jobs to, and a low priority queue for jobs that can run anytime when compute resources are cheaper.
# Compute Environment
+ A compute environment is a set of managed or unmanaged compute resources that are **used to run jobs**.
+ With managed compute environments, you can specify desired compute type (Fargate or EC2) at several levels of detail.
# Reference
[AWS Batch](https://docs.aws.amazon.com/batch/latest/userguide/what-is-batch.html)