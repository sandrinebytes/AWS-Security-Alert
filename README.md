# AWS-Security-Alert

## 📌 To Do
- Build a new security monitoring system  
- Set up alerts for when the security monitoring system is accessed  

## 🛠 Using
- **CloudTrail** – process and analyze events  
- **CloudWatch** – monitoring and log analysis  
- **SNS** – send notifications/alerts  

## 🚀 Steps
1. Set up **Secrets Manager**  
2. Configure **CloudTrail**  
3. Test **CloudTrail**  
4. Configure **CloudWatch**  
5. Set up alert system with **SNS** to receive emails  
6. Test and troubleshoot the entire system  

---

✅ This project demonstrates how AWS native services can be integrated to build a simple but effective **security monitoring and alerting system**. It can be expanded into a foundation for **SIEM-style monitoring** in cloud environments.

## Secrets Manager
In AWS Secrets Manager > Secrets > Store a new secret, I select “Other type of secret.”  
I then entered the Key/Value pairs:  
- **Key:** “The Secret is”  
- **Value:** “I need 3 coffees a day to function.”  
![Secret Key Value](secret-key-value.png)

Next, I added an encryption key. AWS encryption keys are important for protecting sensitive data, and permissions can be assigned so only specific people can access the key.  
![Encryption Key Setup](encryption-key.png)

Another feature I like about Secrets Manager is the ability to replicate secrets across multiple regions for availability.
Secret successfully created.
![Secret replication successful](secret-replication.png)

## Summary
Created a secret called **“TopSecretInfo”** in AWS Secrets Manager containing the string value:
![Secrets Summary Cloud Icons](secrets-summary-cloud-icons.png)

## CloudTrail

Now I’ll configure CloudTrail to detect if someone attempts to access the secret.  
CloudTrail tracks events that happen in an AWS account, logging details about who accessed a resource, when, and how.

**Setting up trails:** When you create a trail, you tell CloudTrail which activities to log and where to store those logs.  

![CloudTrail Setup](cloudtrail-setup.png) <!-- Image 5 -->
## CloudTrail Overview

CloudTrail is essential for security, compliance, and troubleshooting, as it allows detection of suspicious activity.

![CloudTrail Logo](cloudtrail-logo.png)

## S3 Bucket for CloudTrail

Created an S3 bucket to store CloudTrail logs for monitoring and analysis.  
![S3 Bucket Setup 1](s3-bucket-setup-1.png)
![S3 Bucket Setup 2](s3-bucket-setup-2.png)
### Creating an S3 Bucket
Returned to Secrets Manager to view the secret.  
![Secrets Manager View](secrets-manager-view.png) <!-- Image 9 -->

### CloudShell Terminal
In CloudShell, I ran the AWS CLI command to retrieve the secret, replacing `your-region-code` with the correct region.  
Output confirmed the secret value:  
“I need 3 coffees a day to function.”  
![CloudShell Retrieve Secret](cloudshell-retrieve-secret.png) <!-- Image 10 -->
### Secret Retrieval Methods
Two retrieval methods:  
1. Secrets Manager Console (Retrieve value button)  
2. AWS CLI (`get-secret-value` command)  
![Secret Retrieval Methods](secret-retrieval-methods.png) <!-- Image 11 -->

### Analyzing CloudTrail Events
Checking Event history in CloudTrail showed `GetSecretValue` events for both retrieval methods (console & CLI). This confirms CloudTrail successfully tracks when secrets are accessed.  
![CloudTrail Event History](cloudtrail-event-history.png) <!-- Image 12 -->

### CloudWatch Setup
Next, I configured CloudWatch for deeper log analysis and to create metrics that track how often a secret is accessed.  
CloudWatch is crucial because:  
- You can create alerts based on logs.  
- Unlike CloudTrail’s 90-day history, CloudWatch logs can be stored indefinitely.  
- Logs can be aggregated and filtered across multiple AWS services.  

(Event History = short-term view, CloudWatch Logs = long-term, detailed analysis.)  
## Creating a Filter Pattern  
![CloudWatch Metric Filter](cloudwatch-metric-filter.png) <!-- Image 13 -->
Created a metric filter to track all events where the secret was accessed (GetSecretValue).
