https://medium.com/@muppedaanvesh/rolling-update-recreate-deployment-strategies-in-kubernetes-%EF%B8%8F-327b59f27202

Save the below manifest file as rolling-update-deploy.yaml

kubectl apply -f rolling-update-deploy.yaml

$ kubectl get po
NAME                            READY   STATUS    RESTARTS   AGE
echo-app-perc-95f589c4c-2w2cb   1/1     Running   0          29s
echo-app-perc-95f589c4c-ctzhv   1/1     Running   0          29s
echo-app-perc-95f589c4c-n6b62   1/1     Running   0          29s
echo-app-perc-95f589c4c-qt95z   1/1     Running   0          29s
echo-app-perc-95f589c4c-t8d5h   1/1     Running   0          29s

We deployed the application with 5 replicas and now let’s upgrade the image version from v1.0.0 to v2.0.0. After applying the changes,
we will observe how the rollout strategy works and understand the behavior of maxUnavailable and maxSurge.

$ kubectl get po                   
NAME                             READY   STATUS              RESTARTS   AGE
echo-app-perc-65c66d895b-kphbw   0/1     ContainerCreating   0          2s
echo-app-perc-65c66d895b-tn2f4   0/1     ContainerCreating   0          2s
echo-app-perc-95f589c4c-2w2cb    1/1     Terminating         0          7m51s
echo-app-perc-95f589c4c-ctzhv    1/1     Running             0          7m51s
echo-app-perc-95f589c4c-n6b62    1/1     Running             0          7m51s
echo-app-perc-95f589c4c-qt95z    1/1     Running             0          7m51s
echo-app-perc-95f589c4c-t8d5h    1/1     Running             0          7m51s
