# Overview
+ You can use Amazon Data Lifecycle Manager to **automate the creation, retention, and deletion of EBS snapshots and EBS-backed AMIs**.
+ When you automate snapshot and AMI management, it helps you to: 
  + Protect valuable data by enforcing a regular backup schedule.
  + Create standardized AMIs that can be refreshed at regular intervals.
  + Retain backups as required by auditors or internal compliance.
  + Reduce storage costs by deleting outdated backups.
  + Create disaster recovery backup policies that back up data to isolated accounts.
# How Amazon Data Lifecycle Manager works
+ **Snapshots**
    + Snapshots are the primary means to back up data from your EBS volumes
    + To save storage costs, successive snapshots are **incremental**, containing only the volume data that changed since the previous snapshot.
    + When you delete one snapshot in a series of snapshots for a volume, only the data that's unique to that snapshot is removed.
+ **EBS-backed AMIs**
    + Amazon Data Lifecycle Manager **supports EBS-backed AMIs only**.
    + EBS-backed AMIs include a snapshot for each EBS volume that's attached to the source instance.
+ **Target resource tags**
    + Amazon Data Lifecycle Manager uses resource tags to **identify the resources to back up**.
+ **Amazon Data Lifecycle Manager tags**
    + Amazon Data Lifecycle Manager applies the following tags to all snapshots and AMIs created by a policy, to distinguish them from snapshots and AMIs created by any other means: 
    + `aws:dlm:lifecycle-policy-id`
    + `aws:dlm:lifecycle-schedule-name`
    + `aws:dlm:expirationTime` — For policies with age-based retention schedules only.
    + `dlm:managed`
+ Lifecycle policies 
    + **Policy type**—Defines the type of resources that the policy can manage. Amazon Data Lifecycle Manager supports the following types of lifecycle policies: 
        + **Snapshot lifecycle policy**—Used to automate the lifecycle of EBS snapshots. These policies can **target individual EBS volumes or all EBS volumes attached to an instance**.
        + **EBS-backed AMI lifecycle policy**—Used to automate the lifecycle of EBS-backed AMIs and their backing snapshots. These policies can ***target instances only**.
        + **Cross-account copy event policy**—Used to automate snapshot copies across accounts. Use this policy type in conjunction with an EBS snapshot policy that shares snapshots across accounts.
    + **Resource type**—Defines the type of resources that are targeted by the policy. 
        + Snapshot lifecycle policies can target instances or volumes.
        + Use `VOLUME` to create snapshots of individual volumes
        + use `INSTANCE` to create multi-volume snapshots of all of the volumes that are attached to an instance. 
    + **Target tags**—Specifies the tags that must be assigned to an EBS volume or an Amazon EC2 instance for it to be targeted by the policy.
    + **Schedules**—The start times and intervals for creating snapshots or AMIs. 
    + **Retention**—Specifies how snapshots or AMIs are to be retained. 
    + **Policy schedules**
        + Policy schedules define when snapshots or AMIs are created by the policy. Policies can have up to four schedules—one mandatory schedule, and up to three optional schedules.
        + For each schedule, you can define the frequency, fast snapshot restore settings (snapshot lifecycle policies only), cross-Region copy rules, and tags. 
# Reference
[Amazon Data Lifecycle Manager - Amazon Elastic Compute Cloud](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/snapshot-lifecycle.html)
