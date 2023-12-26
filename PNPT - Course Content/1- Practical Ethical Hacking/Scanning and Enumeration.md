`arp-scan` - scan the hosts connected to the n/w (wifi or LAN)
`netdiscover -r 192.179.23.0/24` - network scanning app

##### Nmap - Network Mapper
Stealth scan should be undetectable, but now in modern tech they can find out the nmap scan and signature.

sS - Send the captures -> SYN -> SYN/ACK -> RST
at final connection was getting reset, so it doesn't make any open connection b/w the client and the server.

`nmap -T4 -p- -A *target*`
-T4 - speed for the nmap as well as the coverage it tooks.
-A includes traceroute, service version, os fingerprinting


If a client is hosting a default web page.
1) first thing is to understand about other directories of the web page.

`nikto` - web vulnerability scanner

If an website is enabled `TRACE` they might vulnerable to XSS which reflectes to [[XST - cross site tracing]]

###### Directory Enumeration
`dirb`
`dirbuster`
`gobuster`

file extenstion: php,txt,rar,pdf,docx,zip


###### SMB - file share protocol

Metasploit Framework

Exploits - running the malicious code into a vulnerable component
auxiliary - scanning the ports, enumeration, info gathering
post - post exploitation


`smbclient -L \\\\$ip\\`
`smbclent -L \\$ip`  - if you putting 2 slashes, you don't have put any slashes at the end, its just a character spacing

If does smb accepts anonymous login we can login to admin directory too.

`smbclient \\$ip\ADMIN$`

###### SSH
![[Pasted image 20230703055609.png]]
`ssh $ip -oKeyAlgorithm=+diffie-hellman-group1-sha1 -c aes128-cbc`

-> to check the **banner** of the ssh, sometimes it reveals the ssh version, who is the author and which admin have the access privileges too. it is also one way of enumeration.

`ssh user@ip`

`searchsploit`
`exploit-db`



##### Vulnerability Scanning with Nessus

![[Pasted image 20230703061744.png]]