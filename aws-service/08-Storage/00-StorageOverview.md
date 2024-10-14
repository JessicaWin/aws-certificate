# Storage Type
- Use cases for file storage
    - Web serving
    - Analytis
    - Media and entertainment
    - Home directories
- Block storage
    - The unique characteristics of block storage make it the preferred option for transactional, mission-critical, and I/O-intensive applications
    - File storage treats files as a singular unit, but block storage splits files into fixed-size chunks of data called blocks that have their own addresses. Each block is an individual piece of data storage.
    - If you want to change one character in a file, you just change the block, or the piece of the file, that contains the character.
    - Use cases for block storage
        - Organizations that process time-sensitive and mission-critical transactions store such workloads into a low-latency, high-capacity, and fault-tolerant database. Block storage allows developers to set up a robust, scalable, and highly efficient transactional database.
        - Developers use block storage to store containerized applications on the cloud.
        - Block storage supports popular virtual machine (VM) hypervisors. Users can install the operating system, file system, and other computing resources on a block storage volume.
    + The AWS block storage portfolio consists of three types of block storage services: 
        + Amazon EBS
        + Amazon EC2 instance stores
        + FSx for ONTAP block storage volumes over an iSCSI access protocol
- Object storage
    - In object storage, files are stored as objects. Objects, much like files, are treated as a single, distinct unit of data when stored.
    - Changing just one character in an object is more difficult than with block storage. When you want to change one character in an object, the entire object must be updated.
    - Use cases for object storage
        - data arciving
        - backup and recovery
        - rich media: With object storage, you can accelerate applications and reduce the cost of storing rich media files such as videos, digital images, and music. By using storage classes and replication features, you can create cost-effective, globally replicated architecture to deliver media to distributed users.
![storage](storage.png)

# Amazon Elastic File System (Amazon EFS)
- Amazon Elastic File System (Amazon EFS) is a set-and-forget file system that automatically grows and shrinks as you add and remove files. 
- There is no need for provisioning or managing storage capacity and performance. 
- Amazon EFS can be used with AWS compute services and on-premises resources. 
- You can connect tens, hundreds, and even thousands of compute instances to an Amazon EFS file system at the same time, and Amazon EFS can provide consistent performance to each compute instance.
- You pay only for the storage used and you can choose from a range of storage classes designed to fit your use case. 
- EFS Standard and EFS Standard-Infrequent Access (Standard-IA) offer Multi-AZ resilience and the highest levels of durability and availability.
- EFS One Zone and EFS One Zone-Infrequent Access (EFS One Zone-IA) provide additional savings by saving your data in a single availability zone

# Amazon FSx 
- Amazon FSx is a fully managed service that offers reliability, security, scalability, and a broad set of capabilities that make it convenient and cost effective to launch, run, and scale high-performance file systems in the cloud.
- With Amazon FSx, you can choose between four widely used file systems: Lustre, NetApp ONTAP, OpenZFS, and Windows File Server

# Amazon EC2 instance store
- Amazon Elastic Compute Cloud (Amazon EC2) instance store provides temporary block-level storage for an instance. 
- This storage is located on disks that are physically attached to the host computer.
- This ties the lifecycle of the data to the lifecycle of the EC2 instance.
- If you delete the instance, the instance store is also deleted.
- Because of this, instance store is considered ephemeral storage.

# Amazon EBS
- As the name implies, Amazon Elastic Block Store (Amazon EBS) is block-level storage that you can attach to an Amazon EC2 instance. 
- Detachable: You can detach an EBS volume from one EC2 instance and attach it to another EC2 instance in the same Availability Zone to access the data on it.
- 1-to-1 connection: Most EBS volumes can only be connected with one computer at a time. Most EBS volumes have a one-to-one relationship with EC2 instances, so they cannot be shared by or attached to multiple instances at one time.
- AWS announced the Amazon EBS multi-attach feature that permits Provisioned IOPS SSD (io1 or io2) volumes to be attached to multiple EC2 instances at one time. This feature is not available for all instance types, and all instances must be in the same Availability Zone.
- Amazon EBS operates within a single Availability Zone. EBS volumes are located in the same Availability Zone as the EC2 instances that they are attached to.
- Amazon EBS use cases
    - operating system
    - database
    - enterprise applications
    - big data analytics engines
- EBS volumes are organized into two main categories: solid-state drives (SSDs) and hard-disk drives (HDDs). 
    - SSDs are used for transactional workloads with frequent read/write operations with small I/O size. 
    - HDDs are used for large streaming workloads that need high throughput performance.
- General Purpose SSD volumes： 
    - Provides a balance of price and performance for a wide variety of transactional workloads
    - Volume size 1 GiB–16 TiB
    - Max IOPS per volume 16,000
    - Max throughput per volume： gp3 1,000 MiB/s, gp2 250 MiB/s
    - Amazon EBS Multi-attach: Not supported
- Provisioned IOPS SSD volumes
    - Provides high-performance SSD designed for latency-sensitive transactional workloads
    - Volume size:io2 Block Express:  4 GiB–64 TiB  io1, io2: 4GiB–16 TiB
    - Max IOPS per volume: io2 Block Express: 256,000 , io1, io2: 64,000
    - Max throughput per volume： io2 Block Express: 4,000 MiB/s, io1, io2: 1000 MiB/s
    - Amazon EBS Multi-attach: supported
- Throughput Optimized HDD volumes
    - A low-cost HDD designed for frequently accessed, throughput-intensive workloads
    - Volume size: 125 GiB–16 TiB
    - Max IOPS per volume: 500
    - Max throughput per volume： 500 MiB/s
    - Amazon EBS Multi-attach: Not supported
- Cold HDD volumes
    - The lowest cost HDD designed for less frequently accessed workloads
    - Volume size: 125 GiB–16 TiB
    - Max IOPS per volume: 250
    - Max throughput per volume： 250 MiB/s
    - Amazon EBS Multi-attach: Not supported

# S3
- Object storage is built for the cloud and delivers virtually unlimited scalability, high durability, and cost effectiveness.
- Unlike Amazon EBS, Amazon Simple Storage Service (Amazon S3) is a standalone storage solution that isn’t tied to compute. With Amazon S3, you can retrieve your data from anywhere on the web.
- Amazon S3 provides object storage. Amazon S3 operates as a Regional service and is implemented across multiple Availability Zones by default. Amazon S3 is both highly available and highly durable object storage.

# User Case
- use cases for Amazon EBS storage, including enterprise applications, relational databases, nonrelational (NoSQL) databases, big data analytics, and file systems and media workflows.

# Amazon EFS
- Amazon EFS is a fully managed service providing NFS shared file system storage for Linux workloads.
- Amazon EFS supports the Network File System version 4 (NFSv4.1 and NFSv4.0) protocol. The applications and tools that you use today work seamlessly with Amazon EFS. Multiple compute modules can access an Amazon EFS file system at the same time. 
- Amazon EFS is for file storage using the Network File System (NFS) protocol. Amazon EFS operates as a Regional service and is implemented across multiple Availability Zones by default.
- Standard storage classes – EFS Standard and EFS Standard–Infrequent Access (Standard–IA), which offer multiple Availability Zones (Multi-AZ) resilience and the highest levels of durability and availability.
- One Zone storage classes – EFS One Zone and EFS One Zone–Infrequent Access (EFS One Zone–IA), which offer additional savings by choosing to save data in a single-Availability Zone (Single-AZ).
- User case
    - Containers and serverless persistent file storage
    - Move to managed file systems
    - Analytics and machine learning
    - Web serving and content management
    - Application testing and development
    - Media and entertainment
    - Database backups
# Amazon FSx for Lustre
- Use FSx for Lustre for workloads where speed matters, such as machine learning, high performance computing (HPC), video processing, and financial modeling.
- Amazon FSx for Lustre operates in a single Availability Zone.
- FSx for Lustre is a managed storage service developed on the open-source, high-performance Lustre file system. 
- The open-source Lustre file system is designed for compute-intensive applications that require a fast storage system capable of meeting throughput requirements. 
- It is also designed to meet input/output operations per second (IOPS) requirements at scale.
- FSx for Lustre was built to process large datasets quickly and cost-effectively and scale to meet growing demands.
- An FSx for Lustre file system is capable of delivering hundreds of gibibytes (GiB) per second of throughput and millions of IOPS.
- FSx for Lustre is POSIX compliant.
- User case
    - Horizontal – Machine learning
    - Horizontal – High performance computing
    - Vertical – Genomics and life sciences
    - Vertical – Media processing and transcoding
    - Vertical – Autonomous vehicles
    - Vertical – SAS Grid computing
# Amazon FSx for Windows File Server 
- Amazon FSx for Windows File Server is Single-AZ by default. However, Multi-AZ deployment is an option.
- You pay for the capacity that you provision. Performance characteristics are tied to the provisioned capacity. To increase performance, you can provision larger capacities.
- Amazon FSx for Windows File Server provides fully managed Microsoft Windows file servers, backed by a fully native Windows file system. Amazon FSx for Windows File Server has the features, performance, and compatibility to easily lift and shift enterprise applications to the AWS Cloud.
- To access file storage over a network, FSx for Windows File Server provides native support for Windows file system features and for the SMB protocol. Amazon FSx is optimized for enterprise applications in AWS with native Windows compatibility, enterprise performance and features, and consistent submillisecond latencies.
- Windows applications and workloads ideal for FSx for Windows File Server include the following:
    - Business applications
    - Home directories
    - Web serving
    - Content management
    - Data analytics
    - Software build setups
    - Media processing workloads
- FSx for Windows File Server use cases are similar to those for Amazon EFS. The key difference is that they apply to applications and workflows using SMB protocol instead of the NFS protocol. If you plan to use Windows-based applications, FSx for Windows File Server meets your requirements.
    - Home directories
    - Lift-and-shift Windows applications
    - Highly available Microsoft SQL Server deployments
    - Media workflows
    - Web serving and content management
    - Data analytics
# Amazon FSx for NetApp ONTAP
- With Amazon FSx for NetApp ONTAP, you can launch and scale reliable, high-performance, and feature-rich file storage built on NetApp's popular ONTAP file system. It provides the familiar features, performance, capabilities, and APIs of NetApp file systems with the agility, scalability, and simplicity of a fully managed AWS service. 
- Amazon FSx for NetApp ONTAP provides feature-rich, fast, and flexible shared file storage that’s broadly accessible from Linux, Windows, and macOS compute instances running in AWS or on premises. FSx for ONTAP supports block level storage over iSCSI and file storage using the NFS and SMB protocols.
- FSx for ONTAP offers high-performance SSD storage with sub-millisecond latencies, and makes it quick and easy to manage your data by enabling you to snapshot, clone, and replicate your files with the click of a button. 
- It also automatically tiers your data to lower-cost, elastic storage, eliminating the need to provision or manage capacity and allowing you to achieve SSD levels of performance for your workload while only paying for SSD storage for a small fraction of your data.
- With FSx for ONTAP, you get a fully managed file storage solution with:
    - Support for petabyte-scale data sets in a single namespace
    - Multiple gigabytes per second (GBps) of throughput per file system
    - Multi-protocol access to data using the NFS, SMB, and iSCSI protocols
    - High availability and durability with Multi-AZ deployments
    - Automatic data tiering that reduces storage costs by automatically transitioning infrequently-accessed data to a lower-cost storage tier based on your access patterns
    - Data compression, deduplication, and compaction to reduce your storage consumption
    - Support for NetApp's SnapMirror replication feature
    - Support for NetApp's on-premises caching solutions: NetApp Global File Cache and FlexCache
    - Support for access and management using native AWS or NetApp tools and APIs
        - AWS Management Console, CLI, and SDKs
        - NetApp ONTAP CLI, REST API, and Cloud Manager
    - Support for the following data protection and security features:
        - Encryption of file system data and backups at rest using KMS keys
        - Encryption of data in-transit using SMB Kerberos session keys
        - On-demand anti-virus scanning
        - Authentication and authorization using Active Directory
        - File access auditing
- FSx for ONTAP use cases are similar to those for Amazon EFS, Amazon FSx for Windows File Server, and Amazon FSx for OpenZFS. The key difference is that they apply multi-protocol access for applications and workflows using NFS and SMB protocols with an option for block storage using the iSCSI protocol. If you plan to use applications with multi-protocol access or migrated your existing NetApp ONTAP storage, FSx for ONTAP is your logical choice.
# Amazon FSx for OpenZFS
- Amazon FSx for OpenZFS is a fully managed file storage service that makes it easy to move data residing in on-premises ZFS or other Linux-based file servers to AWS without changing your application code or how you manage data. It offers highly reliable, scalable, high-performing, and feature-rich file storage built on the open-source OpenZFS file system. 
- FSx for OpenZFS file systems are accessible from Linux, Windows, and macOS compute instances and containers via the industry-standard NFS protocol (v3, v4, v4.1, and v4.2).
- Powered by the AWS Graviton family of processors along with the latest AWS disk and networking technologies, FSx for OpenZFS delivers up to 1 million IOPS, with latencies of a few hundred microseconds for your high-performance workloads. 
- FSx for OpenZFS use cases are similar to those for Amazon EFS, Amazon FSx for Windows File Server, and Amazon FSx for NetApp ONTAP. The key difference is that they apply multi-protocol access for applications and workflows using NFS and SMB protocols. If you plan to use applications with multi-protocol access or migrated your existing OpenZFS storage, FSx for OpenZFS is your logical choice.

# Edge and Hybrid Storage Solutions
- AWS edge computing services provide infrastructure and software that move data processing and analysis to where you are located. 
- AWS hybrid cloud solutions and services help you run and manage your applications wherever they may need to reside. 
- AWS provides edge infrastructure and software that moves data processing and analysis as close as necessary to where data is created
- Edge locations are remote locations outside of a normal on-premises data center. The locations often lack connectivity or have intermittent connectivity to the cloud. Often the applications require real-time or low-latency data collection and processing. 
- Hybrid cloud solutions are a blending of cloud resources with on-premises resources. The most common reasons for using hybrid cloud solutions include applications requiring low-latency connectivity to on-premises systems and data residency requirements.
    - One method is to use gateways to connect standard on-premises resources to resources in the cloud. 
    - Another method moves cloud-native technology to the on-premises location.
# AWS Snow Family
- The AWS Snow Family helps you to run operations in harsh, non-data center environments and in locations with inconsistent network connectivity. 
- The Snow Family is composed of AWS Snowcone, AWS Snowball, and AWS Snowmobile.
- Each device is designed to meet the unique compute and capacity challenges required by different use cases. 
- These services help physically transport up to exabytes of data into and out of AWS.
- AWS owns and manages AWS Snow Family devices. The devices integrate with AWS security, monitoring, storage management, and compute capabilities.
- AWS Snowcone for smaller data transfer jobs
- AWS Snowball Edge for transfer jobs between ~30 terabytes and 1 petabyte
- AWS Snowmobile from several petabytes to exabytes in scale
- The AWS Snow Family provides offline data transfers using physical devices. The AWS Snow Family physical devices are AWS Snowcone, AWS Snowball, and AWS Snowmobile.
## AWS Snowcone 
- A small, rugged, portable, secure edge computing, storage, and data transfer device.
- AWS Snowcone is the smallest member of the AWS Snow Family of edge computing and data transfer devices.
- You can use Snowcone to collect, process, and move data to AWS. 
- You can perform these operations offline by shipping the device to AWS, or online using AWS DataSync.
- AWS Snowcone stores data securely in edge locations. AWS Snowcone can run edge computing workloads that use AWS IoT Greengrass or Amazon Elastic Compute Cloud (Amazon EC2) instances.
- AWS Snowcone includes AWS DataSync installed only with a Local compute and storage job type. 
- AWS DataSync client included with Local compute and storage only job type.
- AWS Snowcone is formatted for Network File System (NFS) storage with an Import to Amazon S3 job type. Snowcone is formatted for Amazon Elastic Block Store (Amazon EBS) storage with a Local compute and storage job type. 
- Type
    - AWS Snowcone: Amazon EC2
    - AWS Snowcone SSD: Amazon EC2
    - AWS Snowcone comes in an 8TB HDD version and an 14TB SSD version.
- AWS Snowcone use cases
    - Transportation, logistics, and autonomous vehicles
    - Healthcare IoT
    - Industrial IoT

## AWS Snowball
- AWS Snowball – A rugged petabyte-scale data transport device with onboard storage and compute capabilities. AWS Snowball has different models of AWS Snowball Edge devices to choose from.
- Compute Optimized and Storage Optimized.
- AWS Snowball Edge Storage Optimized devices provide 24 vCPUs of compute capacity, coupled with 80 terabytes (TB) of usable block or Amazon S3-compatible object storage.
- AWS Snowball Edge Compute Optimized devices provide 52 vCPUs, 42 TB of usable block or object storage.
- Customers can use these two options for data collection, data processing with compute services, and storage in edge environments before shipping the device back to AWS. AWS Snowball devices work with or without the internet, do not require a dedicated IT operator, and are designed to be used in remote environments. Some examples of edge use case environments are: 
    - Intermittent connectivity (such as manufacturing, industrial, and transportation)
    - Extremely remote locations (such as military or maritime operations) 
- AWS Snowball Edge Storage Optimize: No compute
    - Snowball Edge storage-optimized (for data transfer) – This Snowball Edge device option has a 100 TB (80 TB usable) storage capacity.
    - Snowball Edge storage-optimized 210 TB – This Snowball Edge device option has 210 TB of usable storage space 
- AWS Snowball Edge Storage Optimized with compute: Amazon EC2 and AWS Lambda
    - This Snowball Edge device option has up to 80 TB of usable storage space, 40 vCPUs, and 80 GB of memory for compute functionality. It also comes with 1 TB of additional SSD storage space for block volumes attached to Amazon EC2-compatible AMIs.
- AWS Snowball Edge Compute Optimized: Amazon EC2 and AWS Lambda
    - Snowball Edge compute-optimized – This Snowball Edge device (with AMD EPYC Gen2) has the most compute functionality, with up to 104 vCPUs, 416 GB of memory, and 28 TB of dedicated NVMe SSD for compute instances.
    - Snowball Edge compute-optimized (with AMD EPYC Gen1) has up to 52 vCPUs, 208 GB of memory, 42 TB (39.5 TB usable) storage space, and 7.68 TB of dedicated NVMe SSD for compute instances.
    - Snowball Edge compute-optimized with GPU – This Snowball Edge device option is identical to the compute-optimized (with AMD EPYC Gen1) option and includes an installed graphics processing unit (GPU). The GPU is equivalent to the one available in the P3 Amazon EC2-compatible instance type.
- AWS Snowball Edge use cases
    - Machine learning
    - Manufacturing
    - Remote locations with simple data
- For the AWS Snowball service, a cluster is a collective of Snowball Edge devices used as a single logical unit for local storage and compute purposes.
## AWS Snowmobile 
- AWS Snowmobile – A large truck to migrate or transport exabyte-scale datasets into and out of the AWS Cloud. 
## Available job types
- Local compute and storage only – Choose this option to perform compute and storage workloads on the device without any data transferred into AWS when returned. AWS erases all data on the device securely.
- Import into Amazon S3 – Choose this option to have AWS ship an empty Snowball Edge device to you. You can use this device for data collection and local processing. When you return the device to AWS, your data is uploaded to your Amazon S3 bucket selected during job creation. After your data is imported into Amazon S3, your data is securely erased from the device.
- Export from Amazon S3 – Choose this option to export data from your Amazon S3 bucket to your device. AWS loads your data on the device and ships it to you. After the device arrives, you copy data from your device to your local storage. When you are done, ship the device to AWS, and your data is securely erased from the device.
## User case
- You require a lightweight device that fits in a backpack to collect data in a remote location. AWS Snowcone could be the appropriate solution.
- Your use case has limited data transfer requirements with intensive data collection and local processing requirements using Amazon EC2 and AWS Lambda compute. AWS Snowball Edge Compute  Optimize could be the appropriate solution.
- Verification is performed after the power is switched on and before the Snowball Edge device is ready to be used. 

# AWS Outposts
- AWS Outposts is a fully managed service that extends AWS infrastructure, services, APIs, and tools to your premises.
- Instances in Outpost subnets communicate with other instances in the AWS Region using private IP addresses, all within the same virtual private cloud (VPC).
- AWS installs your Outpost at your customer-managed physical buildings. A site must meet the facility, networking, and power requirements for your Outpost. Each configuration has unique power, cooling, and weight support requirements. 
- An Outpost requires connectivity to an AWS Region. A service link is a network route that enables communication between your Outpost and its associated AWS Region. Each Outpost is an extension of an Availability Zone and its associated Region. 
- You can create the following resources on your Outpost to support low-latency workloads that must run in proximity to on-premises data and applications: 
    - Amazon EC2 instances and EBS volumes
    - Amazon ECS clusters
    - Amazon Elastic Kubernetes Service (Amazon EKS) nodes 
    - Amazon ElastiCache instances using Amazon ElastiCache for Redis or Amazon ElastiCache for Memcached
    - Amazon EMR clusters
    - Amazon RDS database instances
    - Amazon S3 buckets using Amazon S3 on AWS Outposts
    - Application Load Balancers
    - AWS App Mesh Envoy proxy
- AWS Outposts addresses a wide variety of uses cases that require low-latency or localized data processing and storage.
    - Low-latency compute
    - Local data processing
    - Data residency
    - Migration and modernization

# AWS Storage Gateway
- AWS Storage Gateway is a hybrid solution that connects an on-premises software appliance with cloud-based storage.
- Storage Gateway provides seamless integration with data security features between your on-premises IT environment and the AWS storage infrastructure. 
- You can use the service to store data in the AWS Cloud for scalable and cost-effective storage that helps maintain data security.
- Storage Gateway offers file-based file gateways (Amazon S3 File and Amazon FSx File), volume-based (Cached and Stored), and tape-based storage solutions.
- Use cases include moving backups to the cloud, using on-premises file shares backed by cloud storage, and providing low-latency access to data in AWS for on-premises applications.
- The local gateway appliance maintains a cache of recently written or read data so that your applications can have low-latency access to data that is stored durably in AWS. 
- Storage Gateway offers the following types of storage gateways:
    - Amazon S3 File Gateway
        - With Amazon S3 File Gateway (S3 File Gateway), you can store files as objects in Amazon S3 using the open-standard Network File System (NFS) and Server Message Block (SMB) file protocols. 
    - Amazon FSx File Gateway
        - Amazon FSx File Gateway (FSx File Gateway) provides fast, low-latency on-premises access to file shares in the cloud using the open-standard SMB protocol.
        - For centralized backup and retention, you can use AWS Backup.
    - Tape Gateway
        - Tape Gateway presents a virtual tape library (VTL) to your backup application using storage open standard iSCSI protocol.
        - Each virtual tape is stored in Amazon S3. When you no longer require immediate or frequent access to data contained on a virtual tape, you can use your backup application move it from the Storage Gateway VTL into an archive tier that sits on top of Amazon S3 Glacier or Amazon S3 Glacier Deep Archive cloud storage.
        - Data is stored in an AWS managed Amazon S3 bucket.
    - Volume Gateway
        - Volume Gateway presents volumes for your applications block storage using the iSCSI protocol. Data written to these volumes can be asynchronously backed up as point-in-time snapshots of your volumes and stored in the cloud as Amazon EBS snapshots.
        - Using AWS Backup with Volume Gateway together helps you centralize backup management, reduce your operational burden, and meet compliance requirements. Back up volumes using service-native scheduler or AWS Backup service.
        - Data written to these volumes can be asynchronously backed up as point-in-time snapshots of your volumes.
        - Snapshots are stored in AWS as Amazon EBS snapshots.
- features
    - Fully managed cache
        - The local gateway appliance maintains a cache of recently written or read data so that your applications can have low-latency access to data that is stored durably in AWS. The gateways use a read-through and write-back cache. The cache commits data locally, acknowledges the write operations, and then asynchronously copies data to AWS, all while reducing application latency.
- Use cases
    - Low-latency access for on-premises applications to the cloud
    - Use on-premises file shares backed by cloud storage
    - Move backups to the cloud
    - Data protection and disaster recovery

# AWS Transfer Family
- The workload is about transferring files by internal or external clients or resources. Using this capability, you can lift and shift your current on-premises SFTP, FTPS, and FTP solutions to AWS.
- The AWS Transfer Family is designed to replace on-premises systems for file transfer workflows.
- AWS Transfer Family is for data transfer workflows.
- The AWS Transfer Family provides fully managed support for file transfers directly into and out of Amazon Simple Storage Service (Amazon S3) or Amazon Elastic File System (Amazon EFS). 
- AWS Transfer Family supports Secure File Transfer Protocol (SFTP), File Transfer Protocol Secure (FTPS), and File Transfer Protocol (FTP). 
- With AWS Transfer Family, you get access to a file transfer, protocol-enabled server in AWS without the need to run any server infrastructure.  
- With AWS Transfer Family, you can preserve your existing data exchange processes while taking advantage of the superior economics, data durability, and security of Amazon S3 or Amazon EFS. From the AWS Transfer Family console, you can perform the following actions:
    - Select one or more protocols
    - Configure Amazon S3 buckets or Amazon EFS file systems to store the transferred data
    - Set up your user authentication
        - You can import your existing user credentials or integrate an identity provider such as Microsoft Active Directory or LDAP. 
# AWS DataSync
- AWS DataSync synchronizes your data between a source data location or service and a destination location or service.
- Data synchronization is asynchronous, one-way at a time. Synchronization can go in either direction in or out of a storage service.
- AWS DataSync can be scheduled or run on demand.
- AWS DataSync is used to asynchronously transfer data between supported source and target storage resources.
- DataSync can copy data between the following systems:
    - Network File System (NFS) shares
    - Server Message Block (SMB) shares
    - Self-managed object storage
    - AWS Snowcone
    - Amazon S3 buckets
    - Amazon EFS file systems
    - Amazon FSx for Windows File Server file systems
- Connections between the local DataSync agent and the in-cloud service components are multi-threaded, maximizing performance over your Wide Area Network (WAN). A single DataSync task can fully use 10 Gbps over a network link between your on-premises environment and AWS.
# AWS Application Migration Service (AWS MGN)
- AWS Application Migration Service (AWS MGN), formerly CloudEndure Migration, provides a migration service between your servers and AWS services.
- With AWS Application Migration Service (AWS MGN), you can quickly realize the benefits of migrating applications to the cloud without changes and with minimal downtime.
- AWS MGN is the primary migration service recommended for lift-and-shift migrations to AWS. If you are currently using CloudEndure Migration or AWS Server Migration Service (AWS SMS), you are encouraged to switch to AWS MGN for future migrations. 
- You can use AWS MGN to migrate your on-premises applications from both physical and virtual infrastructure in to AWS. AWS MGN supports migrations from VMware vSphere, Microsoft Hyper-V, Amazon EC2, and other clouds to AWS.
- AWS MGN provides similar capabilities as CloudEndure Migration, but it is available on the AWS Management Console. Because AWS MGN is available from the console, it can integrate easily with other AWS services, such as AWS CloudTrail, Amazon CloudWatch, and IAM.
- How it works
    - Implementation begins by installing the AWS Replication Agent on your source servers. After the agent is installed, you can view and define replication settings. AWS MGN uses these settings to create and manage a Staging Area Subnet. This subnet includes lightweight Amazon EC2 instances that act as replication servers and low-cost staging Amazon EBS volumes.
    - Replication Servers receive data from the agent running on your source servers and write this data to the staging Amazon EBS volumes
    - AWS MGN keeps your source servers up to date on AWS by using continuous, block-level data replication. 
    - Testing and cutover。When you launch Test or Cutover instances, AWS MGN converts your source servers to boot and run natively on AWS automatically. After confirming that your launched instances are operating properly on AWS, you can decommission your source servers. You can then choose to modernize your applications by using additional AWS services and capabilities.
    - For each source server that you want to migrate, you can use AWS MGN for a free period of 2,160 hours, which is 90 days when used continuously.
    - The free period starts as soon as you install the AWS Replication Agent on your source server and continues during active source server replication. 

# AWS Backup
- Use AWS Backup to centralize and automate data protection across AWS services. AWS Backup offers a cost-effective, fully managed, policy-based service that further simplifies data protection at scale.
- AWS Backup is a fully managed data protection service that makes it easy to centralize and automate across AWS services, in the cloud, and on premises. Using this service, you can configure backup policies and monitor activity for your AWS resources in one place. 
- Using the AWS Backup console, you can quickly automate your data protection policies and schedules.
- AWS Backup supports several AWS services, including compute, storage, and database services.
- Compute services
    - Amazon Elastic Compute Cloud (Amazon EC2) instances, including EC2 instances store-backed instances
    - Windows Volume Shadow Copy Service (VSS) on Amazon EC2
- Storage services
    - Amazon Elastic Block Store (Amazon EBS)
    - Amazon Elastic File System (Amazon EFS)
    - Amazon Simple Storage Service (Amazon S3)
    - Amazon FSx for Windows File Server
    - Amazon FSx for Lustre
    - AWS Storage Gateway volumes – Volume Gateway
- Database services
    - Amazon Relational Database Service (Amazon RDS) databases, including all database engines
    - Amazon Aurora clusters
    - Amazon DynamoDB tables
    - Amazon Neptune databases
    - Amazon DocumentDB (with MongoDB compatibility) databases 
- AWS Backup features
    - Centralized backup management
    - Policy-based backup
    - Automated backup scheduling
    - Automated retention management
    - Lifecycle management policies
    - Incremental backups
    - Cross-Region backup
    - Cross-account management and backup
    - Backup activity monitoring
    - Secure data
    - Compliance
# Amazon EBS snapshots
- Using Amazon EBS Snapshots, you can back up the data on your Amazon EBS volumes to Amazon S3 by taking point-in-time snapshot copies. Snapshots are incremental copies of the data, which means that only the blocks on your EBS volumes that have changed after your most recent snapshot are saved. 

# Amazon FSx for Lustre snapshots
- With FSx for Lustre, you can create automatic daily backups and manual backups of persistent file systems that are not linked to an Amazon S3 durable data repository. 
- To provide high durability, FSx for Lustre stores your backups in Amazon S3 with 99.999999999 per

# CloudEndure Disaster Recovery
-  CloudEndure Disaster Recovery uses the same replication method to stage copies of your on-premises applications to cost-effective Amazon EC2 instances and Amazon EBS storage.
- Like AWS Application Migration Service, CloudEndure Disaster Recovery uses Amazon EBS to copy the operating system, application files, and data to AWS. The on-premises block data is replicated to the EBS volumes.
- CloudEndure Disaster Recovery minimizes downtime and data loss by providing fast, reliable recovery of physical, virtual, and cloud-based servers into AWS Cloud, including AWS Regions, AWS GovCloud (US), and AWS Outposts.
- You can use CloudEndure Disaster Recovery to protect your most critical databases, including Oracle, MySQL, and SQL Server, and enterprise applications such as SAP.
- CloudEndure Disaster Recovery continuously replicates your machines into a low-cost staging area in your target AWS account and preferred Region.
- The replication includes operating system, system state configuration, databases, applications, and files. In the case of a disaster, you can instruct CloudEndure Disaster Recovery to automatically launch thousands of your machines in their fully provisioned state in minutes.
- After your on-premises systems are restored to an operational ready state, CloudEndure Disaster Recovery updates those systems with current information and performs a managed failback operation.