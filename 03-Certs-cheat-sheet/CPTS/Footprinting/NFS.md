# NFS

## Default configuration

```
cat /etc/exports
```

```
rw	Read and write permissions.
ro	Read only permissions.
sync	Synchronous data transfer. (A bit slower)
async	Asynchronous data transfer. (A bit faster)
secure	Ports above 1024 will not be used.
insecure	Ports above 1024 will be used.
no_subtree_check	This option disables the checking of subdirectory trees.
root_squash	Assigns all permissions to files of root UID/GID 0 to the UID/GID of anonymous, which prevents root from accessing files on an NFS mount.
```

```
root@nfs:~# echo '/mnt/nfs  10.129.14.0/24(sync,no_subtree_check)' >> /etc/exports
root@nfs:~# systemctl restart nfs-kernel-server 
root@nfs:~# exportfs
```

## Dangerous settings

```
rw	Read and write permissions.
insecure	Ports above 1024 will be used.
nohide	If another file system was mounted below an exported directory, this directory is exported by its own exports entry.
no_root_squash	All files created by root are kept with the UID/GID 0.
```

## Footprinting the service

```
sudo nmap 10.129.14.128 -p111,2049 -sV -sC
sudo nmap --script nfs* 10.129.14.128 -sV -p111,2049
```

## Show available NFS shares

```
showmount -e 10.129.14.128
```

## Mounting NFS shares

```
Ramisto@htb[/htb]$ mkdir target-NFS
Ramisto@htb[/htb]$ sudo mount -t nfs 10.129.14.128:/ ./target-NFS/ -o nolock
Ramisto@htb[/htb]$ cd target-NFS
Ramisto@htb[/htb]$ tree .
```

## List Contents with Usernames & Group Names, UIDs & GUIDs

```
ls -ln mnt/nfs/
```

## Unmounting

```
Ramisto@htb[/htb]$ cd ..
Ramisto@htb[/htb]$ sudo umount ./target-NFS
```
