Deploy IAC

This project is part of a course in A Cloud Guru, for hands-on practice with Terraform and ansible to deploy an ifrastructure on AWS.
The deployment is for a distributed, multi-region Jenkins CI/CD deployment.

It is currently ongoing - 52%


What has been done so far:
1. Backened stateful file was set to S3.
2. Providers.tf was set to work with 2 aws providers.
3. Variables.tf files were set.
4. In networks.tf AWS VPC were created on 2 different regions, with internet gateways and subnets.
5. security_groups.tf - there are 3 SG, "ls-sg" for the load balancer access, "jenkins-sg" for access from the LB to the jenkins master, and "jenkins-sg-oregon" for the connection to the Jenkins worker nodes.
6. Instances.tf contains AMI ID and key pair for jenkins master and jenkins worker in each region.

 ----- 

Prerequisites and instructions using this repo:
- Install Terrform, Ansible and AWS-CLI.
- Have an AWS account.
- Configure user with programmatic access only, and attach an IAM policy to him with relevant permissions.
  Policy JSON: https://raw.githubusercontent.com/linuxacademy/content-deploying-to-aws-ansible-terraform/master/iam_policies/terraform_deployment_iam_policy.json
- Have an AWS account configured on the environment, using the created user key pair (run: aws configure).
- Clone the repository to your workstation.
- Manually create S3 bucket for the state file. *It's manually for now, but can be created from a pipeline in the future.*
- Edit the file "backened.tf" and change the bucket name to the bucket you've created. Note: under bucket = "". Save the file.
- Create a key pair (ssh-keygen -t rsa), and save the key on your workstatio. I saved mine under /tmp/iac_id_rsa
- In instances.tf file make sure the path to the keypair is set to the path you chose under aws_key_pair resources(2 resources).
- Run terraform init & terraform apply to set the environment.