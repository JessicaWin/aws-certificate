# Amazon S3 Glacier
+ Amazon S3 Glacier is **a secure, durable, and extremely low-cost** Amazon S3 storage class for** data archiving and long-term backup**.
+ S3 Glacier is **one of the many different storage classes** for Amazon S3.
# **Data Model**
+ The Amazon S3 Glacier (S3 Glacier) data model core concepts include **vaults and archives**.
+ In S3 Glacier, a vault is a **container for storing archives**. 
+ You can store an **unlimited number of archives** in a vault.
+ Note that vault operations are **Region specific**. 
+ An AWS account can create up to **1,000 vaults per AWS Region**. 
+ An archive can be any data such as a photo, video, or document and is a base unit of storage in S3 Glacier. 
+  S3 Glacier **assigns the archive an ID, which is unique in the AWS Region in which it is stored.
+ **Upload archives in a single operation** – In a single operation, you can upload archives from **1 byte to up to 4 GB** in size. However, we encourage S3 Glacier customers to use **multipart upload** to upload archives **greater than 100 MB**
+ **Upload archives in parts** – Using the multipart upload API, you can upload large archives, up to about 40,000 GB (10,000 * 4 GB).
+ **AWS Snowball** accelerates moving large amounts of data into and out of AWS using Amazon-owned devices, bypassing the internet.
+ S3 Glacier **jobs** can perform a select query on an archive, retrieve an archive, or get an inventory of a vault.  
+ Retrieving an archive and vault inventory (list of archives) are **asynchronous operations** in S3 Glacier in which you first initiate a job, and then download the job output after S3 Glacier completes the job.
+ Because jobs take time to complete, S3 Glacier supports a notification mechanism to **notify you when a job is complete**.
#  Vault Lock
+ S3 Glacier Vault Lock allows you to easily deploy and enforce compliance controls for individual S3 Glacier vaults with a vault lock policy. You can specify controls such as “write once read many” (WORM) in a vault lock policy and lock the policy from future edits. Once locked, the policy can no longer be changed.
# Querying Archives
+ With S3 Glacier Select, you can perform filtering operations using simple Structured Query Language (SQL) statements directly on your data in S3 Glacier.
+ When you provide an SQL query for a S3 Glacier archive object, S3 Glacier Select runs the query in place and writes the output results to Amazon S3.
+ With S3 Glacier Select, you can run queries and custom analytics on your data that is stored in S3 Glacier, without having to restore your data to a hotter tier like Amazon S3.
# Retrieval Policies
+ **No Retrieval Limit policy**: no retrieval quota is set and all valid data retrieval requests are accepted.
+ **Free Tier Only policy**: you can keep your retrievals within your daily free tier allowance and not incur any data retrieval cost. 
+ **Max Retrieval Rate policy** to set a bytes-per-hour retrieval rate quota. ensures that the peak retrieval rate from all retrieval jobs across your account in an AWS Region does not exceed the bytes-per-hour quota you set.
# Reference
[amazon glacier](https://docs.aws.amazon.com/amazonglacier/latest/dev/introduction.html)
