# Overview
+ AWS WAF is a **web application firewall** that lets you **monitor the HTTP and HTTPS requests** that are forwarded to an **Amazon CloudFront distribution, an Amazon API Gateway REST API, an Application Load Balancer, or an AWS AppSync GraphQL API**.
    + AWS WAF also lets you **control access to your content**. 
    + Based on conditions that you specify, such as the IP addresses that requests originate from or the values of query strings, Amazon CloudFront, Amazon API Gateway, Application Load Balancer, or AWS AppSync responds to requests **either with the requested content or with an HTTP 403 status code** (Forbidden).
    + At the simplest level, AWS WAF lets you choose one of the following behaviors: 
        + Allow all requests except the ones that you specify 
        + Block all requests except the ones that you specify
        + Count requests that match your criteria 
        + Run CAPTCHA checks against requests that match your criteria – You can implement CAPTCHA controls against requests to help reduce bot traffic to your protected resources.
    + You can use **AWS WAF web access control lists (web ACLs)** to help minimize the effects of a distributed denial of service (**DDoS) attack**.
+ For **additional protection against DDoS attacks**, AWS also provides **AWS Shield Standard** and **AWS Shield Advanced**. 
    + AWS Shield Standard **is automatically included at no extra cost beyond what you already pay for AWS WAF** and your other AWS services.
    + AWS Shield Advanced provides **expanded DDoS attack protection** for your Amazon EC2 instances, Elastic Load Balancing load balancers, CloudFront distributions, Route 53 hosted zones, and AWS Global Accelerator accelerators.
    + **AWS Shield Advanced incurs additional charges**.
+ AWS Firewall Manager **simplifies your administration and maintenance tasks across multiple accounts and resources** for a variety of protections, including AWS WAF, AWS Shield Advanced, Amazon VPC security groups, AWS Network Firewall, and Amazon Route 53 Resolver DNS Firewall. 
    + With Firewall Manager, **you set up your protections just once and the service automatically applies them across your accounts and resources**, even as you add new accounts and resources.
# Which should I choose
+ It **all starts with AWS WAF**.
+ You can **automate and then simplify AWS WAF management using AWS Firewall Manager**.
+ **Shield Advanced adds additional features on top of AWS WAF**, such as dedicated support from the Shield Response Team (SRT) and advanced reporting.
+ If you want granular control over the protection that is added to your resources, AWS WAF alone is the right choice.
+ If you want to **use AWS WAF across accounts, accelerate your AWS WAF configuration, or automate protection of new resources, use Firewall Manager with AWS WAF**.
+ Finally, if you own high visibility websites or are otherwise prone to **frequent DDoS attacks**, you should consider purchasing the additional features that Shield Advanced provides.
# AWS WAF
+ [AWS-Web-Application-Firewall](./images/AWS-Web-Application-Firewall.png)
## **Benefits**
+ **Additional protection against web attacks** using conditions that you specify.
+ **Rules that can allow, block, or count web requests** that meet the specified conditions. Alternatively, rules can block or count web requests that not only meet the specified conditions, but also exceed a specified number of requests in any 5-minute period.
+ **Rules that you can reuse** for multiple web applications.
+ **Managed rule groups** from AWS and AWS Marketplace sellers.
+ **Real-time metrics** and sampled web requests.
+ **Automated administration** using the AWS WAF API.
## How AWS WAF works
+ **Web ACLs**  
    + You use a web access control list (ACL) to protect a set of AWS resources.+ You create a web ACL and **define its protection strategy by adding rules**. 
+ **Rules**
    + Each rule contains a statement that defines **the inspection criteria, and an action to take** if a web request meets the criteria.
    + When a web request meets the criteria, that's a match.
    + You can configure rules to **block matching requests, allow them through, count them, or run CAPTCHA controls against them**.
    + You can define conditions by using characteristics of web requests such as the following: 
        + IP addresses that requests originate from.
        + Country that requests originate from.
        + Values in request headers.
        + Strings that appear in requests, either specific strings or strings that match regular expression (regex) patterns.
        + Length of requests.
        + Presence of SQL code that is likely to be malicious (known as *SQL injection*).
        + Presence of a script that is likely to be malicious (known as *cross-site scripting*).
    + Rules don't exist in AWS WAF on their own. **They aren't AWS resources**, and they don't have Amazon Resource Names (ARNs). You can **access a rule by name in the rule group or web ACL where it's defined**. 
    + Rule action: 
        + **Count**
            + AWS WAF **counts the request but doesn't determine whether to allow it or block it**.
            + With this action, AWS WAF **continues processing the remaining rules** in the web ACL.
            + You can **insert custom headers** into the request and you can **add labels** that other rules can match against.
        + **Allow**
            + AWS WAF allows the request to be **forwarded to** the protected AWS resource for processing and response.
            + You can **insert custom headers** into the request before forwarding it to the protected resource.
        + **Block**
            + AWS WAF **blocks the request**.+ By default, the AWS resource responds with an HTTP `403 (Forbidden)` status code, but you can customize the response. 
        + **CAPTCHA**
            + AWS WAF runs a CAPTCHA check against the request.
            + The action that AWS WAF takes on the request can be terminating or non-terminating, depending on the results of the check:
            + **CAPTCHA** stands for Completely Automated Public Turing test to **tell Computers and Humans Apart**. CAPTCHA challenges are designed to verify that a human is sending requests and to prevent activity like web scraping, credential stuffing, and spam.
    + Label 
        + When a web request matches a rule, AWS WAF **adds the rule's labels to the request**.
        + The labels remain available on the request as long as AWS WAF is evaluating it against the web ACL.
        + Rules that run later in the web ACL can match against the label by using a **label match statement**.
        + Labels allow you to **evaluate and collect information for multiple rules before taking an action** of allow or block on the web request.
    + For rules that **inspect the web request body**, AWS WAF can **inspect the first 8 KB (8,192 bytes)**, but not beyond. 
+ **Rules groups**  
    + You can use rules individually or in reusable rule groups.
    + AWS Managed Rules and AWS Marketplace sellers provide managed rule groups for your use.
    + You can also define your own rule groups.
## **Resource types**
+ The **resource types that you can protect** using AWS WAF web ACLs are 
    + Amazon CloudFront distribution
    + Amazon API Gateway REST API
    + Application Load Balancer
    + AWS AppSync GraphQL API.
    + For an Amazon API Gateway REST API, an Application Load Balancer, or an AWS AppSync GraphQL API, you can use any of the Regions in the list. You can only associate a web ACL to an Application Load Balancer within AWS Regions. 
    + For a CloudFront distribution, AWS WAF is available globally, but you must use the Region US East (N. Virginia) for all of your work.
    + You can associate each AWS resource with only one web ACL. The relationship between web ACL and AWS resources is **one-to-many**.
    + You can associate a web ACL with one or more CloudFront distributions. You **cannot** associate a web ACL that you have associated with a CloudFront distribution with any other AWS resource type.
## **AWS WAF Web ACL capacity units (WCU)**
+ AWS WAF uses web ACL capacity units (WCU) to **calculate and control** the operating resources that are required to run your rules, rule groups, and web ACLs.
+ **Rule capacity** – AWS WAF calculates rule capacity when you create or update a rule.
+ **Rule group capacity** – AWS WAF requires that each rule group is assigned an immutable capacity at creation. 
+ **Web ACL capacity** – The maximum capacity for a web ACL is 1,500, which is sufficient for most use cases. 
## IP sets and regex pattern sets
+ AWS WAF **stores some more complex information in sets** that you use by referencing them in your rules.
+ Each of these sets has a name and is assigned an **Amazon Resource Name (ARN)** at creation.
+ An IP set provides **a collection of IP addresses and IP address ranges** that you want to use together in a rule statement.
+ A regex pattern set provides a collection of regular expressions that you want to use together in a rule statement.
## Customizing web requests and responses
+ With allow, count, and CAPTCHA actions, you can insert custom headers into the web request. When AWS WAF forwards the web request to the protected resource, the request contains the entire original request plus the custom headers that you've inserted. For the CAPTCHA action, AWS WAF only applies the customization if the request passes the CAPTCHA inspection.
+ With block actions, you can define a complete custom response, with response code, headers, and body. The protected resource responds to the request using the custom response provided by AWS WAF. Your custom response replaces the default block action response of `403 (Forbidden)`.
## Bot Control
+ Bot Control helps you **manage bot activity to your site by categorizing and identifying common bots**, verifying generally desirable bots, and detecting high confidence signatures of bots.
+ Bot Control is a **managed rule group** that gives you visibility and control over common and pervasive bot traffic to your applications.
+ With Bot Control, you can easily monitor, block, or rate-limit bots such as scrapers, scanners, and crawlers.
+ You can also allow common bots like status monitors and search engines. 
## Logging and monitoring web ACL traffic
+ You can enable logging to get detailed information about traffic that is analyzed by your web ACL.
+ Logged information includes the time that AWS WAF received a web request from your AWS resource, detailed information about the request, and details about the rules that the request matched
+ You can send your logs to an Amazon CloudWatch Logs log group, an Amazon Simple Storage Service (Amazon S3) bucket, or an Amazon Kinesis Data Firehose.
# AWS Firewall Manager
+ AWS Firewall Manager **simplifies your administration and maintenance tasks across multiple accounts and resources** for a variety of protections, including AWS WAF, AWS Shield Advanced, Amazon VPC security groups, AWS Network Firewall, and Amazon Route 53 Resolver DNS Firewall.
+ With Firewall Manager, you set up your protections just once and the service automatically applies them across your accounts and resources, even as you add new accounts and resources.
## Benefits
+ Helps to protect resources across accounts
+ Helps to protect all resources of a particular type, such as all Amazon CloudFront distributions
+ Helps to protect all resources with specific tags
+ Automatically adds protection to resources that are added to your account
+ Allows you to subscribe all member accounts in an AWS Organizations organization to AWS Shield Advanced, and automatically subscribes new in-scope accounts that join the organization
+ Allows you to apply security group rules to all member accounts or specific subsets of accounts in an AWS Organizations organization, and automatically applies the rules to new in-scope accounts that join the organization+ Lets you use your own rules, or purchase managed rules from AWS Marketplace
## Prerequisites
+ To use Firewall Manager, your **account must be a member of the organization in the AWS Organizations** service where you want to use your Firewall Manager policies.
+ Set the AWS Firewall Manager administrator account. 
+ When you set the Firewall Manager administrator account, Firewall Manager automatically sets it as the AWS Organizations Delegated Administrator for Firewall Manager. This allows Firewall Manager to access information about the organizational units (OUs).
+ To use Firewall Manager, you must enable **AWS Config**.
+ To manage Firewall Manager Network Firewall and DNS Firewall policies, you must **enable sharing with AWS Organizations in AWS Resource Access Manager**.
+ To use Firewall Manager in a Region that's disabled by default, you must enable the Region for both the management account of your AWS organization and the Firewall Manager administrator account.
## Policies
+ policy type 
    + **AWS WAF policy** – Firewall Manager supports AWS WAF and AWS WAF Classic policies. For both versions, you define which resources are protected by the policy.
    + **Shield Advanced policy** – This policy applies AWS Shield Advanced protection to specified accounts and resources.
    + **Amazon VPC security group policy** – This type of policy gives you control over security groups that are in use throughout your organization in AWS Organizations and lets you enforce a baseline set of rules across your organization.
    + **Network Firewall policy** – This policy applies AWS Network Firewall protection to your **organization's VPCs**.
    + **Amazon Route 53 Resolver DNS Firewall policy** – This policy applies **DNS Firewall protections** to your organization's VPCs.
+ policy scope 
    + The policy scope defines **where the policy applies**.
    + You can either apply centrally controlled policies to **all** of your accounts and resources within your organization in AWS Organizations, or to **a subset** of your accounts and resources.
    + **AWS accounts in scope​​​​​​​​​​**
        + To all accounts in your organization
        + To only a specific list of included account numbers and AWS Organizations organizational units (OUs)
        + To all except a specific list of excluded account numbers and AWS Organizations organizational units (OUs)
    + **Resources in scope**
        + All resources
        + Resources that have **all of the tags** that you specify
        + All resources except those that have all of the tags that you specify
## AWS Firewall Manager findings
+ AWS Firewall Manager creates findings for resources that are out of compliance and for attacks that it detects and sends them to **AWS Security Hub**. 
+ When you use Security Hub and Firewall Manager, Firewall Manager **automatically** sends your findings to Security Hub. 
# AWS Shield
+ AWS provides AWS Shield Standard and AWS Shield Advanced for **protection against DDoS attacks**. 
+ **AWS Shield Standard is automatically included at no extra cost** beyond what you already pay for AWS WAF and your other AWS services.
+ For added protection against DDoS attacks, AWS offers **AWS Shield Advanced**. AWS Shield Advanced provides **expanded DDoS attack protection** for your resources.
## AWS Shield Standard
+ AWS Shield Standard defends against the **most common, frequently occurring network and transport layer DDoS attacks** that target your website or applications.
## AWS Shield Advanced
+ For **higher levels of protection** against attacks, you can subscribe to AWS Shield Advanced.
+ Shield Advanced offers advanced monitoring and protection for the following resource types: 
    + Amazon CloudFront distributions.
    + Amazon Route 53 hosted zones.
    + AWS Global Accelerator accelerators.
    + Amazon EC2 Elastic IP addresses. Shield Advanced protects whatever resource is associated with a protected Elastic IP address.
    + Elastic Load Balancing (ELB) load balancers, as follows: 
        + Application Load Balancers.
        + Classic Load Balancers.+ Network Load Balancers. You protect a Network Load Balancer by associating an Amazon EC2 Elastic IP address to it and then protecting the Elastic IP address with Shield Advanced. 
        + **Not supported: Gateway Load Balancers.**
+ Shield Advanced **health-based detection** uses the health of your AWS resource to improve responsiveness and accuracy in attack detection and mitigation. To use health-based detection, you **define the health check for your resource in Route 53 and then associate it with your Shield Advanced protection**. 
# Reference
[What are AWS WAF, AWS Shield, and AWS Firewall Manager? - AWS WAF, AWS Firewall Manager, and AWS Shield Advanced](https://docs.aws.amazon.com/waf/latest/developerguide/what-is-aws-waf.html)
