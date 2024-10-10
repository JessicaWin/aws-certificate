# Overview
+ AWS Transfer Family is a secure transfer service that enables you to transfer files into and out of AWS storage services
+ AWS Transfer Family supports transferring data from or to the following AWS storage services. 
    + Amazon Simple Storage Service (Amazon S3) storage. 
    + Amazon Elastic File System (Amazon EFS) Network File System (NFS) file system. 
+ AWS Transfer Family supports transferring data over the following protocols: 
    + File Transfer Protocol (FTP):Network protocol for transferring files over TCP/IP
        + Credentials sent in clear text without encryption
    + File Transfer Protocol Secure (FTPS): File transfer protocol over TCP/IP with SSL/TLS encryption
    + SSH or Secure File Transfer Protocol (SFTP): File transfer protocol over SSH using industry standard strong encryption algorithms
    + Applicability Statement 2 (AS2): HTTPS-based protocol to transmit messages (especially Electronic Data Interchange (EDI) messages) safely, cheaply, and quickly 
+ AWS Transfer Family supports any standard file transfer protocol client. Some commonly used clients are the following: 
    + OpenSSH – A Macintosh and Linux command line utility.
    + WinSCP – A Windows-only graphical client.
    + Cyberduck – A Linux, Macintosh, and Microsoft Windows graphical client
    + FileZilla – A Linux, Macintosh, and Windows graphical client.
# Architectural Components
## Users, clients, and trading partners
+ All managed file transfer workflows involve the exchange of files between **a user or application systems** and **the file transfer servers and associated storage systems**. Different workflows have different components. They range from individual users transferring files, to programmatic file transfers by applications, to trading partner applications or workflows.
    + **User**—An individually definable user, group, or system that uses a client application to transfer files using SFTP, FTPS, or FTP protocols.
    + **Client**—A file transfer application for performing file transfers using SFTP, FTPS, or FTP protocols.
    + **Application**—An application or workflow that has an embedded client that transfers files as part of the programming code using SFTP, FTPS, or FTP protocols.
    + **Trading partner application**—An application specifically designed for secure file transfers between trusted business partners as part of a trusted workflow using the AS2 protocol.
+ Transfer Family works with any of the common file transfer client applications. 
    + Open SSH—Available for Windows or Linux
    + WinSCP—Available for Windows only
    + Cyberduck—Available for Windows, Linux, and macOS
    + FileZilla—Available for Windows, Linux, and macOS
## Endpoints
+ To connect programmatically to an AWS service, you use an endpoint.
+ Public endpoints are available for workflows using SFTP protocol.
    + Public endpoints aren't contained within a VPC.
    + Openly reachable from the open or public internet using a specified URL.
+ VPC endpoints for external clients can be used with SFTP, FTPS, and AS2 protocols. 
    + Configured using public elastic IP address.
    + Configure in up to three Availability Zones per Region.
    + Security groups to configure your endpoint firewall for protocols and connections to and from your Transfer Family server.
+ VPC endpoint for internal clients can be used with SFTP, FTPS, FTP, and AS2 protocols. 
    + Configured using private IP addresses.
    + Configure in up to three Availability Zones per Region.
    + Security groups to configure your endpoint firewall for protocols and connections to and from your Transfer Family server.
## DNS
+ To reach the Transfer Family service, you implement DNS to redirect your URL name to the appropriate IP address for the Transfer Family endpoint. 
# User Cases
+ Common use cases for Transfer Family with Amazon S3 are the following: 
    + Data lakes in AWS for uploads from third parties such as vendors and partners.
    + Subscription-based data distribution with your customers.
    + Internal transfers within your organization.
+ The following are some common use cases for Transfer Family with Amazon EFS: 
    + Data distribution
    + Supply chain
    + Content management
    + Web serving applications
+ Common use cases with AS2 protocol
    + Workflows with compliance requirements that rely on having data protection and security features built into the protocol
    + Supply chain logistics
    + Payments workflows
    + B2B transactions
    + Integrations with ERP and customer relationship management (CRM) systems
+ Common use cases with workflow requirements
    + Modernizing secure file transfers with financial and healthcare institutions for regulated data like PCI, PII, or HIPPA
    + Archival compliance of original transferred files 
# Benefits
+ A fully managed service that **scales in real time** to meet your needs.
+ You **don't need to modify your applications** or run any file transfer protocol infrastructure.
+ With your data in durable Amazon S3 storage, you can **use native AWS services for processing, analytics, reporting, auditing, and archival functions**.
+ With Amazon EFS as your data store, you get **a fully managed elastic file system** for use with AWS Cloud services and on-premises resources. 
+ A fully managed, serverless File Transfer Workflow service that makes it easy to set up, run, automate, and monitor processing of files uploaded using AWS Transfer Family.+ There are **no upfront costs**, and you pay only for the use of the service.
+ Transfer Family supports common user authentication systems, including Microsoft Active Directory and LDAP. Alternatively, you can also choose to store and manage users’ credentials directly within the service. 
# How AWS Transfer Family works
+ With Transfer Family, you get access to a file transfer protocol-enabled server in AWS without the need to run any server infrastructure.
+ AWS Transfer Family supports up to 3 Availability Zones and is backed by an auto scaling, redundant fleet for your connection and transfer requests.
+ **Transfer Family Managed File Transfer Workflows**(MFTW) is a fully managed, **serverless File Transfer Workflow service** that makes it easy to set up, run, automate, and monitor processing of files uploaded using AWS Transfer Family.  
+ Customers can use MFTW to automate various processing steps such as copying, tagging, scanning, filtering, compressing/decompressing, and encrypting/decrypting the data that is transferred using Transfer Family. 
+ You can get started with AWS Transfer Family by creating a file transfer protocol-enabled server and then assigning users to use the server.
+ You can host your server's endpoint inside a virtual private cloud (VPC) to use for transferring data to and from an Amazon S3 bucket or Amazon EFS file system without going over the public internet.
# Reference
+ [AWS Transfer Family](https://docs.aws.amazon.com/transfer/latest/userguide/what-is-aws-transfer-family.html)
+ [AWS Transfer Family Primer](https://explore.skillbuilder.aws/learn/course/88/aws-transfer-family-primer)
