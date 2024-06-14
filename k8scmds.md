kubectl version:
 - Check the client and server Kubernetes version.

2. kubectl cluster-info:
 - Display cluster information, including the master node's URL.

3. kubectl get nodes:
 - List all nodes in the cluster.

4. kubectl get pods:
 - List all pods in the default namespace.

5. kubectl get services:
 - List all services in the default namespace.

6. kubectl get deployments:
 - List all deployments in the default namespace.

7. kubectl get namespaces:
 - List all namespaces in the cluster.

8. kubectl describe pod <pod_name>:
 - Display detailed information about a specific pod.

9. kubectl logs <pod_name>:
 - View the logs of a specific pod.

10. kubectl exec -it <pod_name> -- /bin/bash:
 - Open an interactive shell inside a pod for troubleshooting.

11. kubectl create deployment <name> --image=<image>:
 - Create a new deployment with the specified image.

12. kubectl expose deployment <name> --port=<port>:
 - Expose a deployment as a service.

13. kubectl scale deployment <name> --replicas=<num>:
 - Scale the number of replicas in a deployment.

14. kubectl delete pod <pod_name>:
 - Delete a specific pod.

15. kubectl delete deployment <name>:
 - Delete a deployment.

16. kubectl delete service <service_name>:
 - Delete a service.

17. kubectl get pods -o wide:
 - Display additional information (such as node) for each pod.

18. kubectl get events:
 - View cluster events.

19. kubectl apply -f <file.yaml>:
 - Apply configurations from a YAML file.

20. kubectl get replicaset:
 - List all replica sets.

21. kubectl get configmaps:
 - List all config maps.

22. kubectl get secrets:
 - List all secrets.

23. kubectl edit <resource_type> <resource_name>:
 - Edit a resource in the default text editor.

24. kubectl rollout status deployment/<name>:
 - Check the status of a deployment rollout.

25. kubectl rollout history deployment/<name>:
 - View the rollout history of a deployment.

26. kubectl rollout undo deployment/<name>:
 - Rollback a deployment to a previous revision.

27. kubectl get all --all-namespaces:
 - List all resources in all namespaces.

28. kubectl port-forward <pod_name> <local_port>:<remote_port>:
 - Forward ports from a local machine to a pod.

29. kubectl top nodes:
 - Show resource usage (CPU and memory) for nodes.

30. kubectl top pods:
 - Show resource usage for pods.

31. kubectl get pod <pod_name> -o yaml:
 - Display detailed YAML configuration of a pod.

32. kubectl label pod <pod_name> <label_key>=<label_value>:
 - Add a label to a pod.
