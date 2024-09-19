--------------------------------------------
--------------------------------------------
### SMTP Recon cheat sheet

--------------------------------------------
--------------------------------------------

*Tools used :*         nmap, telnet.  
*Goal* :                  Know how to collect information about SMTP server.  

SMTP is a protocol for sending emails in an IP network. It can be used between an email client and an outgoing mail server or between two SMTP servers. SMTP is often combined with the IMAP or POP3 protocols, which can fetch emails and send emails. In principle, it is a client-server-based protocol, although SMTP can be used between a client and a server and between two SMTP servers. In this case, a server effectively acts as a client.

| Client (`MUA`) | <br>`➞` | Submission Agent (`MSA`) | <br>`➞` | Open Relay (`MTA`) | <br>`➞` | Mail Delivery Agent | <br>`➞` | Mailbox (`POP3`/`IMAP`) |
| -------------- | ------- | ------------------------ | ------- | ------------------ | ------- | ------------------- | ------- | ----------------------- |

##### Identifying SMTP :

SMTP servers usually run under port `25` but newer versions can be running under `587`.