--------------------------------------------
--------------------------------------------
### NFS Recon cheat sheet

--------------------------------------------
--------------------------------------------

*Tools used :*         mount, showmount, umount.  
*Goal* :                  Know how to collect information and connect to NFS shares.  

 NFS is a network file system developed by Sun Microsystems and has the same purpose as SMB. Its purpose is to access file systems over a network as if they were local. However, it uses an entirely different protocol. NFS is used between Linux and Unix systems.

#### Identifying NFS :

NFS server runs under port `111` and `2049`. Here is an example of NMAP scan with NFS server opened :

```sh
dawnl3ss@htb[/htb]$ sudo nmap 10.129.14.128 -p111,2049 -sV -sC

Starting Nmap 7.80 ( https://nmap.org ) at 2021-09-19 17:12 CEST
Nmap scan report for 10.129.14.128
Host is up (0.00018s latency).

PORT    STATE SERVICE VERSION
111/tcp open  rpcbind 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   ...SNIP...
2049/tcp open  nfs_acl 3 (RPC #100227)
MAC Address: 00:00:00:00:00:00 (VMware)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.58 seconds
```

#### Footprinting :

Once we identified a NFS service running, we should enumerate it to find some pieces of information. We can do that with the help of some commands.

###### RPC NSE :

We can use a NMAP NSE script to reveal more information about the NFS shares available on the victim machine :

```sh
dawnl3ss@htb[/htb]$ nmap -sV -p 111,2049 IP_ADDR --script nfs*
```

The "IP_ADDR" should be replaced by the ip address of the targeted machine.

###### Interact with NFS :

Once we have discovered that there was a NFS server running, we should be able to interact with it to get the content of the shares.

- Show available shares :

```sh
dawnl3ss@htb[/htb]$ showmount -e IP_ADDR
```

The flag "-e" is used to "export" shares.

The 'IP_ADDR' should be replaced by the ip address of the targeted machine.

- Mount shares :

```sh
dawnl3ss@htb[/htb]$ mkdir target-NFS
dawnl3ss@htb[/htb]$ sudo mount -t nfs IP_ADDR:/ target-NFS/ -o nolock
dawnl3ss@htb[/htb]$ cd target-NFS
dawnl3ss@htb[/htb]$ tree .

.
└── mnt
    └── nfs
        ├── id_rsa
        ├── id_rsa.pub
        └── nfs.share

2 directories, 3 files
```

The flag "-t" is used to precise over what network file system we will mount.

The 'IP_ADDR' should be replaced by the ip address of the targeted machine.

The `target-NFS/` parameter is the destination folder.

- Unmount shares :

```sh
dawnl3ss@htb[/htb]$ sudo umount ./target-NFS
```

#### Conclusion :

NFS is pretty simple to footprint and doesn't even require any type of authentication.
We can easily retrieve files and folders shared by NFS by using mount command.  



07/01/2024,  
Dawnless.

--------------------------------------------
--------------------------------------------