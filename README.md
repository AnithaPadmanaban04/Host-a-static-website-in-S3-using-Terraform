# Hosting Static Website on S3 using Terraform
## Project Description:

Hosting a static website on Amazon S3 using Terraform is a common way to deploy simple websites or front-end apps. This process involves creating an S3 bucket, setting the necessary permissions, and optionally configuring a custom domain or CloudFront for CDN and HTTPS support. 

Here's a step-by-step guide for setting up a basic static website in an S3 bucket using Terraform.

## Architectural Diagram:

![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/fff47c59-b66f-467f-ac1d-8e29b97d991e)

## Prerequisites:

*	AWS account with full administrative rights
*	Terraform installed (Version 1.5 or higher recommended)
*	A foundational understanding of AWS services and Terraform basics.

### Key Components and Features:

#### S3 Bucket: 
This is the fundamental storage component for hosting your website. The bucket name should be globally unique within AWS.
#### Bucket Configuration: 
Configure the bucket for website hosting, specifying an index document and optionally an error document (e.g., "index.html" and "404.html").
#### Access Control: 
Public-read access is necessary for a static website to be publicly accessible. You achieve this via an S3 bucket policy or ACLs.
#### Deployment of Content: 
Upload your static website files (HTML, CSS, JavaScript, images, etc.) to the S3 bucket. This can be done using the AWS CLI, an S3 client, or an automation tool like Terraform.
#### Public URL: 
Each S3 bucket configured for static website hosting has a public URL you can use to access the website. This URL format typically looks like http://your-bucket-name.s3-website-your-region.amazonaws.com.
#### Automation with Infrastructure as Code: 
Using Terraform to automate the deployment and management of S3 static website. This makes it easier to manage changes, rollbacks, and re-deployments.

## Detailed Guide

For a comprehensive walkthrough of the project, please refer to the detailed guide available on [Medium](https://medium.com/@anitha.padmanaban04/hosting-a-static-website-on-amazon-s3-using-terraform-a-step-by-step-guide-4e230392ef24).

## Connect with Me

GitHub: [GitHub Profile](https://github.com/AnithaPadmanaban04)

LinkedIn: [Linkedin](https://www.linkedin.com/in/anitha-padmanaban-7b2665264/)

