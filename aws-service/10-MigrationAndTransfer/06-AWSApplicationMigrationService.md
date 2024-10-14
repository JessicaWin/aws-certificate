# Overview
+ AWS Application Migration Service (MGN) is a highly automated lift-and-shift (rehost) solution that simplifies, expedites, and reduces the cost of migrating applications to AWS.
+ It enables companies to lift-and-shift a large number of physical, virtual, or cloud servers without compatibility issues, performance disruption, or long cutover windows. 
+ Application Migration Service **must be initialized upon first use** from within the Application Migration Service Console. 
+ Application Migration Service works with the AWS Migration Hub (MGH), allowing you to **organize your servers into applications and then to track the progress of all your MGN at the server and app level**, even as you move servers into multiple AWS Regions.
+ Application Migration Service automatically replicates **entire servers, including operating system, applications, data, and configurations**.
# Migration workflow
+ Install the **AWS Replication Agent** on the source server.
+ Wait until Initial Sync is finished.
+ Launch Test instances.
+ Perform acceptance tests on the servers. After the Test instance is tested successfully, finalize the Test and delete the Test instance.
+ Wait for the Cutover window.
+ Confirm that there is no Lag.
+ Stop all operational services on the source server.
+ Launch a Cutover instance.
+ Confirm that the Cutover instance was launched successfully and then finalize the Cutover.
+ Archive the source server.
# Application Migration Service setup
+ the first setup step for Application Migration Service is **creating the Replication Settings template**. 
+ **Replication Servers** - Replication Servers are lightweight Amazon EC2 instances that are used to replicate data between your source servers and AWS. 
+ **Data routing and throttling** - Application Migration Service gives you multiple options to control how data is routed from your source servers to the Replication Servers on AWS. 
+ **Replication resource tags** - Replication resource tags allow you to add custom Tags to your Application Migration Service resources.
+ **Add source servers to Application Migration Service** by installing the AWS Replication Agent (also referred to as "the Agent") on them 
    + After the source server has been added to Application Migration Service, it will undergo the **Migration Lifecycle steps**.
    + **Not ready**- The server is undergoing the Initial Sync process and is not yet ready for testing. Data replication can only commence once all of the Initial Sync steps have been completed.
    + **Ready for testing**- The server has been successfully added to Application Migration Service and data replication has started. Test or Cutover instances can now be launched for this server.
    + **Test in progress**- A Test instance is currently being launched for this server.
    + **Ready for cutover**- This server has been tested and is now ready for a Cutover instance to be launched.
    + **Cutover in progress**- A Cutover instance is currently being launched for this server.
    + **Cutover complete** - This server has been cutover. All of the data on this server has been migrated to the AWS Cutover instance.
    + **Disconnected** - This server has been disconnected from Application Migration Service.
+ After you have added your source servers to the Application Migration Service Console, you will need to **configure the launch settings for each server**.  
    + The launch settings are a set of instructions that determine **how a Test or Cutover instance will be launched for each source server on AWS**.
+ After you have added all of your source servers and configured their launch settings, you are ready to **launch a Test instance**. 
+ Once you have finalized the testing of all of your source servers, you are ready for **cutover**. You should perform the cutover at a set date and time. The cutover will migrate your source servers to the Cutover instances on AWS.
# AWS Server Migration Service
+ AWS Server Migration Service (AWS SMS) automates the migration of your on-premises VMware vSphere, Microsoft Hyper-V/SCVMM, and Azure virtual machines to the AWS Cloud.
+ AWS SMS incrementally **replicates your server VMs as cloud-hosted Amazon Machine Images (AMIs) ready for deployment on Amazon EC2**
+ As of March 31, 2022, AWS will discontinue AWS Server Migration Service (AWS SMS). Going forward, we recommend AWS Application Migration Service (AWS MGN) as the primary migration service for lift-and-shift migrations.
+ The **Server Migration Connector** is a FreeBSD VM that you install in your on-premises virtualization environment. The supported platforms are **VMware vSphere, Microsoft Hyper-V/SCVMM, and Microsoft Azure**.
# Reference
+ [Application Migration Service](https://docs.aws.amazon.com/mgn/latest/ug/what-is-application-migration-service.html)
+ [AWS Server Migration Service](https://docs.aws.amazon.com/server-migration-service/latest/userguide/server-migration.html)
