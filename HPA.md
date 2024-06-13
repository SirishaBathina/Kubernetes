###https://medium.com/@muppedaanvesh/a-hands-on-guide-to-kubernetes-horizontal-vertical-pod-autoscalers-%EF%B8%8F-58903382ef71
## Autoscaling:
Autoscaling is a way to automatically scale up or down the n.of compute resources that are allocated to our application based on demand
## Types:
* Horizontal Pod Autoscaling (HPA)
* Vertical Pod Autoscaling (VPA)
##Horizontal Pod Autoscaling (HPA):
Horizontal Pod Autoscaling (HPA) automatically scales the number of pods based on  CPU utilization (or other select metrics). This allows your application to scale out (add more pods) or scale in (reduce the number of pods).
## To setup HPA in K8Scluster:
* Install metric server
* Deploy sample app
* Create a service
* Deploy HPA
* Increase the load
* Monitor the HPA Events
## Metric Server Setup
The Metrics Server collects resource usage metrics from the cluster’s nodes and pods, which are necessary for autoscaling decisions.
## Download the Components Manifest:

```sh
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```
Verify Installation
```sh
kubectl get pods -n kube-system | grep metrics-server
```
Step 1: Create a Deployment

```sh
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hpa-deploy
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        resources:
          requests:
            cpu: "25m"
          limits:
            cpu: "200m"
```

Apply the deployment:
```sh
kubectl apply -f hpa-deployment.yaml
```
## Step 2: Create a Service
Create a file named nginx-service.yaml with the following content:

```sh
apiVersion: v1
kind: Service
metadata:
  name: nginx-svc
  labels:
    app: nginx
spec:
  ports:
  - port: 80
  selector:
    app: nginx 
```
Apply the service:
```sh
kubectl apply -f nginx-service.yaml
```
## Step 3: Create an HPA
Create a file named hpa.yaml with the following content:

```sh
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: nginx-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: hpa-deploy
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50 
```
Apply the HPA:
```sh
kubectl apply -f hpa.yaml
```

# Testing
 

Run this command to generate load:
```sh
kubectl run -i --tty load-generator --rm --image=busybox:1.28 --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://nginx-svc; done"
```
Check the CPU utilization of the pods:
```sh
 kubectl top pods
```
Monitor the HPA status:
 ```sh
kubectl get hpa -w
```
