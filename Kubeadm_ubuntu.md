
#Please refer below url

#https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

##https://varunmanik1.medium.com/setting-up-a-kubernetes-cluster-on-aws-ec2-with-ubuntu-22-04-lts-and-kubeadm-5c54930a4659

#In master node open port 6443

Kubeadm with ubuntu

# Step 1: create two ec2 instances. master and worker .

# Step 2: connect to it using SSH

login as ubuntu user
 
 Do the following steps both master and worker up to swapoff -a

# Step 3 :
update package 

```sh
sudo apt update 
```
# Install the docker 
```sh
apt install docker.io -y
```
# Start and enable the docker
 
```sh
systemctl start docker
```
```sh
systemctl enable docker
```
# Step 4: Update the apt package index and install packages needed to use the Kubernetes apt repository:
```sh
sudo apt-get update
```
```sh
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
```
# Step 5 : Add the Kubernetes signing key and repository
```sh
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.29/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```
```sh
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.29/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
# Step 6 : Update the apt package index, install kubelet, kubeadm and kubectl, and pin their version
```sh
sudo apt-get update
```
```sh
sudo apt-get install -y kubelet kubeadm kubectl
```
```sh
sudo apt-mark hold kubelet kubeadm kubectl
``` 
# Step 7 :Initializing Your Kubernetes Cluster
#Disable swap memory to satisfy the kubelet prerequisites
Initialize the cluster with kubeadm

```sh
swapoff –a
```
```sh
kubeadm init            ======masteronly
``` 
Kubeadm init command  only for master not for worker.
In kubeadm init we can get the token. That token we can execute in the worker nodes.
 From the below steps we can execute master only. 
# Step 8: Setting Up Kubectl
As a regular user, set up the kubeconfig
```sh
mkdir -p $HOME/.kube
```
```sh
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
```
```sh
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
# Step 9: Applying a CNI Plugin
Apply a network plugin 
```sh
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
``` 
# Step 10: Verifying the Cluster
```sh
kubectl get nodes
``` 

