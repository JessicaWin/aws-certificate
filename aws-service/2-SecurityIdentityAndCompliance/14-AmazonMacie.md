# Overview
+ Amazon Macie is a fully managed **data security and data privacy service** that uses **machine learning and pattern matching** to help you **discover, monitor, and protect sensitive data** in your AWS environment.
+ Macie **automates the discovery of sensitive data**, such as personally identifiable information (PII) and financial data, to provide you with a better understanding of the data that your organization stores in Amazon Simple Storage Service (Amazon S3)
+ Macie also provides you with an inventory of your S3 buckets, and it **automatically evaluates and monitors** those buckets for security and access control.
+ If Macie detects sensitive data or potential issues with the security or privacy of your data, it **creates detailed findings** for you to review and remediate as necessary.
# Features of Amazon Macie
+ Automate the discovery of sensitive data 
    + With Macie, you can automate discovery and reporting of sensitive data by **creating sensitive data discovery jobs**
    + A sensitive data discovery job analyzes objects in S3 buckets to determine whether they contain sensitive data.
+ Discover a variety of sensitive data types
+ Evaluate and monitor data for security and access control
+ Review and analyze findings
+ Monitor and process findings with other services and systems 
    + ​​​​​​​​​​​​​​EventBridge
    + Security Hub
+ Centrally manage multiple Macie accounts 
    + ​​​​​​​integrating Macie with AWS Organizations
    + sending membership invitations from Macie
+ Develop and manage resources programmatically
# Discovering sensitive data
+ To discover sensitive data with Amazon Macie, you create and run **sensitive data discovery jobs**.
+ By creating and running sensitive data discovery jobs, you can **automate discovery, logging, and reporting of sensitive data** in your S3 buckets.
+ Each sensitive data discovery job can analyze objects by using **managed data identifiers** that Macie provides, **custom data identifiers** that you define, or **a combination of the two**
+ **managed data identifiers** can detect a large and growing list of sensitive data types for many countries and regions, including multiple types of financial data, personal health information (PHI), and personally identifiable information (PII)
+ **custom data identifiers** can detect sensitive data that **reflects your organization's particular scenarios**, intellectual property, or proprietary data
+ Macie can analyze an object if the following is true: 
    + The object uses a **supported file or storage format**. 
    + If the object is encrypted, it’s encrypted with a **key that Macie is allowed to use**.
    + The object is **stored directly in Amazon S3 and uses a supported storage class**—S3 Intelligent-Tiering, S3 One Zone-IA, S3 Standard, or S3 Standard-IA. 
    + Macie **can’t analyze data** that’s stored **in Amazon S3 Glacier or other AWS services**.
    + If the bucket has a restrictive bucket policy, the **policy allows Macie to access objects** in the bucket.
+ You can run a job only once, for on-demand analysis and assessment, or on a recurring basis for periodic analysis, assessment, and monitoring. 
+ Each sensitive data discovery job produces records of the sensitive data that it finds and the analysis that it performs—**sensitive data findings** and **sensitive data discovery results**. 
    + A *sensitive data finding* is **a detailed report of sensitive data that Macie found** in an object.
    + A *sensitive data discovery result* is a record that logs details about **the analysis of an object.** 
# Understanding Findings
+ Amazon Macie generates two categories of findings:**policy findings and sensitive data findings**.
+ **A policy finding** is a detailed report of **a potential policy violation** for an Amazon Simple Storage Service (Amazon S3) bucket.
+ **A sensitive data finding** is a **detailed report of sensitive data in an S3 object**
# **​​​​​​​Reference**
+ [What is Amazon Macie? - Amazon Macie](https://docs.aws.amazon.com/macie/latest/user/what-is-macie.html)
