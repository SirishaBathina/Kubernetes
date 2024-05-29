# You can follow the steps from the above link else follow the below steps👇

```sh
https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.2/deploy/static/provider/aws/
```


```sh

git clone https://github.com/kubernetes/ingress-nginx.git
```
```sh
cd ingress-nginx
```
```sh
cd deploy
```
```sh
cd static
```
cd provider
```sh
cd aws
```
```sh
kubectl apply -f deploy.yaml
```
 ```sh
kubectl get ns
```
We have created the ingress controller but let’s see what and all the things are created.
```sh
kubectl get all -n ingress-nginx
```

# Next, we can deploy our application using the ingress controller.
