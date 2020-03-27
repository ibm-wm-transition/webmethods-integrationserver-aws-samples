# MSR Quickstart in AWS cloud using Cloud Formation Template

This project allows user to launch MSR in AWS cloud using AWS Cloud Formation template

## Pre-requisites
1. Create an AWS account https://portal.aws.amazon.com/billing/signup#/start or use existing account
2. Create a S3 bucket https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html
3.  Download Software AG Installer(.bin) file for Linux from https://empower.softwareag.com/Products/DownloadProducts/sdc/default.aspx and copy into the s3 bucket.
http://empowersdc.softwareag.com/dnld/wMInstaller/10.5/SoftwareAGInstaller20191216-LinuxX86.bin is one such example 
4. Clone the webmethods-microservicesruntime-samples repository.
`git clone https://github.com/SoftwareAG/webmethods-microservicesruntime-samples.git`
5. Copy msrInstallerLinuxScript_10_5.txt from cloned repository into s3 bucket
6. Copy the license file(licenseKey.xml) into the s3 bucket
7. Select the region as US East( N.Virginia) as cloud formation is created from US East. If the template has to be used in different region, then CloudFormation template has to be updated with the respective region and availability zone.
8. Create the keypair for accessing ec2 instance https://docs.aws.amazon.com/ground-station/latest/ug/create-ec2-ssh-key-pair.html
9. Some familiarity with AWS console UI

## Getting Started
  
1. Login to the aws console
2. Search and select "CloudFormation" service in AWS console home page 
3. Click "Create stack" button in CloudFormation home page
4. In Step 1 (Specify template) , Select "Upload a template file" 
5. Click "Choose file" and browse  the cloud formation template [[name ]] from cloned repository and select Next
6. In Step 2 ( Specify stack details), Specify Stack name
7. In parameters section provide following values and click Next button
    * MSR Configuration
        | Parameter            	| Description                                                                                   	| Default                   	| Required 	|
        |----------------------	|-----------------------------------------------------------------------------------------------	|---------------------------	|----------	|
        | SAGUserName              	| Empower UserName	|  	| Yes      	|
        | SAGPassword      	| Empower Password                                                                             	|                           	| Yes      	|
        | DefaultPort           	|  MSR default port                                                                                    	|  5555                         	| Yes      	|
        | InstallDir 	| MSR installation directory                                                                            	| /opt/softwareag/msr                      	| Yes      	|

    * AWS Configuration
            
         | Parameter            	| Description                                                                                   	| Default                   	| Required 	|
        |----------------------	|-----------------------------------------------------------------------------------------------	|---------------------------	|----------	|
        | s3BucketName          | Name of S3 bucket where the installation resources resides	                                    |  	                            | Yes      	|
        | keyPair      	        | keypair name to access ec2 instance                                                               |                           	| Yes      	|
        | MyIP           	    | Current system IP for defining security group                                                     |                           	| Yes      	|
 8. In Step 3 (Configure stack options), ignore all the fields and click Next button
 9. In Step 4 (Review), verify the entered information and select the check box in capabilities section. Then, click "Create stack" button
 10. Based on template provided, all AWS resources will be created automatically. Once process is completed, the Load balancer name will be diplayed under value column in Outputs tab
 11. Copy the Load balancer name and paste it in the browser. 
 12. If all resources were configured correctly, the MSR will be up and running.

