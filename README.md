# New To Amazon Web Services (AWS)!!
Nowadays it's very difficult to imagine building an application that does not use any top Cloud providers like AWS, Google Cloud, or Azure. Many fresh or experienced engineers are rushing to learn these cloud services to either upgrade their skillset or build modern applications. 

If you are new to AWS, it can get overwhelming. There are 200+ services and many of them are interdependent and interconnected. I have put a list of core services and concepts that you can refer to and solidify your understanding of the AWS Cloud.

## Purpose
This repo is created for new AWS users to get enough familiarity with the core AWS Cloud services. The focus is on certain critical practices and core services to create a basic mental model that can help the account owners and users to use the AWS cloud safely and effectively.  

Over the years, I have seen many users (Developers or Account Owners) who create AWS accounts for themselves or their team and then quickly find themselves in one or other problems. Having a basic operational understanding of AWS Cloud goes a long way. 

## How to Use this Guide
For each service, I have put some basic explanations, mostly taken from the AWS documentation and other verified sources, and direct links to the documentation pages that the reader will have to go through step by step. 

The AWS documentation is the best source of detailed information. The documentation refererences may feel a bit boring and lengthy, but I have put only the required references that are critical for initial understanding. 

You can stroll around to different resources but do make sure to read through the referenced documentation first.

## AWS Global Infrastructure
The AWS Cloud infrastructure is built around AWS Regions, Availability Zones, and Edge locations. An AWS Region is a group of physical locations that has multiple data centers known as Availability Zones. Availability Zones consist of one or more discrete data centers, each with redundant power, networking, and connectivity, housed in separate facilities. These Availability Zones offer you the ability to operate production applications and databases that are more highly available, fault-tolerant, and scalable than would be possible from a single data center.

- https://aws.amazon.com/about-aws/global-infrastructure/
- https://aws.amazon.com/about-aws/global-infrastructure/regions_az/

### Do
- Understand the benefits of having a well-spread global infrastructure
- Select proper geographic location(s) based on the use case of your application

### Don’t
- While following any tutorial, do not create resources in the geographic locations mentioned in that tutorial as it is. I have seen people follow certain regions as it is, because everyone else does that. 


## AWS Account and Root User
When you create an your AWS account, you begin with one identity that has complete access to all the AWS services and resources in the account. This identity is called the AWS account Root User. You can sign in as the root user using the email address and password that you used to create the account.

It is strongly recommended not use the root user for the everyday tasks, even the administrative ones. Instead, adhere to the best practice of using the root user only to create your first IAM user. Then securely lock away the root user credentials and use them to perform only a few account and service management tasks. The IAM user represents the person or service who uses the IAM user to interact with AWS, either through UI or programmatically. The best thing about an IAM user is that, it can only DO things that is explicitly granted, known as Service policies or permissions. 

- https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html
- https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html


### Do
- Enable MFA on Root User
- Create IAM User with specific IAM Permissions
- Create Groups for specific sets of users and Assign Permissions to the Group
- Check permissions of the IAM User before generating and sharing the Access Keys

### Don’t 
- Do not give your Root User Credentials to Anyone
- Do not generate Access Keys for Root User
- Do not generate Access Keys for IAM Users if not needed


## AWS Billing
AWS automatically charges the credit card that you provided when you sign up for an AWS account. You can view or update your credit card information at any time, including designating a different credit card for AWS to charge. Do keep in mind that the charges are only applied if you have used any resources. AWS has highly granular structure for the charges and each service has different and multiple types of charges applied. 

- https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_billing.html
- https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/checklistforunwantedcharges.html

AWS Cost Explorer is a tool that enables you to view and analyze your costs and usage. You can explore your usage and costs using the main graph, the Cost Explorer cost and usage reports, or the Cost Explorer RI reports. You can use Cost Explorer to identify areas that need further inquiry and see trends that you can use to understand your costs.

You can use AWS Budgets to track and take action on your AWS cost and usage. You can use AWS Budgets to monitor your aggregate utilization and coverage metrics.

- https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html

### Do
- Create Budget alerts based on your estimated monthly spending
- Give Budget Access Permissions to authorized users only
- Spend a few minutes per month to check your Bill and analyze the resource usage

### Don’t 
- Don’t Assume anything, AWS can be very costly if you do not put guardrails
- Give full permissions to every user that you create in your account


## Amazon Simple Storage Service (S3)
Amazon S3 is an object storage service that offers industry-leading scalability, data availability, security, and performance. Customers of all sizes and industries can use Amazon S3 to store and protect any amount of data for a range of use cases. Amazon reported it stored more than 100 trillion objects as of [March 2021](https://aws.amazon.com/blogs/aws/amazon-s3s-15th-birthday-it-is-still-day-1-after-5475-days-100-trillion-objects/). Amazon S3 was the earliest cloud service that focused on API-driven Cloud Infrastructure, freeing developers from any capacity planning, pay only for used storage, and with practically unlimited storage capacity. 

Over the years, S3 has kept on adding new innovative features. You can use S3 for the following use cases:
- Privately storing your application data (CSV, Images, Videos, or any other types)
- Static Website Hosting (Angular, Vue, React, or any other JavaScript-based Single Page Applications)
- Store files in different storage formats like Instant Retrieval, Infrequent Retrieval, Long-term backup, etc. Each format has different storage and retrieval cost. 
- Automatically transition stored files to an optimal storage format based on file age, this reduces the storage cost over the period of time.
- Automatically Delete stored files after certain periods of time

### Refereces
- https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html
- https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-bucket-intro.html
- https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html
- https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html
- https://docs.aws.amazon.com/AmazonS3/latest/userguide/aws-billing-reports.html
- https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html

### Do
- Depending on your use case, create the Bucket in the same region where the rest of your application resources are running.
- Check your use case and Create Private Buckets Only
- Create Lifecycle policies to transition files to an optimal storage tier
- Create Pre-signed URLs to share files stored in the bucket

### Don’t 
- Do not create Public Buckets unless really required
- Make sure you do not store sensitive user information inside the S3 bucket files unless your application and AWS account has enough security in place. For example, User Personal details, Credit card information, Medical information, etc.
