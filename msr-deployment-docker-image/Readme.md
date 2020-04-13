# Deploy Microservices Runtime From Existing Docker Image in AWS cloud using CloudFormation Template

This project allows user to launch Softaware AG webMethods Microservices Runtime from docker image uploaded to AWS ECR or Docker hub in AWS cloud using AWS CloudFormation template

## Pre-requisites
1. Access to AWS management console.
2. ECR or Docker hub repository url containing docker image.
3. Clone the webmethods-integrationserver-aws-samples repository.
`git clone https://github.com/SoftwareAG/webmethods-integrationserver-aws-samples.git`
4. Select the region as US East( N.Virginia) as cloud formation is created from US East. If the template has to be used in different region, template has to be updated with the respective region and availability zone.
5. Create a Secret using Secret Manager Service. Navigate to AWS Secret Manager and click on Store new Secret. Add username and password  as secret keys which should correspond to the docker credential having access to private repository on docker hub or ECR Make note of the generated Secret ARN which will be used at the time of creating cloud formation stack.


## Getting Started
  
1. Login to the AWS console
2. Search and select "CloudFormation" service in AWS console home page 
3. Click "Create stack (with new resources standard)" button in CloudFormation home page
4. In Step 1 (Specify template) , Select "Upload a template file" 
5. Click "Choose file" and browse  the cloud formation template CloudFormationTemplate-DockerImageDeployment.yml from cloned repository(webmethods-integrationserver-aws-samples/msr-deployment-docker-image) and select Next
6. In Step 2 ( Specify stack details), Specify Stack name
7. In parameters section provide following values and click Next button
    * MSR Configuration
        | Parameter            	| Description                                                                                   	| Default                   	| Required 	|
        |----------------------	|-----------------------------------------------------------------------------------------------	|---------------------------	|----------	|
        | DockerCredentialSecret       | ARN of the Secret created in Secret manager. This credential will be used by docker to pull images from private repository	|  	| Yes      	|
		| DockerImageUrl        | Specifies the Docker image url from where the docker image will be downloaded	|  	| Yes      	|
		| ECSAMI              	| Name of the ECS optimized instance id obtained from https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs-optimized_AMI.html 	|  	| Yes      	|
        | EcsClusterName 	| Specifies the ECS Cluster Name with which the resources would be associated | default                      	| Yes      	|

 8. In Step 3 (Configure stack options), ignore all the fields and click Next button
 9. In Step 4 (Review), verify the entered information and select the check box in capabilities section. Then, click "Create stack" button
 10. Based on template provided, all AWS resources will be created automatically. Once process is completed, the LoadBalancerDNS will be diplayed under value column in Outputs tab
 11. Copy the Load balancer DNS and paste it in the browser. 
 12. If all resources were configured correctly, the MSR will be up and running.

