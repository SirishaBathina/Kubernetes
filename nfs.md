sudo apt install nfs-kernel-server
sudo apt update
sudo mkdir -p /mnt/NFS_share
sudo chown -R nobody:nogroup /mnt/NFS
sudo vim /etc/exports

/mnt/NFS_share *(rw,sync,no_subtree_check,insecure)
sudo exportfs -a
 - to check exports 
 sudo exportfs -v or showmount -e 
  sudo systemctl restart NFS-kernel-server
