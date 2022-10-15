# Deploy IAC

 This project is part of a course in A Cloud Guru, for hands-on practice with Terraform and ansible to deploy an ifrastructure on AWS.

The deployment is for a distributed, multi-region Jenkins CI/CD deployment.

It is currently ongoing - 52% 

👾👾👾

---

## What has been done so far:

1. Backened stateful file was set to S3.

2. Providers.tf was set to work with 2 aws providers.

3. Variables.tf file was set.

4. In networks.tf AWS VPC were created on 2 different regions, with internet gateways and subnets.

5. security_groups.tf - there are 3 SG, "ls-sg" for the load balancer access, "jenkins-sg" for access from the LB to the jenkins master, and "jenkins-sg-oregon" for the connection to the Jenkins worker nodes.

6. Instances.tf contains AMI ID, key pair and EC2 instances for jenkins master and jenkins worker in each region.

7. Outputs.tf - showing the EC2 Ips.

  ---

## Prerequisites and instructions using this repo:

AWS account ☁️
- Have an AWS account to deploy the code to.

Installations 
- Install Terrform, Ansible and AWS-CLI on your workstation.
- Install boto3 python SDK for AWS
    *pip3 install boto3 --user*
	
User configurations:
- Configure a user with programmatic access only, and attach an IAM policy to him with relevant permissions. 

	Policy JSON file: https://raw.githubusercontent.com/linuxacademy/content-deploying-to-aws-ansible-terraform/master/iam_policies/terraform_deployment_iam_policy.json

- Configure the user on the environment, using it's key pair.
	*aws configure*

Clone code
- Clone the repository to your workstation.
	*git clone https://github.com/netashiloh/deploy_iac.git*

Set S3 bucket 🪣 for statefile 
- Create S3 bucket for the state file using aws cli.
	*aws s3api create-bucket --bucket <Bucket_name>*

- Edit the file "backened.tf" and change the bucket name to the bucket you've created. 
	Note: under bucket = "".

Key pair for EC2 🔑
- Create a key pair, and save the key on your workstation. *I saved mine under /tmp/iac_id_rsa.
	*ssh-keygen -t rsa*

- Make sure your private key has suitable permissions.
	*chmod 700 /tmp/iac_id_rsa*

- In instances.tf file, set the keypair path you chose under aws_key_pair resources(2 resources).

Run code
- In the repository folder "deploy_iac", run terraform init & terraform apply to set the environment.
	*terraform init
	terraform apply*