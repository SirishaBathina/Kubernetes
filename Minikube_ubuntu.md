# Docker install
```sh
sudo apt-get update
```
```sh
sudo apt-get install ca-certificates curl
```
```sh
sudo install -m 0755 -d /etc/apt/keyrings
```
```sh
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
```
```sh
sudo chmod a+r /etc/apt/keyrings/docker.asc
```
# Add the repository to Apt sources:

```sh
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
```
```sh
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```sh
sudo apt-get update
```
```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
```sh
sudo service docker start
```
 ================================================================
# kubectl install

```sh
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
```
```sh
chmod +x ./kubectl
```
```sh
sudo mv ./kubectl /usr/local/bin/kubectl
```
```sh
kubectl version –client
```
================================================================

# minikube install
##To install the latest minikube stable release on x86-64 Linux using binary download:
```sh
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
```sh
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
```

```sh
sudo minikube start --driver=docker --force
```
 
```sh
minikube status
```
