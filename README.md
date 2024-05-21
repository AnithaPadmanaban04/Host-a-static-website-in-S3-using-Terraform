# Hosting Static Website on S3 using Terraform
## Project Description:

Hosting a static website on Amazon S3 using Terraform is a common way to deploy simple websites or front-end apps. This process involves creating an S3 bucket, setting the necessary permissions, and optionally configuring a custom domain or CloudFront for CDN and HTTPS support. 

Here's a step-by-step guide for setting up a basic static website in an S3 bucket using Terraform.

## Architectural Diagram:

![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/a85f7e80-bcd8-4e24-aea1-a713107fac03)


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

- Install Terraform and the AWS Command Line Interface (CLI) on your local machine. Configure your AWS credentials by running aws configure and provide your AWS access key and secret key. Check this [link](https://github.com/aniwardhan/Getting-Started-with-Terraform.git) to configure Terraform and AWS CLI
        
- Create a working directory in your local machine and open the folder in MS Visual Code Editor to start the project
        
  ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/2da1f423-a250-499b-b7b7-bce68ba35fb3)


#### 2. Initialize your Terraform environment

* A provider in Terraform is a plugin that enables interaction with an API. This includes Cloud providers and Software-as-a-service providers. 
* The providers are specified in the Terraform configuration code. They tell Terraform which services it needs to interact with.
* Provider configurations should be declared in the root module of your Terraform project.

* Create a file named [providers.tf](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/blob/main/provider.tf) to configure the specific cloud providers or services that your Terraform configuration will interact with.

  ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/e4ff15b4-43a7-4bd8-9140-bb8f4909f98d)

Once File created run the terraform init command so that Terraform downloads necessary plugins and resources required for connecting to AWS and managing your infrastructure.
 
Run the following command to initialize your Terraform environment
```hcl
terraform init
```

  ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/41915893-cbfb-4a70-a4bd-d00926f6edbb)


#### 3. Define your AWS Resource file ([main.tf](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/blob/main/main.tf))

Create a main.tf file. Here you define the resources you want to create or manage using Terraform.

Create an s3 bucket to store the files for hosting a website. S3 bucket name should be globally unique

 ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/77590709-4cf7-402d-a638-7acab5ef701c)
 

#### 4. Create [variable.tf](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/blob/main/variables.tf) to define all necessary variables used in main.tf 
 
  ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/e4e72eac-986b-431f-920a-4e50d353198f)


#### Step 5: Resource: aws_s3_bucket_ownership_controls.

It is used to define and manage ownership controls for an Amazon S3 bucket, this ensures everything in the bucket is owned by us.

 ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/c5951e44-06d5-42cb-8d88-678f4b526aa2)


#### Step 6: Resource: aws_s3_bucket_public_access_block.

This line of code defines if the contents of the bucket can be publicly accessed or not. Setting this to “true” will block public access. Setting all to false to make bucket public.

![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/eec8890d-0eba-451c-921d-2c1233e01763)


![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/47eac11c-392b-4ac9-84ed-4aa949bb2cda)

 
#### Step 7: Resource: aws_s3_bucket_acl.

The purpose of an S3 bucket ACL is to define who has access to the objects in the bucket and what level of access they have. ACLs can be used to control both public and private access to the objects. So, we have to make acl public-read.

This part defines whether the bucket access will be private or not. In the AWS console, this is what it looks like.

 ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/710ac1d3-a7b6-4993-b0f5-4a5ff51a0f83)


 ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/e07572ef-8ab7-43c9-86dc-ca1027aea7b2)

 
#### Step 8: Upload static files into the S3 bucket

Upload index.html and error.html to your local working directory and then add these files in code to upload to S3 bucket

 ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/821b12a8-54e6-4106-9541-afbb0ef1264e)


#### Step 9: Enable Static Website Hosting Resource: aws_s3_bucket_website_configuration to host static web content that can be accessed via a web browser.

Now to enable Static Website Hosting first we need to put [index.html](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/blob/main/index.html) and [error.html](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/blob/main/error.html) in S3 bucket using "aws_s3_bucket_object" because both these files are needed in "aws_s3_bucket_website_configuration".

 ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/2fc3f17b-4b5f-48cc-9f3f-300696e3e93e)

depends_on = [ aws_s3_bucket_acl.example ] means the website will only host if the acl is set to public-read.

Verify Static Web Hosting enabled for the bucket

![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/2721a316-fd5d-4a61-8fc0-95adc39f36ee)


#### Step 10: Create [output.tf](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/blob/main/outputs.tf) to get website endpoint in the terminal itself.
 
 ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/35f540d8-e612-450d-bf6e-3e889f1cca37)

After creating all the necessary files execute the following Terraform commands 

```hcl
terraform fmt

terraform validate

terraform plan

terraform apply -auto-approve
```
 
![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/0cb1f376-5772-445e-b388-99502e1ab5da)



![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/7bbf60db-25cf-4ec1-a825-192fc40476a9)



#### Step 11: Verify the Output in AWS Console

index.html

![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/ea381267-9c19-41a5-bf7a-098f3cc72f0d)

error.html

![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/2b2d5a14-4b24-4492-ae50-f3b4aa276c34)

#### Step 12: Clean up Resources

```hcl
terraform destroy -auto-approve
```

![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/7879e6ef-614e-437a-bc29-7a72d39993cc)

#### Reference Documents:

https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_website_configuration

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_public_access_block

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_policy

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_object

