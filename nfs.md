```sh
sudo apt install nfs-kernel-server
````
```sh
sudo apt update
```
```sh
sudo mkdir -p /mnt/NFS_share
```
sudo chown -R nobody:nogroup /mnt/NFS
```sh
sudo vim /etc/exports
```
```sh
/mnt/NFS_share *(rw,sync,no_subtree_check,insecure)
```
sudo exportfs -a
 - to check exports 
```sh
 sudo exportfs -v or showmount -e 
```
```sh
  sudo systemctl start nfs-kernel-server
```
```sh
  sudo systemctl status nfs-kernel-server
```
```sh
apt install nfs-common
```
```sh
mount -t NFS <server ip>:/mnt/nfs_share /mn
```
