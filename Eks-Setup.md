Step 1:Launch new Ubuntu VM using AWS Ec2 ( t2.micro )

Connect to machine and install kubectl using below command
$curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
$chmod +x ./kubectl
$sudo mv ./kubectl /usr/local/bin
$kubectl version --short --client


Install AWS CLI latest version using below commands:
$sudo apt install unzip
$curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
$unzip awscliv2.zip
$sudo ./aws/install
$aws --version


Install eksctl using below commands:
$curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
$sudo mv /tmp/eksctl /usr/local/bin
$eksctl version


Step 2:
Create New Role in AWS ec2 using IAM service ( Select Usecase - ec2 )

Add below permissions  policies for the role
IAMfullaccess
AmazonVPCfullaccess
AmazonEC2fullaccess
AWSCloudFomrationfullaccess
Administratoracces
Enter Role Name (EKSEC2Role-1)



Attach created role to EKS Management Host 
(Select EC2 => Click on Security => Modify IAM Role => attach IAM role we have created)



Step 3: Create EKS Cluster using eksctl
Syntax:
eksctl create cluster --name cluster-name --region region-name --node-type instance-type --nodes-min 2 --nodes-max 2 \ --zones ,


 For mumbai Region server
 $eksctl create cluster --name aamirit-cluster  --region ap-south-1 --node-type t2.medium  --zones ap-south-1a,ap-south-1b

 For US Region server
 $eksctl create cluster --name aamirit-cluster  --region us-east-1 --node-type t2.medium  --zones us-east-1a,us-east-1b


 Step 4: After  practising, delete Cluster and other resources we have used in AWS Cloud to avoid billing
  Deleting mumbai region cluster
 $eksctl delete cluster --name aamirit-cluster --region ap-south-1

    steps to delete already created cluster from AWS GUI
    A First click on cluster name link->Compute->ng-b54xxx(delete it)    
