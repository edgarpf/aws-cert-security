# Tips for AWS Certified Security – Specialty
* When you use imported key material, you remain responsible for the key material while allowing AWS KMS to use a copy of it. To set an expiration time for the key material in AWS and to manually delete it, but to also make it available again in the future. In contrast, scheduling key deletion requires a waiting period of 7 to 30 days, after which you cannot recover the deleted CMK."
This would be the only way to "delete" a key earlier than 7 days.
* Default CloudFront certificate, Custom SSL certificate stored in AWS IAM and Custom SSL certificate stored in AWS Certificate Manager are valid configurators for using SSL certificates with Amazon CloudFront.
* Download and run the EC2Rescue for Windows Server utility from AWS. With that you can collect a memory dump of the EC2 instance for forensic analysis.
* Encrypted volumes can stops EC2 instances immediately. Check the permissions if this is happening.