# Tips for AWS Certified Security – Specialty
* When you use imported key material, you remain responsible for the key material while allowing AWS KMS to use a copy of it. To set an expiration time for the key material in AWS and to manually delete it, but to also make it available again in the future. In contrast, scheduling key deletion requires a waiting period of 7 to 30 days, after which you cannot recover the deleted CMK."
This would be the only way to "delete" a key earlier than 7 days.
* Default CloudFront certificate, Custom SSL certificate stored in AWS IAM and Custom SSL certificate stored in AWS Certificate Manager are valid configurators for using SSL certificates with Amazon CloudFront.
* Download and run the EC2Rescue for Windows Server utility from AWS. With that you can collect a memory dump of the EC2 instance for forensic analysis.
* Encrypted volumes can stops EC2 instances immediately. Check the permissions if this is happening.
* You can configure a key policy for this CMK. Use kms:ViaService to check if the request comes from an AWS service.
* Add the below condition in the key policy:  "Condition": {     "Bool": {       "kms:GrantIsForAWSResource": true     }   } to make sure that the grant should only be created by integrated AWS services.
* Use Cloud HSM if you want to have a secure way of generating, storing, and managing cryptographic keys, but they want to have exclusive access to the management of the keys.
* AWS Config provides a detailed list of resources defined in your AWS Account.
* Customer-managed CMK gets rotated automatically every 365 days.
* When you define access to objects in a bucket, you need to ensure that you specify which objects in the bucket access need to be given. In this case, the * can be used to assign the permission to all objects in the bucket.
* AWS recommends using a custom solution in place for monitoring intrusions into their systems.
* For AWS managed keys, users cannot manage the key rotation. And the key is automatically rotated every 3 years.
* There is no need to add the key information in "aws kms decrypt". This is different from "aws kms encrypt".
* When users create a new CMK, the key material origin can be selected as External which means the key material will be imported.
* If you are using Customer Master Key (CMK) and need to rotate the key create a new CMK with new key material. Change the target CMK of the key alias to the new one.
* You can generate and download an IAM credential report through AWS Management Console or AWS SDKs.IAM role information does not exist in the report. Also, there is no SAML IAM identity provider information.
*  By default, AWS CloudTrail event log files are encrypted using Amazon S3 server-side encryption (SSE). You can also define Amazon S3 lifecycle rules to archive or delete log files automatically. If you want notifications about log file delivery and validation, you can set up Amazon SNS notifications.
* To provide S3 cross-account access, you need two things: S3 bucket policy on account A for account B IAM user to access and then in Account B, the IAM user needs to have an allow access for the S3 bucket in the IAM policy.
* With AWS Config, you can review changes in configurations and relationships between AWS resources, dive into detailed resource configuration histories, and determine your overall compliance against the configurations specified in your internal guidelines.
* Use Systems Manager Patch Manager to generate the report of out of compliance instances/servers. Use Systems Manager Patch Manager to install the missing patches.
* After account B has uploaded objects to the bucket in account A, the objects are still owned by account B, and account A does not have access to it. In order to fix this, the option of --acl "bucket-owner-full-control" should be added when the object is uploaded via aws s3api put-object.
* AWS Shield Advanced protection provides always-on, flow-based monitoring of network traffic and active application monitoring to provide near real-time notifications of DDoS attacks.
* AWS Artifact provides a report and details on how your AWS infrastructure & services being used on your account are PCI compliant and helps validate the implementation and operating effectiveness of AWS security controls. It can provide the SOC compliance report.
* Users can develop custom rules using Lambda functions and then add them to AWS Config rules. 
* App Client ID, App Client Secret and List of scopes are required to configure a social IdP correctly.
* You could use a third-party tool such as OpenSSL to generate a key pair and then import the public key to Amazon EC2 using using "Import key pair" to import the public key to the EC2 service.
* A bucket owner can enable other AWS accounts to upload objects. These objects are owned by the accounts that created them. The bucket owner does not own objects that the bucket owner did not create. Therefore, for the bucket owner to grant access to these objects, the object owner must first grant permission to the bucket owner to use an object ACL. The bucket owner can then delegate those permissions via a bucket policy.
* Unauthenticated guest access is a feature of Amazon Cognito Identity Pools instead of User Pools.
* AWS AppSync enables subscriptions to synchronize data across devices.
* Create a COGNITO_USER_POOLS authorizer and configure a single-space separated list of OAuth Scopes on the API method to properly authorize a call to one of the REST API methods using an access token.
* Create an Auth Challenge Lambda Trigger to implement a CAPTCHA as part of the user sign-in process.
* You need to create an IAM role that establishes a trust relationship between IAM and the corporate directory identity provider to enable Single Sign-On.
*  