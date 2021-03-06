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
* Create a new DHCP options set and replace the existing one to ensure that instance in a VPC does not use AWS DNS for routing DNS requests as you want to use your own managed DNS instance.
* In addition to VPC peering and setting the right route tables, the security group of the AD EC2 instance needs to have the right rule to allow incoming traffic,
* You can enforce the MFA authentication requirement using the aws:MultiFactorAuthAge key in a bucket policy. For the Bucket policy add a condition for { "Null": { "aws:MultiFactorAuthAge":true }}.
* The SSM Run command can be used to send OS-specific commands to an instance. Here you can check and see the running processes on an instance and then send the output to an S3 bucket.
*  The SSM Agent stores logs in /var/log/amazon/ssm/errors.log. The information in these log files can help you to troubleshoot problems. 
* The AWS Documentation mentions some key aspects with regards to the configuration of On-premises AD with AWS.
  * **Active Directory Configuration***:
Determining how you will create and delineate your AD groups and IAM roles in AWS is crucial to how you secure access to your account and manage resources. SAML assertions to the AWS environment and the respective IAM role access will be managed through regular expression (regex) matching between your on-premises AD group name to an AWS IAM role.
One approach for creating the AD groups that uniquely identify the AWS IAM role mapping is by selecting a common group naming convention. For example, your AD groups would start with an identifier, for example, AWS-, as this will distinguish your AWS groups from others within the organization. Next, include the 12-digit AWS account number. Finally, add the matching role name within the AWS account. Here is an example:
  * ***Active Directory Federation Services Configuration***:
ADFS federation occurs with the participation of two parties; the identity or claims provider (in this case the owner of the identity repository – Active Directory) and the relying party, which is another application that wishes to outsource authentication to the identity provider; in this case Amazon Secure Token Service (STS). The relying party is a federation partner that is represented by a claims provider trust in the federation service.
* You can use SAML to provide your users with federated single sign-on (SSO) to the AWS Management Console or federated access to call AWS API operations.
* The deletion of CMK has no immediate effect on the EC2 instance or the EBS volume because Amazon EC2 uses the plaintext data key—not the CMK—to encrypt the disk I/O to the EBS volume.
* AWS IAM Access Advisor provides permission guardrails to help control which services your developers and applications can access. By analyzing the last accessed information, you can determine the services not used by IAM users and roles
* AWS KMS supports multi-region keys, which are AWS KMS keys in different AWS Regions that can be used interchangeably – as though you had the same key in multiple Regions. With multi-Region keys, you can more easily move encrypted data between Regions without having to decrypt and re-encrypt with different keys in each Region. Multi-Region keys are not global. You create a multi-Region primary key and then replicate it into Regions that you select within an AWS partition. Then you manage the multi-Region key in each Region independently. Neither AWS nor AWS KMS ever automatically creates or replicates multi-Region keys into any Region on your behalf. 
* You currently have an S3 bucket hosted in an AWS Account. It holds information that needs to be accessed by a partner account. Which is the MOST secure way to allow the partner account to access the S3 bucket in your account
  * Ensure an IAM role is created which can be assumed by the partner account.
  * Ensure the partner uses an external id when making the request.
  * Provide the ARN for the role to the partner account.
* The km: ViaService condition key limits the use of a customer-managed CMK to requests from particular AWS services. (AWS managed CMKs in your account, such as aws/s3, are always restricted to the AWS service that created them.)
* Your private key file must be protected from read and write operations from any other users. Otherwise you will receive an “Unprotected Private Key File” error.
* In a distributed HPC system you can use GenerateDataKeyWitoutPlaintext API to generate a data key. This data key is then distributed to the individual components of the distributed system. Decrypt API needs to be used by the individual components processing the data to decrypt the data key.  Then plaintext key can be used to encrypt the data.
* To change the expiration date of a KMS key, you must reimport the same key material and specify a new expiration date.
* The key material for customer-managed CMK must be a 256-bit symmetric key. The import token has a 24-hour expiration time.
* Using the SSM run command to run the AWSSupport-RunEC2RescueForWindowsTool command document with the ResetAccess command is the easiest way to reset a lost Windows Server password.
* The S3 bucket objects are encrypted, the metadata is not encrypted. So the best option is to store the metadata in the DynamoDB table and encrypt using AWS KMS during the table creation process.
* When there are applications that work on legacy protocols, you need to ensure that the ELB can be used at the network layer as well. Hence you should choose the Classic LB. Since the traffic needs to be secure between the Client and the EC2 Instances, the SSL termination should occur on the EC2 Instances.
* Data key caching stores data keys and related cryptographic material in a cache. When you encrypt or decrypt data, the AWS Encryption SDK looks for a matching data key in the cache. If it finds a match, it uses the cached data key rather than generates a new one. Data key caching can improve performance, reduce cost, and help you stay within service limits as your application scales.
* A host-based intrusion detection system can be used to monitor and inspect packets for security threats.
* Amazon GuardDuty has reported that an EC2 instance has been compromised. AWS recommends that you Investigate the potentially compromised instance for malware and remove any discovered malware.
* Amazon RDS creates an SSL certificate and installs the certificate on the DB instance when the instance is provisioned. Once an encrypted connection is established, data transferred between the DB Instance and your application will be encrypted during transfer. You can also require your DB instance only to accept encrypted connections.
* A device manufacturer wants to digitally sign their firmware software to generate a digital signature to ensure authenticity. For that case you can use the Sign API provided by AWS KMS.
* Amazon Inspector offers a programmatic way to find security defects or misconfigurations in your operating systems and applications. Because you can use API calls to access both the processing of assessments and the results of your assessments, integration of the findings into workflow and notification systems is simple. DevOps teams can integrate Amazon Inspector into their CI/CD pipelines and use it to identify any pre-existing issues or when new issues are introduced.
* To track requests for access to your S3 bucket, you can enable access logging. 
* You could use a third-party tool and then import the public key to Amazon EC2. Each key pair requires a name. Be sure to choose a name that is easy to remember. Amazon EC2 associates the public key with the name that you specify as the key name.
* When you write such an app, you'll make requests to AWS services that must be signed with an AWS access key. However, we strongly recommend that you do not embed or distribute long-term AWS credentials with apps that a user downloads to a device, even in an encrypted store. Instead, build your app so that it requests temporary AWS security credentials dynamically when needed using web identity federation. The supplied temporary credentials map to an AWS role that has only the permissions needed to perform the tasks required by the mobile app.
* GuardDuty can perform an assessment of network communication and produce “CryptoCurrency:EC2/BitcoinTool.B” finding when an EC2 instance is querying an IP address(es) that is associated with Bitcoin.
* You can use groups to create a collection of users in a user pool, which is often done to set the permissions for those users. For example, you can create separate groups for users who are readers, contributors, and editors of your website and app.
* In a WAF sandwich the EC2 instance running your WAF software is included in an Auto Scaling group and placed between two Elastic load balancers. 
* When using “Single-User Rotation” mode in AWS Secrets Manager, Secrets Manager uses a single user to rotate its own credentials.  Sign-in failures can occur between the moment when the old password is removed by the rotation and the moment when the updated password is made accessible as a new version of the secret. This time window should be very short, but it can happen.
There are two ways to avoid this issue:
  * The application can implement retry with an exponential back-off strategy.  Thus, the application would retry sign-in several times over a longer time period.  A failure should be reported only after repeated sign-in failures.
  * Multi-User Rotation can be enabled.  In this scenario, separate “master” user credentials are used for secret rotation. The old version of the secret continues to operate and handle service requests while the new version is prepared and tested. The old version isn't deleted until after the clients switch to the new version. There's no downtime while changing between versions.
* With the AWS KMS Encrypt CLI command, you can directly encrypt small amounts of arbitrary data that is less than 4k, such as a personal identifier or database password.
* The correct sequence of how KMS manages the keys when used along with the Redshift cluster service is the master keys encrypt the cluster key. The cluster key encrypts the database key. The database key encrypts the data encryption keys.
* If you need to sniff the actual network packets, the ideal approach would be to use a network monitoring tool provided by an AWS partner.
* VPC Gateway Endpoint supports Amazon S3 and Amazon DynamoDB services and not the KMS Service. A VPC Interface Endpoint enables a private connection between VPC to KMS service without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.
* The following objectives would you achieve by implementing an IPSec tunnel:
  * Data encryption across the Internet
  * Protection of data in transit over the Internet
  * Peer identity authentication between VPN gateway and customer gateway
  * Data integrity protection across the Internet
* In S3 It is possible to have different encryption keys for different versions of the same object.
* To allow read access to these objects from your website, you can add a bucket policy that allows s3: GetObject operation with a condition, using the aws: referer key, that the get request must originate from specific webpages.
* The Amazon DynamoDB service uses VPC Gateway Endpoint for enabling private connection to a VPC and you must create a route table rule for prefix list ID of the DynamoDB service with the DynamoDB VPC endpoint as the target.
* You need to generate the SSH key pairs of EC2 Instances by third-party tools so that you can have complete control of the access keys.
* If you cannot find the SSH private key for instance, and it seems that the key is lost eetach the root volume, attach it to another instance as a data volume, modify the authorized_keys file to include the new SSH public key and move the volume back.
* In a public AMI identify unauthorized public SSH keys by locating all authorized_keys files on disk. Remove any unrecognized keys.
* the command with “--sse-specification Enabled=true“ parameter ensures that the data for the DynamoDB table is encrypted at rest.
* In combination with information gleaned from your VPC Flow Logs, AWS CloudTrail Event Logs, and DNS logs, GuardDuty can detect many different types of dangerous and mischievous behavior, including probes for known vulnerabilities, port scans, and access from unusual locations.
* You can use an OIDC identity provider when you want to establish trust between an OIDC-compatible IdP—such as Google, Salesforce, and many others—and your AWS account. This is useful if you create a mobile app or web application that requires access to AWS resources, but you don't want to create custom sign-in code or manage your own user identities.
* A user pool is a user directory in Amazon Cognito. The users can sign in to your web or mobile app through Amazon Cognito with a user pool. Users can also sign in through social identity providers like Facebook or Amazon and through SAML identity providers. Whether your users sign in directly or through a third party, all members of the user pool have a directory profile that you can access through an SDK.
* You can use a new condition key, aws:PrincipalOrgID, in IAM policies to require all principals to access the resource from an account in the organization.
*  Amazon API Gateway Lambda authorizer (formerly known as a custom authorizer) is a Lambda function that you provide to control access to your API methods. A Lambda authorizer uses bearer token authentication strategies, such as OAuth or SAML. It can also use the information described by headers, paths, query strings, stage variables, or context variables request parameters.
* CloudFront signed URLs should be used for securing and limiting access to content in RTMP distribution.
* API Gateway Access logs contain details about the user and IPs accessing the APIs exposed via API Gateway.
* Amazon S3 Glacier is the most cost-effective storage solution for archive data. Amazon S3 Glacier Vault Lock can be used to implement a “Write-Once-Read-Many” archive storage solution.
* Elliptic Curve Diffie-Hellman Ephemeral (ECDHE) cipher suites support PFS.
* You can create a private CA using the ACM console. After filling in all the required information, such as CA subject name and key algorithm, you can fully manage the private CA.
* Users can create an audit report for a private CA. The report is saved in an S3 bucket and contains the required information. 
* A private CA in ACM is a highly available service. However, its scope is within an AWS region. You need to create multiple CAs that run independently in at least two regions for redundancy and disaster recovery.
* Multiple certificates can be installed on the HTTPS listener. The application load balancer supports SNI, and it can choose a certificate for a client automatically.
* AWS supports the identity federation with SAML. You use an IAM identity provider when you want to establish trust between a SAML-compatible IdP such as Shibboleth or Active Directory Federation Services and AWS so that users in your organization can access AWS resources.
* The temporary security credentials returned by STS include SessionToken, SecretAccessKey, and AccessKeyId. Applications can use these credentials to sign calls to AWS service API operations.
* By default, the temporary security credentials created by AssumeRoleWithWebIdentity last for one hour. However, you can use the optional DurationSeconds parameter to specify the duration of your session. You can provide a value from 900 seconds (15 minutes) up to the maximum session duration setting for the role. This setting can have a value from 1 hour to 12 hours.
* You can configure GuardDuty to use your own custom trusted IP list containing your allowed IP addresses for secure communication with your AWS infrastructure and applications. By doing so, GuardDuty would ignore the Scanner IP warnings and alerts.
* AWS Firewall Manager can help manage WAF web ACLs for accounts within an AWS Organizations.
* Exposed Access Keys check-in AWS Trusted Advisor can identify potentially leaked or compromised access keys. When there is an alert, users can take immediate actions to secure the account.
* Users can create a VPC endpoint for the CloudWatch Logs service to establish a private connection. You can establish a private connection between the VPC and CloudWatch Logs via an interface VPC endpoint to meet the security requirements.
* Parameter Store does support versioning. You can specify a parameter name and a specific version number in API calls and SSM documents.
* While deploying CloudHSM Cluster, you can include multiple HSM instances in different availability zones which are automatically synchronized between each other. 
* A common Virtual Private Gateway is required and each VPG supports ten IPsec VPN connections. Besides, for each local data center, a redundant Site-to-Site VPN connection should be established to ensure connectivity if one Customer Gateway becomes unavailable. Two Customer Gateways are required for each local data center
* A Lambda authorizer is useful if you want to implement a custom authorization scheme that uses a bearer token authentication strategy such as OAuth or SAML or uses request parameters to determine the caller's identity. When a client makes a request to one of your API's methods, API Gateway calls your Lambda authorizer, which takes the caller's identity as input and returns an IAM policy as output.
* The external ID will be checked when IAM entities assume the role, which prevents the Confused Deputy problem. AWS does not treat the external ID as a secret. After creating a secret like an access key pair or a password in AWS, you cannot view them again. The external ID for a role can be seen by anyone with permission to view the role.
* In order to enable the single sign-on to AWS, the third-party IdP should be configured to use AWS as a relying party.
* Microsoft Active Directory standard edition is ideal for small and midsize businesses with up to 5,000 employees and 30,000 directory objects. It also supports a large number of AWS managed applications and services.
* You can bind up to 25 certificates per load balancer. 
* Create a VPC endpoint for AWS KMS with private DNS enabled and add the aws:sourceVpce condition to the AWS KMS key policy referencing the company's VPC endpoint ID. With that VPC and KMS communication will travel entirely within the AWS network and not use public service endpoints.
* CloudTrail console will store all the events for the last 90 days in the even history.
* Service Control Policies can be used to restrict access to all the users, including ROOT.
* We cannot export public certificates created by ACM and We can export private certificate created by ACM and use them in EC2.
* What happens if EBS is encrypted with CMK and that CMK is deleted?
  * EBS will work till it is not unmounted. Back up your data quickly.
* You cannot automatically rotate CMKs with imported key material. You can rotate them manually.
* CMKs are region-specific and cannot be shared across regions.
* If you have accidentally deleted the imported key material in CMK, then you can download the new wrapping key and import token, and import the original key into the existing CMK.
* With S3 Object Lock, you can store objects using a write-once-read-many (WORM) model.
