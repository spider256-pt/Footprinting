Developed By Sun Microsystems 
same purpose as SMB
Can Access file over a network as if they were local.

## Important Points About NFS:

1. NFSv4 uses either UDP or TCP port 2049 to run the device. {Simplifies the use of protocol across the firewall}.

2. NFS is Based on (ONC-RPC/SUN-RPC){**Open Network Computing Remote Procedure Call**}Protocol exposed on TCP and UDP ports 111.




### Default Configuration options
1. rw - read and write permission
2. ro - read only permission
3. sync - Synchronous data transfer {slower}
4. async - Asynchronous data transfer {faster}
5. secure - ports above 1024 will not be used
6. insecure - ports above 1024 will be used
7. no_subtree_check - disables checking of sub dir
8. root_squash - Assigns all permissions to files of root UID/GID 0 to the UID/GID of anonymous, which prevents `root` from accessing files on an NFS mount.

```shell-session
echo '/mnt/nfs  10.129.14.0/24(sync,no_subtree_check)'
```
*we have shared /mnt/nfs to the subnet 10.129.14.0/24
this means that all the hosts on the network will be able to mount NFS share and inspect the contents of the folder.*


### Dangerous Settings of NFS
1. rw - read and write permission 
2. insecure - ports above 1024 will be used 
3. nohide - If another file system was mounted below an exported directory, this directory is exported by its own exports entry
4. no_root_squash - all file created by root are kept with the UID/GID 0.

### Footprinting the Service

a.  Nmap: nmap <taget> -p111,2049 -sV -sC  
	by using nmap and scanning the known ports can give many information about NFS service and the hosts via RPC.
		 

b. nmap --scripts nfs* <target> -sV -p111, 2049 
		this script will run al the nfs script from NSE and can show contents of the share and its stats.

{Once NFS service is discovered} the it csan be mount to the local machine.
some imp commnads

## Show Available NFS Shares

1. showmount -e <taget>

##Mounting NFS Share

1. mkdir <name-NFS>
2. sudo mount -t nfs 10.129.14.128:/ ./<name-NFS>/ -o nolock
3. cd <name.NFS>
4. tree.

##List Contents with Username & Group Name
cd
1. ls -l mnt/nfs/

## List Contents with UIDs & GUIDs

1. ls -n mnt/nfs/

[Note:It is important to note that if the `root_squash` option is set, we cannot edit the `backup.sh` file even as `root`]*

##Unmounting 

1. cd ..
2. sudo unmount ./<name-NFS>


[[Nmap Basics]]
[[Footprinting important commands]]