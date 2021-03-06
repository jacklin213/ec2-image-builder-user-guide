# Prerequisites<a name="image-builder-setting-up"></a>

The following prerequisites must be verified in order to create an image pipeline with EC2 Image Builder\.

## EC2 Image Builder Service\-Linked Role<a name="image-builder-auto-scaling-prereq"></a>

EC2 Image Builder uses a service\-linked role to grant permissions to other AWS services on your behalf\. You don't need to manually create a service\-linked role\. When you create your first Image Builder resource in the AWS Management Console, the AWS CLI, or the AWS API, Image Builder creates the service\-linked role for you\. For more information about the service\-linked role that Image Builder creates in your account, see [Using Service\-Linked Roles for EC2 Image Builder](image-builder-service-linked-role.md)\. 

## Auto Scaling Groups<a name="image-builder-auto-scaling-prereq"></a>

EC2 Image Builder uses Auto Scaling groups to launch instances during the build and test phases of the image pipeline\. When you use Amazon EC2 Auto Scaling, a required service\-linked role is created in your account\. If this role is not present in your account when you use Image Builder, the Image Builder service\-linked role will create if for you\. 

## Configuration Requirements<a name="image-builder-config"></a>
+ EC2 Image Builder does not support encrypted AMIs as the source for or output image of a pipeline\.
+ You must specify a VPC in the infrastructure configuration\. Image Builder does not support EC2\-Classic\. 
+ Image Builder does not support Amazon VPC endpoints \(PrivateLink\)\.
+ Instances used to build images and run tests using Image Builder must have access to the Systems Manager service\. All build activity is orchestrated by SSM Automation\. The SSM Agent will be installed on the source image if it is not already present, and it will be removed before the image is created\.

## IAM<a name="image-builder-IAM-prereq"></a>

The IAM role that you associate with your instance profile must have permissions to run the build and test components included in your image\. The following IAM role policies must be attached to the IAM role that is associated with the instance profile: **EC2InstanceProfileForImageBuilder** and **AmazonSSMManagedInstanceCore**\.

If you configure logging, the instance profile specified in your infrastructure configuration must have `s3:PutObject` permissions for the target bucket\. 
