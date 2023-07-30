# AWS Sample Code Deploy Using Git

## 1. Create Two IAM Roles
*First you have to Create an IAM role (EC2 - CodeDeploy) Full Access much better for practise.
*Second You have to create separate CodeDeploy role.

![CodeDeploy Role](https://drive.google.com/file/d/1ebUxClrgNxrl_VFuoTVBGvYEb4BVPFLd/view?usp=drive_link)

## 1.1 Why are we creating an IAM Role?

EC2 Instance to CodeDeploy are different services in AWS so to connect this service we are creating an IAM Role (Service to Service) in AWS.

## 2. Launch a Instance to Deploy our Sample App.

*EC2 -> Launch instance -> Name it as "sampleapp" or what ever -> I'll choose Amazon Linux and you Choose any OS -> Set security group (Open All Port for practice)
*Advanced details -> Attach the first created IAM Role(EC2-CodeDeploy)
*Atlast User data -> Copy paste the scripts from user_data_script.txt [Install CodeDeploy Agent on Amazon linux](https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-linux.html).

Script Varies for other OS:
[Install CodeDeploy Agent On Ubuntu](https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-ubuntu.html).

[Install CodeDeploy Agent On Windows Server](https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-windows.html).

Note: You Can Modify IAM Role after the Instance Launched.

## 3. Create Sample Application Name on CodeDeploy Section

*Go to CodeDeploy Section on AWS console.
*On Application Section, click create application.
*Give any name like "sampleapp" in Application name.
*On Compute Platform -> EC2/On Premises.

![Create Application](https://drive.google.com/file/d/1ebUxClrgNxrl_VFuoTVBGvYEb4BVPFLd/view?usp=drive_link)

## 4. Create Deployment Group

*Once you create Application, Create Deployment Group Option will be available.
*Name the deployment group "sampleappdg" or whatever.
*Attach the second role which we created at first 'CodeDeploy Role'
*Deployment type -> In-place
*Environment Configuration -> EC2 Instance -> Select our "sampleapp" instance
*Disable Load Balancer. If you need you can enable.
*Click Create deployment group.

## 4. Code Pipeline
*Step 1: Pipeline name -> sampleapp-pl
  *Service role -> New service role
  *Keep other options default and click next
*Step 2: Source stage -> Source provider -> GitHub Version 2
  *Connect to GitHub
  *Repository name -> repository which has the source code
  *Enable Change detection options and click next
*Step 3: Skip build stage
*Step 4: Deploy stage -> Choose AWS CodeDeploy in Deploy Provider, fill other options and click next
*Step 5: Click Create pipeline