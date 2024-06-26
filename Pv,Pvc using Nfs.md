                                                  # Pv, Pvc using nfs-server


##Ec2Instances:
*Kops-up&running
*Nfs-server

Create a Nfs-server instance open port 2049 in  nfs-server instance and worker nodes in the cluster.(all nodes open port and install nfs)
Create volume and attach to kops
In Nfs-server:
Follow below steps

```sh 
sudo apt install nfs-kernel-server
```
```sh
sudo systemctl enable nfs-server
```
```sh
sudo mkfs.ext4 /dev/xvdf
```
```sh 
mkdir /app
```
```sh 
mount  /dev/xvdb  /app
```
```sh 
df -h
```
```sh 
sudo vim /etc/exports 
```
```sh 
/app *(rw, sync)
```
```sh
sudo exportfs -a
```
```sh 
sudo chown -R root:root  /app
```
```sh
sudo  chmod 777  /app
```
 

 
 
 

We have to create pv.yaml and pvc.yaml
In kops:
```sh
vi pv.yaml
```
```sh 
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nfsvol
spec:
  capacity:
    storage: 10Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: manual
  mountOptions:
    - hard
    - nfsvers=4.1
  nfs:
    path: /app
    server: 43.204.212.61 (nfs-server-Ip)
```
```sh

kubectl apply -f pv.yaml
```

create pvc.yaml file

```sh
vi pvc.yaml
```
```sh
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nfsvol
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 5Gi
```
```sh
kubectl apply -f pvc.yaml
```
create deployment.yaml file

```sh
vi deployment.yaml
```
```sh
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
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
        image: devopsbathinasirisha28/nginxapp:latest
        ports:
        - containerPort: 80
        volumeMounts:
        - mountPath: /var/www/html
          name: nfsvol
      volumes:
      - name: nfsvol
        persistentVolumeClaim:
          claimName: nfsvol
```
```sh
kubectl apply -f deployment.yaml
```
 


 
 
