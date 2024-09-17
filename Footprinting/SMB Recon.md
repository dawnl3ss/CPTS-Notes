--------------------------------------------
--------------------------------------------
### SMB Recon cheat sheet

--------------------------------------------
--------------------------------------------

*Tools used :*        smbclient, rpcclient, enum4linux.  
*Goal* :                  Know how to collect information and connect to SMB shares.  

SMB is a client-server protocol that regulates access to files and entire directories and other network resources such as printers, routers, or interfaces released for the network on Windows. The Linux equivalent is implemented with tools such as Samba.  

#### Identifying SMB :

SMB Server usually uses port `445`and `139`. Here is an example of NMAP scan with Samba opened:

```sh
dawnl3ss@htb[/htb]$ sudo nmap 10.129.14.128 -sV -sC -p139,445

Starting Nmap 7.80 ( https://nmap.org ) at 2021-09-19 15:15 CEST
Nmap scan report for sharing.inlanefreight.htb (10.129.14.128)
Host is up (0.00024s latency).

PORT    STATE SERVICE     VERSION
139/tcp open  netbios-ssn Samba smbd 4.6.2
445/tcp open  netbios-ssn Samba smbd 4.6.2
MAC Address: 00:00:00:00:00:00 (VMware)

Host script results:
|_nbstat: NetBIOS name: HTB, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-09-19T13:16:04
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.35 seconds
```

#### Footprinting :

Once we identified a SMB service running, we should enumerate it to find some pieces of information. We can do that with the help of some tools.

###### SMB Client :

- Enumerating Shares :

```sh
dawnl3ss@htb[/htb]$ smbclient -N -L //IP_ADDR
```

The flag "-L" is used to list all the shares.  

The flag "-N" is used to connect as Anonymous since we are allowed to connect as Anonymous as written in the NMAP scan.  

- Connecting to one Share :

```sh
dawnl3ss@htb[/htb]$ smbclient //IP_ADDR/share_name
```

The 'share_name' can be replaced with the share that we want to connect.

###### RPC Client :

rpcclient can be used to get plenty of information about the SMB server.

- Connecting to SMB server :

```sh
dawnl3ss@htb[/htb]$ rpcclient -U "" IP_ADDR
```

- Getting info :

```sh
rpcclient $> srvinfo

rpcclient $> enumdomains

rpcclient $> querydominfo

rpcclient $> netshareenumall

rpcclient $> netsharegetinfo share_name
```

The 'share_name' can be replaced with one of the shares we discovered with the `netshareenumall` command.

- Enumerating users :

```sh
rpcclient $> enumdomusers

user:[mrb3n] rid:[0x3e8]
user:[cry0l1t3] rid:[0x3e9]                         (example)
```

Since we have RIDs of users, we can get some information about them :

```sh
rpcclient $> queryuser RID
```

The 'RID' can be replaced with the RID of one user.

###### Enum4linux :

Enum4linux is a widely used tool to basically get all of the info that we listed before in one command.

- Installation :

```sh
dawnl3ss@htb[/htb]$ git clone https://github.com/cddmp/enum4linux-ng.git
dawnl3ss@htb[/htb]$ cd enum4linux-ng
dawnl3ss@htb[/htb]$ pip3 install -r requirements.txt
```

- Usage :

```sh
dawnl3ss@htb[/htb]$ ./enum4linux-ng.py IP_ADDR -A
```

The 'IP_ADDR' can be replaced with the target ip address.

#### Conclusion :

SMB is pretty simple to footprint if we can log as Anonymous. If we can't, we should find a username and a password.
The use of enum4linux is appreciate since it does pretty much all in one command.



07/01/2024,  
Dawnless.

--------------------------------------------
--------------------------------------------