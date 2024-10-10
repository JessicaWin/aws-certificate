# Overview
+ AWS CloudHSM provides **hardware security modules** in the AWS Cloud.
+ A hardware security module (HSM) is a **computing device that processes cryptographic operations and provides secure storage for cryptographic keys**.
+ When you use an HSM from AWS CloudHSM, you can perform a variety of cryptographic tasks: 
    + Generate, store, import, export, and **manage cryptographic keys**, including symmetric keys and asymmetric key pairs.
    + Use symmetric and asymmetric algorithms to **encrypt and decrypt data**.
    + Use cryptographic hash functions to **compute message digests and hash-based message authentication codes** (HMACs).
    + Cryptographically **sign data (including code signing) and verify signatures**.
    + Generate cryptographically **secure random data**.
# User Cases
+ Offloading reduces the computational burden on your web server and provides extra security by storing the server's private key in the HSMs.
+ Protect the Private Keys for an Issuing Certificate Authority (CA),  store the private key in the HSM in your AWS CloudHSM cluster, and use the HSM to perform the cryptographic signing operations.
+ Some versions of Oracle's database software offer a feature called Transparent Data Encryption (TDE). You can store the TDE master encryption key in the HSMs in your AWS CloudHSM cluster, which provides additional security.
# AWS CloudHSM Clusters
+ AWS CloudHSM provides hardware security modules (HSMs) in a *cluster*.
+ A cluster is **a collection of individual HSMs** that AWS CloudHSM **keeps in sync**.
+ You can create a cluster that has from **1 to 28 HSMs** (the [default limit](https://docs.aws.amazon.com/cloudhsm/latest/userguide/limits.html) is 6 HSMs per AWS account per AWS Region)
+ You can place the HSMs in **different Availability Zones** in an AWS Region.
+ Adding **more HSMs** to a cluster provides **higher performance**.
+ **Spreading clusters across Availability Zones** provides **redundancy and high availability**.
+ When you create a cluster, you specify an **Amazon Virtual Private Cloud** (VPC) in your AWS account and **one or more subnets in that VPC**.
+ When you create an AWS CloudHSM cluster with more than one HSM, you **automatically get load balancing**. 
+ AWS CloudHSM makes **periodic backups** of the users, keys, and policies in the cluster. The service stores backups in a service-controlled Amazon Simple Storage Service (Amazon S3) bucket in the same region as your cluster.
+ When AWS CloudHSM makes a backup from the HSM, the HSM **encrypts all of its data before sending it to AWS CloudHSM**. The data never leaves the HSM in plaintext form.
# Managing HSM Users and Keys
+ Unlike most AWS services and resources, you **do not use AWS Identity and Access Management** (IAM) users or IAM policies to access resources within your cluster.
+ Instead, you **use HSM users directly** on the hardware security module (HSM) with AWS CloudHSM.
+ Before you can use your AWS CloudHSM cluster for cryptoprocessing, you must **create users and keys** on the HSMs in your cluster.
+ The HSM authenticates each HSM user and each HSM user has a **type that determines which operations you can perform** on the HSM as that user. 
+ **precrypto officer (PRECO)**
    + The precrypto officer (PRECO) is a **temporary user** that exists only on the first HSM in an AWS CloudHSM cluster.
    + The PRECO user can only **change its own password and perform read-only operations** on the HSM.
    + You use the PRECO user to activate a cluster. To [activate a cluster](https://docs.aws.amazon.com/cloudhsm/latest/userguide/activate-cluster.html), you log in to the HSM and **change the PRECO user's password**.
    + When you change the password, the PRECO user **becomes the primary crypto officer (PCO)**.
+ **Crypto Officer (CO | PCO)**
    + A crypto officer (CO) can perform **user management operations**.
    + PCO is the designation for first CO you create, the primary CO. 
+ **Crypto User (CU)**
    + **Key management** – Create, delete, share, import, and export cryptographic keys.
    + **Cryptographic operations** – Use cryptographic keys for encryption, decryption, signing, verifying, and more.
+ Appliance User (AU) 
    + The appliance user (AU) can perform **cloning and synchronization operations**.
    + AWS CloudHSM uses the AU to **synchronize the HSMs in an AWS CloudHSM cluster**.
    + The AU exists on all HSMs provided by AWS CloudHSM, and has limited permissions. 
# Reference
[What Is AWS CloudHSM? - AWS CloudHSM](https://docs.aws.amazon.com/cloudhsm/latest/userguide/introduction.html)
