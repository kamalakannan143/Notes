Abuse those features of windows not misconfigurations
#ADKeywords  SLAAC(Stateless Address Auto Configuration), LLMNR
##### Introduction:
#References  [Medium](https://medium.com/@adam.toscher/top-five-ways-i-got-domain-admin-on-your-internal-network-before-lunch-2018-edition-82259ab73aaa)

##### LLMNR Poisoning: 
LLMNR - Link Local Multicast and Name Resolution - 
* basically DNS
* previously called the name as NBT-NS (net bios name service)
* DNS packet format for IPv4 and IPv6 to perform name resolution for hosts and services on the same link.

`Flaw - when we repond to LLMNR it will respond back us with username and password hash`

	Actual DNS name: \\senorita
	Wrong DNS name: \\senoriT

Eg: If a victim is looking for an wrong DNS name, server could not understand because the DNS was not there. Then, the victim will send a broadcast to everyone in the network. Here, what attacker comes into picture. he will respond to the victim that he knows the DNS name and he will ask the victim to share the user name and password hash.

This LLMNR poisoning part covers similar to MITM attack.

#Tools: repsonder
`python responder.py -l tun0 -rdw`

Run the tool and wait for the response from any of the machines which is looking for wrong dns.

Once you got the hash, try to crack it using hashcat (moreover not possible in many assessments to crack the hash)

##### LLMNR Poisoning Defense:

* Disable LLMNR and NBT-NS
	 if DNS fails packet will goes to LLMNR, if LLMNR fails it will go to NBT-NS while doing the broadcast.	 
	 
![[Pasted image 20230730190207.png|500]]

##### SMB Relay Attack: 
Instead of cracking hashing, we can relay the password hashes to gain access to another machines.

Possible to do SMB Relay:
* Target should have any **SMB signing enabled but not required** (packet level protocol) in their machine.
	If the SMB  signing is enabled, it will find out the relay packets are not signed by the victim and it was sent by the attacker.
* Relayed user creds must be **Admin** on the machine - then only it can dumps the SAM hashes of local users and admin.

###### Scenario:
Step 1:
**Changing the configuration in responder:**

![[Pasted image 20230730191245.png|400]]

Step 2:
`python ntlmrelayx.py -tf targets.txt smb2support`
	It will send the SMB relay to targets hosts and fetch the SAM hashes of the machine.

Step 3: 
`python ntlmrelayx.py -tf targets.txt smb2support -i`
	i - Interactive SMB shell
	c - run specific commands -c "whoami"
	-e - executes file, we can generates the .exe from msfvenom and use the file here to get the meterpreter session.

###### How to find out SMB signing Disabled ?
* Through Nessus scan it will show up SMB Disabled.
* #tools Github - [SMB Signing Checks](https://github.com/actuated/check-smb-signing/blob/master/check-smb-signing.sh) scripts would be available, you can make use of that.
* Nmap
	`nmap --script=smb2-security-mode.nse -p 445 *192.179.23.0/24*`
		Result: -> If the SMB signing was disabled. Target hosts (192.168.57.141 - 142)
		
![[Pasted image 20230731060838.png]]  ![[Pasted image 20230731061020.png|350]]

![[Pasted image 20230811213927.png]]
##### SMB Relay Mitigation - Defense :
* Enabling SMB signing in every machines
**Pros:**  can completely stops the SMB relay devices
**Cons:** can cause performance issues with file copies -> File sharing speed issues

* Disable NTLM authentication on network
**Pros:** Stops the attack
	Its better use the kerberos authentication.
**Cons:** If kerberos auth stops working, windows default back to NTLM anyways.

* Account Tiering
**Pros:** Giving account restriction would stops the attacks. Like Domain Admin should not be log on to user accounts and whatever the DA needs permission to connect to DC that should be configured in the policy.
**Cons:** Enforcing the policy is difficult.

* Local Admin Restriction
**Pros:** Can prevent lot of lateral movement
**Cons:** If any failures occurs on the employee machine. It may requires of service desk tickets for the resolution. potentially it could increase the count of tickets.

##### Gaining Shell via PSexec:
#tips In meterpreter you don't have to give lhost as ip. you can give lhost = wlan0 (or) eth0

`psexec.py marvel.local/fcastle:Password1@192.168.23.23` = SUCESS

`smbexec.py marvel.local/fcastle:Password1@192.168.23.23` = FAIL

`wmiexec.py marvel.local/fcastle:Password1@192.168.23.23` = FAIL

##### IPV6 Attacks

we can authenticate to the DC via LDAP or SMB

If we reboot a machine, that will trigger an event to the DNS. We can use the same machine to login to the DC. It doesn't requires admin.
Whoever login to the victim machine it will comes it as NTLM 

#Tools: [MITM6](https://github.com/dirkjanm/mitm6)
#References https://www.blackhillsinfosec.com/mitm6-strikes-again-the-dark-side-of-ipv6/
https://blog.fox-it.com/2018/01/11/mitm6-compromising-ipv4-networks-via-ipv6/
https://medium.com/@browninfosecguy/ipv6-exploitation-in-ad-environment-b22a7c3ec8af

	WPAD configuration - Web proxy auto discovery // windows machines send out request and looking for any proxy server in the network. When an attacker which acts as a IPV6 DNS server get this request. 

Step 1:
`mitm6 -d marvel.local`

//generated fakepad.marvel.local so will use this in the next step

spawning up the relay 
Step 2:
			bottom->	domain controller IP in LDAP	
`ntlmrelayx.py -6 -t ldaps://192.178.12.23  -wh faekpad.marver.local -l lootme`
`-l` - will create a foot under the name of lootme which contains whole data of DC
`--delegate-access` It will create a another computer.

After restarting the windows machine. it looks for the DNS

## DO LABS WHATEVER LEARNED IN AD
