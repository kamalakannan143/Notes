#Resource [Internal Pentest AD](https://xedex.gitbook.io/internalpentest/internal-pentest/active-directory)

#ADKeywords -- Active directory, domain controller, AD DS, Group Policies, Schema, Forest, Trees

***The server that runs the active directory services is called as Domain Controller**

* Active Directory used by windows
* Authenticate using kerberos tickets
* Non Windows devices also can authenticate to Active Directory via RADIUS and LDAP.
* Identity management services

Eg: Phonebook

*one user name and passwords you can authenticate into any devices.*

###### Physical components of AD:
**Domain Controllers:**
	A domain controller is a server with the ADDS (Active Directory Domain Services) server role installed that has specifically promoted to a Domain Controller.

* Host a copy of the AD DS directory store
* Provides authentication and authorization services
* Replicate updates to other domain controller in the domain and the forest
* Allow administrative access to manage user accounts and network resources

* Group policies
* ADDS data store (contains the DB files and processes that store and manage directory information for users, services and applications)
	holds the file Ntds.dit #sensitive password hashes, AD data and users info

###### Logical components of AD:
**AD DS schema (blueprint)
* enforces rules regarding object creation
* defines every type of object that can be stored in directory

| Object Type | Function | Examples |
|:----------:      |  :------:     |  -----        | 
| class object | what objects can be created  user and computers |

**Domains:** Manages groups and multiple objects into an single organization.
* Administrative boundary for applying policies to group of objects
* A replication boundary for replicating data between domain controllers
* authentication and authorization boundary provides a way to limit the scope of resources.

**Trees:** Hierarchy of domain in AD DS
Eg: eu.domain.com - child 1 and am.domain.com - child 2

![[Pasted image 20230729153147.png|500]]

**FOREST**
Forest is an connection of multiple trees in a domain.
Forest can make replica of one item, so that they can be able to update to the item in domain controller.

![[Pasted image 20230729153230.png|600]]

* contain the link of one business tree to another
* Enable trusts between all domains in the forest

**Organizational Units:** OU's
Active directory containers that contains user, groups, computers and other OU's
* Manage a collection of object in a consistent way.
* Apply policies
* delegate permissions to administer group of objects

**Trusts:**
- Provides users to gain and access the resources in another domain.

![[Pasted image 20230729153726.png|500]]

**Objects:**

![[Pasted image 20230729153910.png|500]]


##### LAB Setup Build
Key Tips:

while creating a domain controller give the domain name as "somedomain.local" or "somedomain.com" or "somedomain.ru"

###### Setting up users, group and policies:
Server Manager -> Tools -> Active Directory users and computers -> 

###### Setting up a file share:
File and storage services -> Shares -> Tasks -> New Share -> SMB Share Quick -> Create the folder in directory.  

**SPN - service principal name**
	unique identifier of a service instance
	Kerberos authentication uses SPN's to associate a service instance with a service sign-in account.

After creating a SQLservice account in the Active directory users and computer, he did this step.

![[Pasted image 20230729210629.png]]
#Resource [Service Principal Name](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-adts/cd328386-4d97-4666-be33-056545c1cad2)

	For example, "ldap/dc-01.fabrikam.com/fabrikam.com" is a three-part SPN where "ldap" is the service class name, "dc-01.fabrikam.com" is the host name, and "fabrikam.com" is the service name.

#Pending Group Policy Management:


### Types of Objects in active directory:

1) **Users:**
Users are one of the most common object types of active directory.
Users can gain authentication for the privilege resources like printers, files.
Users can be represented as two entities:
	**people:** access to the network to employee
	**services:** service user can run only with the privleges requires for the specified service like IIS or MSSQL
2) **Machines:**
		for every computers that joins AD, a machines would be created. it also considered as a security principals

OU vs Security Groups:
	OU's for applying policies - includes specific configurations  for users on their particular role in their enterprise.
	security groups: Grant permissions over the resources. An user can be part of many group which is needed to grant access to multiple resources.

# THM:

#### ADBasics:

resetting the password using powershell
```powershell
Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose
```

Force reset the password at next logon:

```powershell
Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose
```
connect to RDP
`xfreerdp /v:10.10.88.126 /u:'THM\sophie' /p:DonutMan@123 /dynamic-resolution
`