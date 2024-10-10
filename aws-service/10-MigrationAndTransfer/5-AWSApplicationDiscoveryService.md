# Overview
+ AWS Application Discovery Service helps you **plan your migration to the AWS cloud by collecting usage and configuration data about your on-premises servers**. 
+ Application Discovery Service is **integrated with AWS Migration Hub**, which **simplifies your migration tracking** as it aggregates your migration status information into a single console.
+ You can **view the discovered servers, group them into applications, and then track the migration status** of each application from the Migration Hub console in your home region.
+ Application Discovery Service integrates with **application discovery solutions from AWS Partner Network (APN) partners**. These third-party solutions can help you import details about your on-premises environment directly into Migration Hub, without using any discovery connector or discovery agent.
# Agentless discovery
+ **Agentless discovery** can be performed by deploying the **AWS Agentless Discovery Connector (OVA file)** through your VMware vCenter.
+ After the Discovery Connector is configured, it identifies virtual machines (VMs) and hosts associated with vCenter.
+ The Discovery Connector collects the following static configuration data: 
    + Server hostnames
    + IP addresses
    + MAC addresses
    + disk resource allocations
    + Additionally, it collects the utilization data for each VM and computes average and peak utilization for metrics such as CPU, RAM, and Disk I/O.
# Agent-based discovery
+ **Agent-based discovery** can be performed by deploying the AWS Application Discovery Agent on each of your VMs and physical servers.
+ The agent installer is available for Windows and Linux operating systems.
+ It collects static configuration data, detailed time-series system-performance information, inbound and outbound network connections, and processes that are running.
# AWS Application Discovery Agent
+ The AWS Discovery Agent is AWS **software that you install on on-premises servers and VMs targeted for discovery and migration**.
+ Agents capture system configuration, system performance, running processes, and details of the network connections between systems.
+ Agents support most Linux and Windows operating systems, and you can deploy them on physical **on-premises servers, Amazon EC2 instances, and virtual machines**.
+ The Discovery Agent runs in your local environment and **requires root privileges**.
+ After registration, the agent starts collecting data for the host or VM where it resides. The agent **pings the Application Discovery Service at 15-minute intervals for configuration information**.
# AWS Agentless Discovery Connector
+ **Agentless discovery uses the AWS Discovery Connector.**
+ The AWS Discovery Connector is a **VMware appliance** that can collect information **only about VMware virtual machines (VMs)**.
+ You **install the Discovery Connector as a VM** in your VMware vCenter Server environment using an Open Virtualization Archive (OVA) file
+ After you deploy and configure the Discovery Connector, it **registers with the Application Discovery Service endpoint, and pings the service at regular intervals**, approximately every 60 minutes, for configuration information.
+ After registration, the connector **connects to VMware vCenter Server**, where it collects data about all the VMs and hosts managed by this specific vCenter. 
# Data Exploration in Amazon Athena
+ Data Exploration in Amazon Athena allows you to **analyze the data collected from all the discovered on-premises servers by Discovery Agents in one place**.
+ Once Data Exploration in Amazon Athena is enabled from the Migration Hub console (or by using the StartContinousExport API) and the data collection for agents is turned on, data collected by agents will **automatically get stored in your S3 bucket at regular intervals**.
+ You can then visit Amazon Athena to run **pre-defined queries** to analyze the time-series system performance for each server, the type of processes that are running on each server and the network dependencies between different servers.
# Reference
+ [AWS Application Discovery Service](https://docs.aws.amazon.com/application-discovery/latest/userguide/what-is-appdiscovery.html)



