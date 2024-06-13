Vertical Pod Autoscaling (VPA):
Vertical Pod Autoscaling (VPA) adjusts the CPU and memory resource requests and limits for your pods. Instead of adding more pods, VPA modifies the resources allocated to existing pods.


## Step 1: Install VPA

```sh
git clone https://github.com/kubernetes/autoscaler.git
```
```sh
cd autoscaler
````
autoscaler/vertical-pod-autoscaler/hack  ==run the script
```sh
./vpa-up.sh
``` 
Verify Installation:
```sh
kubectl get pods -n kube-system | grep vpa
``` 
## Step 2: Create a Deployment

Create a file named vpa-deployment.yaml with the following content:
```sh
apiVersion: apps/v1
kind: Deployment
metadata:
  name: high-cpu-utilization-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: cpu-utilization-app
  template:
    metadata:
      labels:
        app: cpu-utilization-app
    spec:
      containers:
      - name: cpu-utilization-container
        image: ubuntu
        command: ["/bin/sh", "-c", "apt-get update && apt-get install -y stress-ng && while true; do stress-ng --cpu 1; done"]
        resources:
          limits:
            cpu: "0.05"
          requests:
            cpu: "0.05"
```
This deployment repeatedly runs a CPU stress test using the `stress-ng` tool, consuming a small but continuous amount of CPU (limited to 0.05 cores) to simulate high CPU utilization.

Apply the deployment:

```sh
 kubectl apply -f vpa-deployment.yaml
```
Step 3: Create a VPA
Create a file named vpa.yaml with the following content:

```sh
apiVersion: "autoscaling.k8s.io/v1"
kind: VerticalPodAutoscaler
metadata:
  name: stress-vpa
spec:
  targetRef:
    apiVersion: "apps/v1"
    kind: Deployment
    name: high-cpu-utilization-deployment
  updatePolicy:
    updateMode: Auto
  resourcePolicy:
    containerPolicies:
      - containerName: '*'
        minAllowed:
          cpu: 100m
          memory: 50Mi
        maxAllowed:
          cpu: 200m  #maximum vpa will be allocating this many cpus even if demand is higher.
          memory: 500Mi
        controlledResources: ["cpu", "memory"]
```
Apply the VPA:

```sh
kubectl apply -f vpa.yaml
```
Step 4: Testing
First, let’s check the initial CPU utilization of the target pods:

 
Verify the CPU requests for the pods:
```sh
kubectl get po -o jsonpath='{.items[*].spec.containers[*].resources.requests.cpu}'
```
Next, check the VPA status:
 
Wait for some time and then check the pod status again:
 
Check the updated CPU requests:
```sh
kubectl get po -o jsonpath="{.items[*].spec.containers[*].resources.requests.cpu}"
```
 
Monitor the updated CPU utilization:
 

As observed, the pods were restarted and their CPU request values increased from 50m to 100m due to the VPA’s minAllowed setting. The pods will continue generating load until they reach their limits.
