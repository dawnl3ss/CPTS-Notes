--------------------------------------------
--------------------------------------------
### SMB Recon cheat sheet

--------------------------------------------
--------------------------------------------

*Tools used :*         smbclient, rpclient, enum4linux, crackmapexec.  
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