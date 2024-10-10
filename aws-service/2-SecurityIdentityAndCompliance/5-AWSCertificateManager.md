# Overview
+ AWS Certificate Manager (ACM) handles the complexity of **creating, storing, and renewing public and private SSL/TLS X.509 certificates and keys** that protect your AWS websites and applications.
+ ACM certificates can secure **singular domain names, multiple specific domain names, wildcard domains, or combinations of these**.
+ ACM **wildcard certificates** can protect **an unlimited number of subdomains**.
# ACM certificate characteristics
+ **Managed Renewal and Deployment**
    + ACM manages the process of renewing ACM certificates and provisioning the certificates after they are renewed.
    + **Automatic renewal** can help you avoid downtime due to incorrectly configured, revoked, or expired certificates.
+ **Multiple Domain Names**
    + Each ACM certificate must include at least one fully qualified domain name (FQDN), and you can add additional names if you want.
+ **Wildcard Names**
    + ACM allows you to use an asterisk (*) in the domain name to create an ACM certificate containing a wildcard name that can **protect several sites in the same domain**. 
    + When you request a wildcard certificate, **the asterisk (`*`) must be in the leftmost position** of the domain name and can **protect only one subdomain level**. 
+ **Domain Validation (DV)**
    + Before the Amazon certificate authority (CA) can issue a certificate for your site, AWS Certificate Manager (ACM) must **prove that you own or control all of the domain names that you specify** in your request.
    + DNS validation 
        + When you choose DNS validation, ACM **provides you with one or more CNAME records that must be added to this database**.
        + These records contain **a unique key-value pair** that serves as proof that you control the domain. **key-value pair is same for same domain**
        +  Each record, created **specifically for your domain and your account**, contains a name and a value. 
    + Email validation 
        + ACM sends email messages to the three contact addresses listed in the WHOIS database and to five common system addresses for each domain that you specify. That is, up to eight email messages will be sent for every domain name and subject alternative name that you include in your request.
        + Email messages are sent to the following three registered contact addresses in WHOIS: 
            + Domain registrant
            + Technical contact
            + Administrative contact
# Managed renewal
+ Managed **renewal is fully automated** for ACM certificates that were **originally issued using [DNS validation](https://docs.aws.amazon.com/acm/latest/userguide/dns-validation.html)**.  ACM automatically renews your certificate as long as the certificate is in use and your CNAME record remains in place.
+ ACM certificates are valid for 13 months (395 days). To be renewed, email-validated certificates require an action by the domain owner. ACM begins sending renewal notices 45 days before expiration, using the domain's WHOIS mailbox addresses and to five common administrator addresses. The notifications contain a link that the domain owner can click for easy renewal. Once all listed domains are validated, ACM issues a renewed certificate with the same ARN. 
+ Request a domain validation email message 
+ After you have configured contact email addresses for your domain, you can use the AWS Certificate Manager console or the ACM API to request that ACM send you a domain validation email for your certificate renewal. 
+ Automating email validation 
+ Organizations dealing with large numbers of email-validated certificates may prefer to create a parser that can automate the required responses.
# Importing certificates
+ In addition to requesting SSL/TLS certificates provided by AWS Certificate Manager (ACM), you can **import certificates that you obtained outside of AWS**. 
+ To renew an imported certificate, you can obtain a new certificate from your certificate issuer and then manually [reimport](https://docs.aws.amazon.com/acm/latest/userguide/import-reimport.html#reimport-certificate-api) it into ACM. 
+ All certificates in ACM are **regional resources**, including the certificates that you import. To use the same certificate with Elastic Load Balancing load balancers in different AWS Regions, you must **import the certificate into each Region where you want to use it**. 
# Exporting a private certificate
+ You can export a certificate issued by ACM Private CA for use anywhere in your private PKI environment.
+ The exported file contains the certificate, the certificate chain, and the encrypted private key. 
# Reference
[What Is AWS Certificate Manager? - AWS Certificate Manager](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html)
