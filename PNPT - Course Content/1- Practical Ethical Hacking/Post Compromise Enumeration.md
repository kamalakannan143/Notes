#Tools Bloodhound, Plumhound, LDAP domain dump, Ping castle, Powerview

##### Passback Accounts
#Incident: organization haven't any traditional methods like responder or any other attacks like pass the hash.
but they do have one file shares and printer password exposed as a LDAP connection.


LDAP Domain Dump:
`sudo ldapdomaindump ldaps://192.168.22.2` -u 'MARVEL\fcastle' -p Password1

you will get all the domain detilas in a directory as shown in the IPV6 attacks. I think it was similar to ntlmrelay attack

Bloodhound:
`sudo bloodhound-python -d MARVEL.local -u fcastle -p Password1 -ns 192.168.138.136 -c all

upload-data 

Plumhound :
bloodhound should needs to be up and running.
`sudo git clone path/plumhound.git`
it is for purple teaming people.

PingCastle:
if you are admin, you can run it as a administrator.
