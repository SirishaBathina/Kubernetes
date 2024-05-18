                                      KOPS ON UBUNTU

###Create Ubuntu EC2 instance
#install AWSCLI
curl https://s3.amazonaws.com/aws-cli/awscli-bundle.zip -o awscli-bundle.zip

 sudo apt update

 sudo apt install unzip python
 unzip awscli-bundle.zip
     sudo apt-get install unzip 
    ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
                                  (Or)

sudo snap install aws-cli --classic
$ aws –version
$ aws configure

#  Install kubectl on ubuntu instance
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo  mv ./kubectl /usr/local/bin/kubectl
#Install kops on ubuntu instance

  curl -LO            https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
 chmod +x kops-linux-amd64
  sudo mv kops-linux-amd64 /usr/local/bin/kops
##Create an IAM user/role with Route53, EC2, IAM and S3 full access
Attach IAM role to ubuntu instance

aws configure
Create a Route53 private hosted zone (you can create Public hosted zone if you have a domain)
Route53 --> hosted zones --> created hosted zone  
Domain Name: siri.com

create an S3 bucket
    aws s3 mb s3://clusters.dev.siri.com
Expose environment variable:
             export KOPS_STATE_STORE=s3://clusters.dev.siri.com
vi  /etc/profile
export KOPS_STATE_STORE=s3://clusters.dev.siri.com


Create ssh keys before creating cluster
 ssh-keygen
Create Kubernetes cluster definitions on S3 bucket
 kops create cluster --cloud=aws --zones=ap-south-1b --      name=clusters.dev.siri.com --dns-zone=siri.com --dns private

 kops create cluster --zones=ap-south-1b clusters.dev.siri.com --dns- zone=siri.com --dns private

kops edit ig --name=clusters.dev.siri.com nodes-ap-south-1b

kops delete cluster --name clusters.dev.siri.com --yes
