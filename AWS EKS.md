                              Setup Kubernetes on Amazon EKS

You can follow same procedure in the official AWS document Getting started with Amazon EKS – eksctl
Pre-requisites:
an EC2 Instance
AWS EKS Setup
Setup kubectl

a. Download kubectl version 1.20
b. Grant execution permissions to kubectl executable
c. Move kubectl onto /usr/local/bin
d. Test that your kubectl installation was successful
```sh
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
```
```sh
chmod +x./kubectl
```
```sh
mv./kubectl /usr/local/bin 
```
```sh
      kubectl version --short --client
```
# Setup eksctl
a. Download and extract the latest release
b. Move the extracted binary to /usr/local/bin
c. Test that your eksctl installation was successful
```sh
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
``
```sh
sudo  mv /tmp/eksctl /usr/local/bin
```
```sh
eksctl version
```
##1.	Create an IAM Role and attached it to EC2 instance
Note: create IAM user with programmatic access if your bootstrap system is outside of AWS
IAM user should have access to

IAM
EC2
VPC
CloudFormation
# 2.Create your cluster and nodes
```sh
eksctl create cluster --name cluster-name --region region-name --node-        type instance-type --nodes-min 2 --nodes-max 2  
```

   #   To create the EKS cluster

    ```sh
    eksctl create cluster --name ekssiri-cluster28 --region ap-south-1 --node-   type t2.small --nodes-min 2 --nodes-max 2
```
 
 
# 3.   To delete the EKS cluster
```sh
eksctl delete cluster --name=ekssiri-cluster28 --region=ap-south-1
```
#Validate your cluster using by creating by checking nodes and by creating a pod
```sh
kubectl get nodes
```
```sh
kubectl run pod tomcat --image=tomcat 
```  
