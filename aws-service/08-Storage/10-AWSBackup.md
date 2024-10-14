# Overview
+ AWS Backup is a fully-managed **data protection service** that makes it easy to centralize and automate across AWS services, in the cloud, and on premises.
+ Using this service, you can **configure backup policies** and **monitor activity** for your AWS resources in one place.
+ There is **no additional charge** to use the AWS Backup centralized backup features
# Supported features 
+ Centralized backup management
+ Policy-based backup
+ Tag-based backup policies
+ Lifecycle management policies
+ Incremental backups 
    + DynamoDB and Aurora do not support incremental backup.
+ Cross-Region backup 
    + DynamoDB does not support cross-Region backup
+ Cross-account management and cross-account backup 
    + DynamoDB also does not support cross-account backup.
+ Backup activity monitoring
+ [KMS-integrated backup encryption](https://docs.aws.amazon.com/aws-backup/latest/devguide/encryption.html)
+ Satisfy compliance obligations
# Backing Up Amazon EC2 Resources
+ When backing up an Amazon EC2 instance, AWS Backup takes a snapshot of the **root Amazon EBS storage volume, the launch configurations, and all associated EBS volumes**.
+ AWS Backup stores certain configuration parameters of the EC2 instance, including instance type, security groups, Amazon VPC, monitoring configuration, and tags.
+ The backup data is stored as an **Amazon EBS volume-backed Amazon Machine Image** (AMI).
# [Backup plan​​​​​​​​​​​​​​](https://docs.aws.amazon.com/aws-backup/latest/devguide/create-cross-account-backup.html)
+ a *backup plan* is **a policy expression** that defines **when and how** you want to back up your AWS resources+ You can **assign resources to backup plans**, and AWS Backup automatically backs up and retains backups for those resources according to the backup plan.
+ Backup plans are composed of **one or more backup rules**
+ Each backup rule consists of the following elements: 
    + Backup rule name
    + Backup frequency
    + Backup window
+ On occasion, a backup plan might contain multiple, overlapping rules. When the start windows of different rules overlap, AWS Backup **retains the backup under the rule with the longer retention period**.
+ The **lifecycle** defines when a backup is transitioned to cold storage and when it expires.
+ A **backup vault** is a container to organize your backups in
# Continuous backups
+ AWS Backup supports **continuous backups and point-in-time recovery (PITR)** in addition to snapshot backups. 
+ Continuous backup works by **first creating a full backup** of your resource, and then **constantly backing up your resource’s transaction logs**.
+ PITR **restore works by accessing your full backup** and **replaying the transaction log** to the time that you tell AWS Backup to recover.
+ AWS Backup supports continuous backups and point-in-time recovery for the following services and applications:  
    + Amazon S3
    + RDS
    + Aurora
    + SAP HANA on Amazon EC2 instances
+ If you want to stop continuous backups, you must **delete the continuous backup rule** from your backup plan.
+ If a continuous backup rule also specifies a cross-account or cross-Region copy, AWS Backup **takes a snapshot** of the continuous backup, **copies that snapshot** to the destination vault, and **then deletes the source snapshot**. 
+ AWS Backup **does not support copies of Amazon RDS continuous backups** because Amazon RDS does not allow copies of its transaction logs.
+ The minimum retention period is 1 day. The maximum retention period is 35 days.
+ In general, you should protect **each resource with no more than one continuous backup rule**. 
# Cross-Region backup
+ Using AWS Backup, you can **copy backups to multiple AWS Regions** on demand or automatically as part of a scheduled backup plan.
+ Cross-Region replication is particularly valuable if you have **business continuity or compliance requirements** to store backups a minimum distance away from your production data.
+ When you copy a backup to a new AWS Region for the first time, AWS Backup copies the backup in **full**.
+ If a service supports incremental backups, **subsequent** copies of that backup in the same AWS Region will be **incremental**.
+ AWS Backup will **re-encrypt** your copy using the customer managed key of your destination vault.
+ DynamoDB does not support cross-Region backup.
+ Amazon RDS and Aurora support cross-Region backup, or cross-account backup, but not both in the same backup plan.
+ Amazon EFS supports cross-Region copy at the plan level. To apply a different copy rule to a subset of file systems, create a new plan.
# Cross-account backup
+ Using AWS Backup, you can back up to **multiple AWS accounts** on demand or automatically as part of a scheduled backup plan.
+ Use a cross-account backup if you want to **securely copy your backups to one or more AWS accounts** in your organization for operational or security reasons.
+ cross-account backup work flow: 
    + In your destination account, you must create a backup vault.
    + Then, you assign a customer managed key to encrypt backups in the destination account, and a resource-based access policy to allow AWS Backup to access the resources you would like to copy.
    + In the source account, if your resources are encrypted with a customer managed key, you must share this customer managed key with the destination account.
    + You can then create a backup plan and choose a destination account that is part of your organizational unit in AWS Organizations.
+ DynamoDB does not support cross-account backup.
+ For all services except Amazon EFS, cross-account backup only supports customer managed keys. 
+ For Amazon EFS, you can perform cross-account backups using any Amazon EFS backup vault because AWS Backup independently manages the encryption for each Amazon EFS backup vault.
+ Amazon EC2 does not allow cross-account copies of AWS Marketplace AMIs. 
# Reference
+ [AWS Backup](https://docs.aws.amazon.com/aws-backup/latest/devguide/whatisbackup.html)

