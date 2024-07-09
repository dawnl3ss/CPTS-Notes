--------------------------------------------
--------------------------------------------
### DNS Recon cheat sheet

--------------------------------------------
--------------------------------------------

*Tools used :*         dig.  
*Goal* :                  Know how to collect information about a domain.  

DNS is an integral part of the Internet. For example, through domain names, such as [https://hardware-hub.fr](https://hardware-hub.fr), we can reach the web servers that the hosting provider has assigned one or more specific IP addresses. DNS is a system for resolving computer names into IP addresses, and it does not have a central database. Simplified, we can imagine it like a library with many different phone books. The information is distributed over many thousands of name servers

#### Record table :

Here is a double entry table with some of the most well-known DNS records associated with their role.

| **DNS Record** | **Description**                                                                                                                                                                                                                                   |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `A`            | Returns an IPv4 address of the requested domain as a result.                                                                                                                                                                                      |
| `AAAA`         | Returns an IPv6 address of the requested domain.                                                                                                                                                                                                  |
| `MX`           | Returns the responsible mail servers as a result.                                                                                                                                                                                                 |
| `NS`           | Returns the DNS servers (nameservers) of the domain.                                                                                                                                                                                              |
| `TXT`          | This record can contain various information. The all-rounder can be used, e.g., to validate the Google Search Console or validate SSL certificates. In addition, SPF and DMARC entries are set to validate mail traffic and protect it from spam. |
| `CNAME`        | This record serves as an alias for another domain name. If you want the domain www.hackthebox.eu to point to the same IP as hackthebox.eu, you would create an A record for hackthebox.eu and a CNAME record for www.hackthebox.eu.               |
| `PTR`          | The PTR record works the other way around (reverse lookup). It converts IP addresses into valid domain names.                                                                                                                                     |
| `SOA`          | Provides information about the corresponding DNS zone and email address of the administrative contact.                                                                                                                                            |

#### Footprinting :

Now that we know what DNS record is important and their own role, we should be able to dig deeper and find some information about a particular domain.

###### DIG :

- NS Query :

```sh
dawnl3ss@htb[/htb]$ dig ns domain.com @IP_ADDR
```

The '`domain.com`' should be replaced with the domain that we want to footprint.

The '`IP_ADDR`' should be replaced with the target ip address associated with the domain.

- Version Query :

```sh
dawnl3ss@htb[/htb]$ dig CH TXT version.bind IP_ADDR
```

The '`IP_ADDR`' should be replaced with the target ip address associated with the domain.

- ANY Query :

```sh
dawnl3ss@htb[/htb]$ dig any domain.com @IP_ADDR
```

The '`domain.com`' should be replaced with the domain that we want to footprint.

The '`IP_ADDR`' should be replaced with the target ip address associated with the domain.

- AXFR Query :

```sh
dawnl3ss@htb[/htb]$ dig axfr domain.com @IP_ADDR
```

The '`domain.com`' should be replaced with the domain that we want to footprint.

The '`IP_ADDR`' should be replaced with the target ip address associated with the domain.

- AXFR Query - internal :

```sh
dawnl3ss@htb[/htb]$ dig axfr internal.domain.com @IP_ADDR
```

The '`domain.com`' should be replaced with the domain that we want to footprint.

The '`IP_ADDR`' should be replaced with the target ip address associated with the domain.

###### DNS Enum :

DNS Enum is a tool that can be basically used to do all of that automatically. It also provides a subdomain bruteforcing side that is really useful.

- Usage :

```sh
dawnl3ss@htb[/htb]$ dnsenum --dnsserver IP_ADDR -enum -p 0 -s 0 -f wordlist.txt domain.com
```

The '`domain.com`' should be replaced with the domain that we want to footprint.

The '`IP_ADDR`' should be replaced with the target ip address associated with the domain.

The '`wordlist.txt`' should be replaced with the path of our bruteforcing wordlist.

#### Conclusion :

DNS can be really important when it comes to information gathering and the recon of domains should not be ignored when doing a pentesting.



07/07/2024,  
Dawnless.

--------------------------------------------
--------------------------------------------