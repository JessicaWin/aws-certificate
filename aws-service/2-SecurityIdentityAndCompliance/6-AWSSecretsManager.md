# Overview
+ Secrets Manager enables you to **replace hardcoded credentials** in your code, including passwords, **with an API call to Secrets Manager** to retrieve the secret programmatically.
+ This helps ensure the secret can't be compromised by someone examining your code, because the secret no longer exists in the code.
+ Also, you can configure Secrets Manager to  **automatically rotate the secret** for you according to a specified schedule.
# Features
+ Secrets Manager enables you to replace stored credentials with a runtime call to the Secrets Manager Web service, so you can retrieve the credentials dynamically when you need them. 
+ Most of the time, your client requires access to the most recent version of the encrypted secret value.
+ However, other versions can exist at the same time. 
+ Store different types of secrets 
+ Secrets Manager enables you to store text in the encrypted secret data portion of a secret.
+ Secrets Manager **encrypts the protected text of a secret by using AWS KMS**
    + AWS KMS ensures secure encryption of your secret when at rest. Secrets Manager associates every secret with a KMS key.
    + Whenever Secrets Manager encrypt a new version of the protected secret data, Secrets Manager requests AWS KMS to **generate a new data key from the KMS key.**
    + Secrets Manager uses this data key for [envelope encryption](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#enveloping).
    + Secrets Manager **stores the encrypted data key with the protected secret data**.
    + Whenever the secret needs decryption, Secrets Manager **requests AWS KMS to decrypt the data key**, which Secrets Manager then uses to decrypt the protected secret data.
    + Secrets Manager **never stores the data key in unencrypted form**, and **always disposes the data key immediately after use**.
# Concepts
+ **Secret**
    + In Secrets Manager, a *secret* consists of **a set of credentials, user name and password, and the connection details** to access a database or other service. 
    + A secret has **metadata**: 
        + An **Amazon Resource Name (ARN)** with the following format:
            + The **name of the secret**, a description, a resource policy, and tags.
            + The **ARN for an encryption key**, an AWS KMS key that Secrets Manager uses to encrypt and decrypt the secret value.
        + Information about **how to rotate the secret**, if you set up rotation
+ **Rotation**
    + *Rotation* is the process of **periodically updating a secret** to make it more difficult for an attacker to access the credentials.
    + In Secrets Manager, you can set up **automatic rotation** for your secrets.
    + When Secrets Manager rotates a secret, it **updates the credentials in both the secret and the database or service**. 
+ **Version**
    + A secret has *versions* which hold copies of the encrypted secret value.
    + When you change the secret value, or the secret is rotated, Secrets Manager creates a new version.
    + A secret always has a version with the staging label **`AWSCURRENT`**, which is the current secret value.
    + `AWSCURRENT` indicates the version that is actively used by clients. A secret always has an `AWSCURRENT` version.
    + `AWSPENDING` indicates the version that will become `AWSCURRENT` when rotation completes.
    + `AWSPREVIOUS` indicates the *last known good* version, in other words, the previous `AWSCURRENT` version
    + Secrets Manager deprecates versions with **no staging labels and removes them when there are more than 100**.
    + Secrets Manager doesn't remove versions created less than 24 hours ago.
    + You can attach **up to 20 staging labels to a secret**. Two versions of a secret **can't have the same staging label**.
# Monitor [AWS](https://so.csdn.net/so/search?q=AWS&spm=1001.2101.3001.7020) Secrets Manager secrets
+ Use **AWS CloudTrail** to log activity for your secrets
+ Use **Amazon CloudWatch** to respond when events of interest occur
+ Use **AWS Config** to assess secrets and track changes to them
+ Use **Security Hub** for security best practices in Secrets Manager
# Reference
[What is AWS Secrets Manager? - AWS Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)
