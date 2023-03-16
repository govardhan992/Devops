# Setup Kubernetes on Amazon EKS


You can follow same procedure in the official  AWS document [Getting started with Amazon EKS – eksctl](https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html)   

#### Pre-requisites: 
  - an EC2 Instance 
#### AWS EKS Setup
1.Installing or updating the latest version of the AWS CLI
```sh
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws --version
```
2. To install or update kubectl on Linux
```sh   
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.25.6/2023-01-30/bin/linux/amd64/kubectl
chmod a+x kubectl
mv kubectl /usr/local/bin
kubectl version
```

3. To install or update eksctl
a. Download and extract the latest release of eksctl with the following command.
b. Move the extracted binary to /usr/local/bin.
c.Test that your installation was successful or not
```sh
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
```

4. Create an IAM Role and attache it to EC2 instance    
   `Note: create IAM user with programmatic access if your bootstrap system is outside of AWS`   
   IAM user should have access to   
   IAM   
   EC2   
   VPC    
   CloudFormation   
   
5. Create your cluster and nodes
```sh
eksctl create cluster --name dev-cluster --region us-east-2 --node-type t2.small
```    


   
  
