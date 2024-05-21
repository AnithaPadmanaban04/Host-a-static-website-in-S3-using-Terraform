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

## Steps
#### 1. Create Terraform Environment

- Install Terraform and the AWS Command Line Interface (CLI) on your local machine. Configure your AWS credentials by running aws configure and provide your AWS access key and secret key. Check this [link](https://github.com/AnithaPadmanaban04/Getting-Started-with-Terraform.git) to configure Terraform and AWS CLI
        
- Create a working directory in your local machine and open the folder in MS Visual Code Editor to start the project
        
  ![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/81eb9f91-4e9c-4102-9ea1-4b3628b6d0c4)


#### 2. Initialize your Terraform environment

* A provider in Terraform is a plugin that enables interaction with an API. This includes Cloud providers and Software-as-a-service providers. 
* The providers are specified in the Terraform configuration code. They tell Terraform which services it needs to interact with.
* Provider configurations should be declared in the root module of your Terraform project.

* Create a file named [providers.tf](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/blob/main/provider.tf) to configure the specific cloud providers or services that your Terraform configuration will interact with.

 ![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/b8aea51d-0aab-46d7-87fb-e870b42302fc)


Once File created run the terraform init command so that Terraform downloads necessary plugins and resources required for connecting to AWS and managing your infrastructure.
 
Run the following command to initialize your Terraform environment
```hcl
terraform init
```

 ![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/4f04eeae-87df-4450-8db6-d3e68a40f351)


#### 3. Define your AWS Resource file ([main.tf](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/blob/main/main.tf))

Create a main.tf file. Here you define the resources you want to create or manage using Terraform.

Create an s3 bucket to store the files for hosting a website. S3 bucket name should be globally unique

![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/43ee2a9b-42bf-4a5f-951b-d550fbbe4f17)

 
#### 4. Create [variable.tf](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/blob/main/variables.tf) to define all necessary variables used in main.tf 
 
 ![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/ff362351-d609-4a64-b09c-2c71c3544ee4)


#### Step 5: Resource: aws_s3_bucket_ownership_controls.

It is used to define and manage ownership controls for an Amazon S3 bucket, this ensures everything in the bucket is owned by us.

![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/4186c1eb-f6f7-4043-aed5-c25ee77c9121)


#### Step 6: Resource: aws_s3_bucket_public_access_block.

This line of code defines if the contents of the bucket can be publicly accessed or not. Setting this to “true” will block public access. Setting all to false to make bucket public.

![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/32f8f278-96fd-4ff2-af43-d246813d0b73)


![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/5ec2aff9-cb4c-4655-bf13-78f6b4c16c64)

 
#### Step 7: Resource: aws_s3_bucket_acl.

The purpose of an S3 bucket ACL is to define who has access to the objects in the bucket and what level of access they have. ACLs can be used to control both public and private access to the objects. So, we have to make acl public-read.

This part defines whether the bucket access will be private or not. In the AWS console, this is what it looks like.

![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/4350930b-909d-4853-af9f-d7a27a40cb4b)


![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/ed968869-ad48-4ee5-aba1-8e7e4589f923)

 
#### Step 8: Upload static files into the S3 bucket

Upload index.html and error.html to your local working directory and then add these files in code to upload to S3 bucket

![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/121d209b-d37f-48ea-a8ec-66dd52a92407)


#### Step 9: Enable Static Website Hosting Resource: aws_s3_bucket_website_configuration to host static web content that can be accessed via a web browser.

Now to enable Static Website Hosting first we need to put [index.html](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/blob/main/index.html) and [error.html](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/blob/main/error.html) in S3 bucket using "aws_s3_bucket_object" because both these files are needed in "aws_s3_bucket_website_configuration".

![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/822fdf9d-8f63-46de-9826-a1963bd2baa9)

depends_on = [ aws_s3_bucket_acl.example ] means the website will only host if the acl is set to public-read.

Verify Static Web Hosting enabled for the bucket

![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/88911429-11e3-414a-84b9-3e9d73b9ea1f)


#### Step 10: Create [output.tf](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/blob/main/outputs.tf) to get website endpoint in the terminal itself.
 
![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/d1e478ba-1ca4-4fd8-bd89-332a7e03d558)


After creating all the necessary files execute the following Terraform commands 

```hcl
terraform fmt

terraform validate

terraform plan

terraform apply -auto-approve
```
 
![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/10e5f692-b569-426f-8c10-7f755857ae0a)


![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/dd284d92-fce8-49b5-ae5d-564e84e6f83a)


#### Step 11: Verify the Output in AWS Console

index.html

![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/5148e260-550a-4d88-9662-65db4d75cbf1)


error.html

![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/10825eb4-f43c-49c1-b445-10629d0a5814)


#### Step 12: Clean up Resources

```hcl
terraform destroy -auto-approve
```

![image](https://github.com/AnithaPadmanaban04/Host-a-static-website-in-S3-using-Terraform/assets/170385807/c1edf391-6a5a-481f-8137-e10cbc8c2b49)



#### Reference Documents:

https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_website_configuration

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_public_access_block

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_policy

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_object

