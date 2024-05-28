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
  sudo systemctl restart NFS-kernel-server
```
