1 𝐤𝐮𝐛𝐞𝐜𝐭𝐥 𝐠𝐞𝐭
→ kubectl get pods (list pods)
→ kubectl get deployments (list deployments)
→ kubectl get services (list services)
→ kubectl get all (list most resources in a namespace)

2 𝐤𝐮𝐛𝐞𝐜𝐭𝐥 𝐝𝐞𝐬𝐜𝐫𝐢𝐛𝐞
→ kubectl describe pod my-pod
→ kubectl describe node my-node

3 𝐤𝐮𝐛𝐞𝐜𝐭𝐥 𝐜𝐫𝐞𝐚𝐭𝐞
→ kubectl create -f my-deployment.yaml

4 𝐤𝐮𝐛𝐞𝐜𝐭𝐥 𝐚𝐩𝐩𝐥𝐲
→ kubectl apply -f my-deployment.yaml (apply a deployment definition)

5 𝐤𝐮𝐛𝐞𝐜𝐭𝐥 𝐝𝐞𝐥𝐞𝐭𝐞
→ kubectl delete pod my-pod
→ kubectl delete service my-service

Debugging and Troubleshooting

6 𝐤𝐮𝐛𝐞𝐜𝐭𝐥 𝐥𝐨𝐠𝐬
→ kubectl logs my-pod
→ kubectl logs my-pod -c my-container (specify a container)

7 𝐤𝐮𝐛𝐞𝐜𝐭𝐥 𝐞𝐱𝐞𝐜
→ kubectl exec -it my-pod -- bash (interactive shell)

8 𝐤𝐮𝐛𝐞𝐜𝐭𝐥 𝐩𝐨𝐫𝐭-𝐟𝐨𝐫𝐰𝐚𝐫𝐝
→ kubectl port-forward my-pod 8080:80

9 𝐤𝐮𝐛𝐞𝐜𝐭𝐥 𝐭𝐨𝐩
→ kubectl top pod (pod resource usage) 
→ kubectl top node (node resource usage)

10 𝐤𝐮𝐛𝐞𝐜𝐭𝐥 𝐞𝐱𝐩𝐥𝐚𝐢𝐧
→ kubectl explain pod 
→ kubectl explain pod.spec (more specific)

Managing Workloads

11 𝐤𝐮𝐛𝐞𝐜𝐭𝐥 𝐫𝐨𝐥𝐥𝐨𝐮𝐭
→ kubectl rollout status deployment/my-deployment 
→ kubectl rollout undo deployment/my-deployment

12 𝐤𝐮𝐛𝐞𝐜𝐭𝐥 𝐬𝐜𝐚𝐥𝐞
→ kubectl scale deployment/my-deployment --replicas=5

13 𝐤𝐮𝐛𝐞𝐜𝐭𝐥 𝐞𝐝𝐢𝐭
→ kubectl edit deployment my-deployment
