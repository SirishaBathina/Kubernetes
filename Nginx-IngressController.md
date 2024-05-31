# You can follow the steps from the  link else follow the below steps👇

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
```sh
cd provider
```
```sh
cd aws
```
```sh
# Enter the below command to create the controller

kubectl apply -f deploy.yaml
```
 ```sh
kubectl get ns
```
We have created the ingress controller but let’s see what and all the things are created.
```sh
kubectl get all -n ingress-nginx
```
If you go to the AWS management console we can see the network load balancer has been created

# Next, we can deploy our application using the ingress controller.

```sh
vim deployment.yaml
```

```sh
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  selector:
    matchLabels:
      run: my-app
  replicas: 1
  template:
    metadata:
      labels:
        run: my-app
    spec:
      containers:
      - name: my-app
        image: devopsbathinasirisha28/nginxapp:latest
        ports:
        - containerPort: 80
```
```sh
vi svc.yaml
```

```sh
apiVersion: v1
kind: Service
metadata:
  name: my-app
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    run: my-app
  type: ClusterIP
```
```sh
kubectl apply -f deployment.yaml
```
```sh
kubectl apply -f svc.yaml
```
```sh
 kubectl get svc
```
```sh
kubectl get pods
```

```sh
kubectl describe svc my-app
```

###Our service is up and running. Now let’s create the ingress controller

# Create new file to create ingress controller
```sh
vi ingress.yaml
```
```sh
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: vpro-ingress
  annotations:
    nginx.ingress.kubernetes.io/use-regex: "true"
spec:
  ingressClassName: nginx
  rules:
  - host: afe73fc7dbee7433db50796c16ade927-2b7ce3742e5bb884.elb.ap-south-1.amazonaws.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-app
            port:
              number: 80
```

```sh
kubectl apply -f ingress.yaml
```
```sh
kubectl get ingress
```
```sh
curl afe73fc7dbee7433db50796c16ade927-2b7ce3742e5bb884.elb.ap-south-1.amazonaws.com
```
# troubleshoot purpose

```sh
kubectl exec -it <pod-name> -n <namespace> -- /bin/bash
```
```sh
kubectl logs -n ingress-nginx <nginx-ingress-controller-pod>
```
```sh
kubectl logs my-app-5c6fdc8b57-gfzcj
```
```sh
kubectl logs my-app-<pod-id>
```
```sh
docker run -dit nginx
```
```sh
docker images
```
```sh
docker run -dit -p 80:80 nginx:latest
```

