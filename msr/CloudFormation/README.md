# Microservices Runtime Quickstart in AWS cloud using CloudFormation Template

This project allows user to launch Softaware AG webMethods Microservices Runtime in AWS cloud using AWS CloudFormation template

## Pre-requisites
1. Create an AWS account https://portal.aws.amazon.com/billing/signup#/start or use existing account
2. Create a S3 bucket https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html
3.  Download Software AG Installer(.bin) file for Linux from https://empower.softwareag.com/Products/DownloadProducts/sdc/default.aspx and copy into the s3 bucket.
http://empowersdc.softwareag.com/dnld/wMInstaller/10.5/SoftwareAGInstaller20191216-LinuxX86.bin is one such example. Rename this file as installer.bin.
4. Clone the webmethods-integrationserver-aws-samples repository.
`git clone https://github.com/SoftwareAG/webmethods-integrationserver-aws-samples.git`
5. Copy msrInstallerLinuxScript_10_5.txt from cloned repository (webmethods-integrationserver-aws-samples/msr/CloudFormation) into s3 bucket created from step 2
6. Copy license file(licenseKey.xml) into the created s3 bucket
7. Select the region as US East( N.Virginia) as cloud formation is created from US East. If the template has to be used in different region, template has to be updated with the respective region and availability zone.
8. Create the keypair for accessing ec2 instance https://docs.aws.amazon.com/ground-station/latest/ug/create-ec2-ssh-key-pair.html
9. Some familiarity with AWS console UI

## Getting Started
  
1. Login to the AWS console
2. Search and select "CloudFormation" service in AWS console home page 
3. Click "Create stack" button in CloudFormation home page
4. In Step 1 (Specify template) , Select "Upload a template file" 
5. Click "Choose file" and browse  the cloud formation template MsrSagStack.template.json from cloned repository(webmethods-integrationserver-aws-samples/msr/CloudFormation) and select Next
6. In Step 2 ( Specify stack details), Specify Stack name
7. In parameters section provide following values and click Next button
    * MSR Configuration
        | Parameter            	| Description                                                                                   	| Default                   	| Required 	|
        |----------------------	|-----------------------------------------------------------------------------------------------	|---------------------------	|----------	|
        | EmpowerUserName              	| Empower UserName	|  	| Yes      	|
        | EmpowerPassword      	| Empower Password                                                                             	|                           	| Yes      	|
        | DefaultPort           	|  MSR default port                                                                                    	|  5555                         	| Yes      	|
        | InstallDirectory 	| MSR installation directory                                                                            	| /opt/softwareag/msr                      	| Yes      	|

    * AWS Configuration
            
         | Parameter            	| Description                                                                                   	| Default                   	| Required 	|
        |----------------------	|-----------------------------------------------------------------------------------------------	|---------------------------	|----------	|
        | S3BucketName          | Name of S3 bucket where the installation resources resides	                                    |  	                            | Yes      	|
        | KeyPair      	        | keypair name (created from Pre-requisites) to access ec2 instance                                                               |                           	| Yes      	|
        | MyIP           	    | Current system IP for defining security group                                                     |                           	| Yes      	|
 8. In Step 3 (Configure stack options), ignore all the fields and click Next button
 9. In Step 4 (Review), verify the entered information and select the check box in capabilities section. Then, click "Create stack" button
 10. Based on template provided, all AWS resources will be created automatically. Once process is completed, the Load balancer name will be diplayed under value column in Outputs tab
 11. Copy the Load balancer name and paste it in the browser. 
 12. If all resources were configured correctly, the MSR will be up and running.

