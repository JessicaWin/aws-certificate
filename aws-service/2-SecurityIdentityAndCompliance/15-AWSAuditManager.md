# Overview
+ AWS Audit Manager helps you **continually audit your AWS usage** to simplify how you manage risk and compliance with regulations and industry standards.
+ Audit Manager **automates evidence collection** so you can more easily assess whether your policies, procedures, and activities—also known as controls—are operating effectively.
+ When it's time for an audit, Audit Manager helps you **manage stakeholder reviews of your controls**. This means that you can build audit-ready reports with much less manual effort.
+ Audit Manager provides **prebuilt frameworks that structure and automate assessments** for a given compliance standard or regulation.
+ You can create an assessment from any framework. When you create an assessment, Audit Manager automatically runs resource assessments.
# Features of Audit Manager
+ **Get started quickly** — Create your first assessment by selecting from a gallery of prebuilt frameworks that support a range of compliance standards and regulations. Then, initiate automatic evidence collection to audit your AWS service usage.
+ **Upload and manage evidence from hybrid or multicloud environments** — In addition to the evidence that Audit Manager collects from your AWS environment, you can also **upload and centrally manage evidence from your on-premises or multicloud environment**.
+ **Support common compliance standards and regulations** — Choose one of the AWS Audit Manager standard frameworks. These frameworks provide prebuilt control mappings for common compliance standards and regulations. These include the CIS Foundation Benchmark, PCI DSS, GDPR, HIPAA, SOC2, GxP, and AWS operational best practices.
+ **Monitor your active assessments** — Use the Audit Manager dashboard to view analytics data for your active assessments, and quickly identify non-compliant evidence that needs to be remediated.
+ **Search for evidence** — Use the **evidence finder feature** to quickly find evidence that’s relevant to your search query. You can generate an assessment report from your search results, or export your search results in CSV format.
+ **Create custom controls** — Create your own control from scratch or customize an existing control to meet your needs. You can also use the custom controls feature to create risk assessment questions and store the responses to those questions as manual evidence.
+ **Customize frameworks** — Create your own frameworks with standard or custom controls based on your specific requirements for internal audits.
+ **Share custom frameworks** — Share your custom Audit Manager frameworks with another AWS account, or replicate them into another AWS Region under your own account.
+ **Support cross-team collaboration** — Delegate control sets to subject matter experts who can review related evidence, add comments, and update the status of each control.
+ **Create reports for auditors** — Generate assessment reports that summarize the relevant evidence that's collected for your audit and link to folders that contain the detailed evidence.
+ **Ensure evidence integrity** — Store evidence in a secure location, where it remains unaltered.
# concepts and terminology
## Assessment
+ You can use an Audit Manager assessment to **automatically collect evidence that’s relevant for an audit**.
+ An assessment is based on a framework, which is **a grouping of controls** that are related to your audit.
+ When you create an assessment, Audit Manager automatically starts to assess resources in your AWS accounts and services based on the controls that are defined in the framework. Next, it collects the relevant evidence and converts it into an auditor-friendly format. After doing this, it then attaches the evidence to the controls in your assessment. When it's time for an audit, you—or a delegate of your choice—can review the collected evidence and then add it to an assessment report. This assessment report helps you to demonstrate that your controls are working as intended.
## Assessment report
+ An assessment report is a finalized document that's generated from an Audit Manager assessment.
## Assessment report destination
An assessment report destination is the default S3 bucket where Audit Manager saves your assessment reports.
## Audit
+ An audit is an independent examination of the assets, operations, or business integrity of your organization. 
## Audit owner
+ The term audit owner has two different meanings depending on the context.
+ In the context of Audit Manager, an audit owner is a user or role that manages an assessment and its related resources. The responsibilities of this Audit Manager persona include creating assessments, reviewing evidence, and generating assessment reports. 
+ In business terms, an audit owner is someone who coordinates and oversees the audit readiness efforts of their company, and presents evidence to an auditor. Typically, this is a governance, risk, and compliance (GRC) professional, such as a Compliance Officer or a GDPR Data Protection Officer
## Changelog
+ For each control in an assessment, Audit Manager captures changelogs to track user activity for that control.
## Cloud compliance
+ Cloud compliance is the general principle that cloud-delivered systems must be compliant with the standards that are faced by cloud customers.
## Compliance regulation
+ A compliance regulation is a law, rule, or other order that's prescribed by an authority, typically to regulate conduct. One example is GDPR.
## Compliance standard
+ A compliance standard is a structured set of guidelines that detail the processes of an organization for maintaining accordance with established regulations, specifications, or legislation.
## Control
+ A control is a safeguard or countermeasure that’s prescribed for an information system or an organization. Controls are designed to protect the confidentiality, integrity, and availability of your information, and to meet a set of defined security requirements.
## Control domains
+ You can think of a control domain as a general category of controls that **isn’t specific to any one framework**.
+ Control domain groupings are one of the most powerful features of the Audit Manager dashboard.
+ Audit Manager highlights the controls in your assessments that have non-compliant evidence, and **groups them by control domain**. 
+ This enables you to focus your remediation efforts on specific subject domains as you prepare for an audit.
## Data source
+ Audit Manager uses a data source to collect evidence for a control. 
+ A **Data source type** defines where Audit Manager collects evidence from for a control.  If you upload your own evidence, the data source type is **Manual**. If Audit Manager collects the evidence on your behalf, the data source type is one of the following: **AWS Security Hub, AWS Config, AWS CloudTrail, or AWS API calls**.
+ A **Mapping** is a specific keyword that relates to a data source type. For example, this might be a CloudTrail event name or an AWS Config name.
+ A **Data source name** is a name that's given to a data source.
+ A single control can have multiple data source types and multiple mappings. For example, one control might collect evidence from a mixture of data source types (such as AWS Config and Security Hub). Another control might have AWS Config as its only data source type, with multiple AWS Config rules as mappings.
## Delegate
+ A delegate is an AWS Audit Manager user with limited permissions. Delegates typically have specialized business or technical expertise. 
## Evidence
+ Evidence is a record that contains the information that's needed to demonstrate compliance with a control's requirements
+ Automated evidence — This is the evidence that Audit Manager collects automatically. 
    + Compliance check
    + User activity
    + Configuration data
+ Manual evidence — This is the evidence that you add to Audit Manager yourself. There are three ways to add your own evidence:
    + Import a file from Amazon S3
    + Upload a file from your browser
    + Enter a text response to a risk assessment question
## Evidence collection method
+ Automated controls
+ Manual controls
## Export destination
+ An export destination is the default S3 bucket where Audit Manager saves the files that you export from evidence finder. 
## Framework
+ An Audit Manager framework is a file that's used to structure and automate assessments for a specific standard or risk governance principle. These frameworks help map your AWS resources to the requirements in a control.
## Framework sharing
+ You can use the custom framework sharing feature of Audit Manager to quickly share your custom frameworks across AWS accounts and Regions. To share a custom framework, you create a share request. 
## Resource
+ A resource is a physical or information asset that's assessed in an audit.
## Resource assessment
+ A resource assessment is the process of assessing an individual resource. This assessment is based on the requirement of a control. 
## Resource compliance
+ Resource compliance refers to the evaluation status of a resource that was assessed when collecting compliance check evidence.
+ Non-compliant
+ Compliant
+ Inconclusive 
## Service in scope
+ This is an AWS service that's included in the scope of your assessment
# How AWS Audit Manager collects evidence
## 1. Assessing a resource from the data source
+ To start evidence collection, Audit Manager assesses an in-scope resource from a data source.
+ It does this by capturing a configuration snapshot, a related compliance check result, and any user activities.
+ It then runs an analysis to determine which control this data supports.
+ The result of the resource assessment is then saved and converted into evidence.
## 2. Converting assessment results to evidence
+ The result of the resource assessment contains both the original data that's captured from that resource, and the metadata that indicates which control the data supports.
+ AWS Audit Manager converts the original data into an auditor-friendly format.
+ The converted data and metadata are then saved as Audit Manager evidence before being attached to a control.
## 3. Attaching evidence to the related control
+ Audit Manager reads the evidence metadata.
+ Then, it attaches the saved evidence to a related control within the assessment.
+ The attached evidence becomes visible in Audit Manager.
+ This completes the cycle of a resource assessment.
# Integrations with related AWS services
+ AWS Security Hub
+ AWS CloudTrail
+ AWS Config
+ AWS License Manager
+ AWS Control Tower
+ AWS Artifact
# Integrations with third-party GRC products
+ If your company uses a hybrid cloud model or multicloud model, it’s likely that you use a GRC product to manage evidence from those environments. When that product is integrated with Audit Manager, you can pull evidence about your AWS usage directly into your GRC environment. This simplifies how you manage compliance by providing you with a centralized place to review and remediate evidence as you prepare for audits.
## Understanding how third-party integrations work with Audit Manager
+ GRC partners can use the Audit Manager public APIs to integrate their products with Audit Manager. With this integration in place, you can map the enterprise controls in your GRC environment to the controls that Audit Manager provides.
+ After you complete this one-time control mapping exercise, you can create Audit Manager assessments directly in the GRC product. This action starts the collection of evidence about your AWS usage. You can then see this AWS evidence along with the other evidence that’s collected from your hybrid environment, all within the same context of your enterprise controls.
## Third-party GRC partner products that integrate with Audit Manager
+ The following third party GRC products can ingest evidence from Audit Manager.
+ MetricStream
# Notifications in AWS Audit Manager
+ AWS Audit Manager can notify you about user actions through Amazon Simple Notification Service (Amazon SNS).
+ Audit Manager sends notifications when one of the following events occurs:
+ An audit owner delegates a control set for review.
+ A delegate submits a reviewed control set back to the audit owner.
+ An audit owner completes the review of a control set.
# What are typical use cases for Audit Manager?
+ ransition from manual to automated evidence collection
+ Continuous auditing and compliance
+ Internal risk and compliance assessments
+ Evidence to test specific controls efficacy

# ​Reference
+ [AWS Audit Manager](https://docs.aws.amazon.com/audit-manager/latest/userguide/what-is.html)
+ [Getting Started with AWS Audit Manager](https://explore.skillbuilder.aws/learn/course/14905/play/70102/getting-started-with-aws-audit-manager)
