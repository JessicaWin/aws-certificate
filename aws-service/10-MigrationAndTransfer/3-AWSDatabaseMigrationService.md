# Overview
+ AWS Database Migration Service (AWS DMS) is a web service that you can use to migrate data from a source data store to a target data store.
+ AWS Database Migration Service (AWS DMS) is a cloud service that makes it easy to migrate relational databases, data warehouses, NoSQL databases, and other types of data stores. 
+ With AWS DMS, you can perform **one-time migrations**, and you can **replicate ongoing changes to keep sources and targets in sync**
+ If you want to migrate to a **different database engine**, you can use the **AWS Schema Conversion Tool** (AWS SCT) to translate your database schema to the new platform.
+ At a basic level, AWS DMS is **a server in the AWS Cloud that runs replication software**. 
    + You create a source and target connection to tell AWS DMS where to extract from and load to.
    + Then you schedule a task that runs on this server to move your data.  
+ The only requirement to use AWS DMS is that **one of your endpoints must be on an AWS service**. You can't use AWS DMS to migrate from an on-premises database to another on-premises database.
# How AWS Database Migration Service works
+ At a high level, when using AWS DMS you do the following: 
    + Create a replication server.
    + Create source and target endpoints that have connection information about your data stores.
    + Create one or more migration tasks to migrate data between the source and target data stores.
+ A task can consist of three major phases: 
    + The full load of existing data 
        + During a full load migration, where **existing data from the source is moved to the target**, AWS DMS loads data from tables on the source data store to tables on the target data store.
        + While the full load is in progress, any changes made to the tables being loaded are **cached on the replication server**; these are the cached changes.
    + The application of cached changes 
        + When the full load for a given table is complete, AWS DMS immediately begins to apply the cached changes for that table. 
    + Ongoing replication 
        + Once the table is loaded and the cached changes applied, AWS DMS begins to collect changes as transactions for the ongoing replication phase.
        + If a transaction has tables not yet fully loaded, the changes are stored locally on the replication instance.
        + After AWS DMS applies all cached changes, tables are transactionally consistent.
        + At this point, AWS DMS moves to the ongoing replication phase, applying changes as transactions.
# AWS DMS data validation
+ AWS DMS provides support for data validation to ensure that your data was migrated accurately from the source to the target. If enabled, validation begins immediately after a full load is performed for a table.
# Reference
+ AWS Database Migration Service](https://docs.aws.amazon.com/dms/latest/userguide/Welcome.html)



