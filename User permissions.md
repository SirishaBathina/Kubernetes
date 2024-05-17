
#A Step-by-Step Guide to Creating Users in Kubernetes
##Followed by this Url

https://aungzanbaw.medium.com/a-step-by-step-guide-to-creating-users-in-kubernetes-6a5a2cfd8c71
1.	Generate certificates for the user.
2.	Create a certificate signing request (CSR).
3.	Sign the certificate using the cluster certificate authority.
4.	Create a configuration specific to the user.
5.	Add RBAC rules for the user or their group.
1. Generate certificates for the user.
```sh
openssl genpkey -out siri.key -algorithm Ed25519
```

```sh 
openssl req -new -key siri.key -out siri.csr -subj "/CN=siri,/O=edit"*
```
2. Create a certificate signing request (CSR).
```sh
cat siri.csr | base64 | tr -d "\n"
 ```
 

 
3. Sign the certificate using the cluster certificate authority.
```sh
kubectl certificate approve siri
```
```sh
kubectl describe csr/siri
```
4. Create a configuration specific to the user.
   ```sh
kubectl get csr/siri -o jsonpath="{. status.certificate}" | base64 -d > siri.crt
```
```sh
cp  ~/.kube/config siri-kube-config
```
```sh
kubectl config get-clusters
```
```sh 
kubectl --kubeconfig siri-kube-config config set-credentials siri --client-key siri.key --client-certificate siri.csr --embed-certs=true
```
```sh
kubectl --kubeconfig siri-kube-config config set-context siri --cluster default --user siri
 ```

5. Add RBAC rules for the user or their group.
   ```sh
kubectl create role pod-manager --verb=create,list,get --resource=pods --namespace=default
```
Bind the Role with a ClusterRoleBinding:
```sh
kubectl create clusterrolebinding siri-pod-manager — clusterrole=pod-manager — user=siri
```
Verify authorization using kubectl auth can-i:
```sh
kubectl auth can-i create deployments --namespace=default --as=siri
```
no
```sh
kubectl auth can-i create secrets --namespace=default --as=siri
```
no
```sh
kubectl auth can-i get pods --namespace=default --as=siri
```
yes


  
 kubectl apply -f pod-reader-role.yaml

kubectl apply -f read-pods-binding.yaml
















