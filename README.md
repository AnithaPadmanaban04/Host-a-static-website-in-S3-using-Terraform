# Hosting Static Website on S3 using Terraform
## Project Description:

Hosting a static website on Amazon S3 using Terraform is a common way to deploy simple websites or front-end apps. This process involves creating an S3 bucket, setting the necessary permissions, and optionally configuring a custom domain or CloudFront for CDN and HTTPS support. 

Here's a step-by-step guide for setting up a basic static website in an S3 bucket using Terraform.

## Architectural Diagram:
 ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/22b89081-22a7-471b-8706-0996499ce9d3)

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

## Steps
#### 1. Create Terraform Environment

Install Terraform and the AWS Command Line Interface (CLI) on your local machine. Configure your AWS credentials by running aws configure and providing your AWS access key and secret key.

#### 2. Initialize your Terraform environment

Inside the project directory, create a file named [providers.tf](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/blob/main/provider.tf) to configure the specific cloud providers or services that your Terraform configuration will interact with.

![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/9a1a1258-8448-4215-ba99-221bd0dedef6)

 
Run the following command to initialize your Terraform environment
```hcl
terraform init
```
#### 3. Define your AWS Resource file ([main.tf](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/blob/main/main.tf))

Create a main.tf file. Here you define the resources you want to create or manage using Terraform.

 ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/aca089ad-34c9-41d8-9f69-61776c67e443)


#### 4. Create [variable.tf](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/blob/main/variables.tf) to define all necessary variables used in main.tf 
 
![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/92735418-3bf9-4ca5-b7d3-767ce8905011)


#### Step 5: Resource: aws_s3_bucket_ownership_controls.

It is used to define and manage ownership controls for an Amazon S3 bucket, this ensures everything in the bucket is owned by us.

 ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/eb71e55c-998e-4b23-982a-91f486ea15eb)


#### Step 6: Resource: aws_s3_bucket_public_access_block.

Allows you to enforce certain rules on an S3 bucket to control its public access. Setting all to false to make bucket public.

![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/fdec45bb-eff3-49ed-b2ac-1a44aa0fa752)

 
#### Step 7: Resource: aws_s3_bucket_acl.

The purpose of an S3 bucket ACL is to define who has access to the objects in the bucket and what level of access they have. ACLs can be used to control both public and private access to the objects. So, we have to make acl public-read.

 ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/89e53bef-6bca-4e29-acf5-32cec075810e)


#### Step 8: Enable Static Website Hosting

Now to enable Static Website Hosting first we need to put [index.html](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/blob/main/index.html) and [error.html](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/blob/main/error.html) in S3 bucket using "aws_s3_bucket_object" because both these files are needed in "aws_s3_bucket_website_configuration".

 ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/2aaa27c8-980e-467d-9ce2-643c60eb286d)



#### Step 9: Resource: aws_s3_bucket_website_configuration to host static web content that can be accessed via a web browser.

![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/c5dc3537-2e7b-4748-aff5-3edfb7af8530)

 
depends_on = [ aws_s3_bucket_acl.example ] means the website will only host if the acl is set to public-read.

#### Step 10: Create [output.tf](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/blob/main/outputs.tf) to get website endpoint in the terminal itself.
 
![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/b389e914-adfb-41cd-b542-aa3ab0c2ce9c)

After creating all the necessary files execute the following Terraform commands 
```hcl
terraform fmt

terraform validate

terraform plan

terraform apply -auto-approve
```
 
![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/7f0064e8-7bc2-422f-9aa4-c6597c6fd748)

#### Step 11: Verify the Output in AWS Console

![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/f11a8e3a-b9d5-4615-84b4-2e44c3f0b19b)

 
#### Step 12: Clean up Resources

```hcl
terraform destroy -auto-approve
```
