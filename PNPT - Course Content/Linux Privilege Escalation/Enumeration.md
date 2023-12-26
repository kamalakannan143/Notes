##### System Enumeration:

![[Recording 20230806182510.webm]]

Try to low down the presence while giving the commands through terminal with low count of commands.
**understanding** and working on it as a good way of low down commands entered.
if a command is not required there, then why you have to give here. its unnecessary right ?

 *Try to reduce the unnecessary actions while performing any assessment*
 
![[Pasted image 20230806180241.png]]
##### Initial steps: 
Why we have to do this?
	here we can find the data of kersion version hostname and distribution info also. 
`uname -a `
`cat /proc/version`  - #UtilizeThis - everything about sys info from user, hostname upto dist
`cat /etc/issue` - distribution type
`lscpu` - system CPU information 
![[Pasted image 20230806181524.png|500]]

`ps aux`  - Running services on the linux machine. what user running what task or command

##### User Enumeration:
`whoami`
`id`
`sudo -l` -- lists which user having root privileges to run a command. 
`cat /etc/passwd`
`history` - some juicy info about history is if you give space and then write the command it won't save the command in history --- verified with my machine


##### Network Enumeration:
`ip a`
`ip route`
`ip neigh` -  stale and reachable ip's
`netstat -ano`  which ports are talking to which destination. 
##### Password Hunting:

```shell
	grep --color=auto -rnw '/' -ie "PASSWORD"  --color=always 2> /dev/null
```
	it will highlight the color of password text mentioned in the docs or dirs.

keywords - think out of the box
`pwd`
`passwd`
`password`
`pass`


##### Automated Tools:
#Tools 
1) `LinPEAS` - Linux privilege escalation awesome scripts
2) Run any other tools, [LinEnum](https://github.com/rebootuser/LinEnum)
3) [LinuxExploitSuggester](https://github.com/mzet-/linux-exploit-suggester)
4) [LinuxPrivchecker](https://github.com/sleventyeleven/linuxprivchecker)

**LinPEAS**
![[Pasted image 20230807044906.png]]

* check whether any scheduled jobs are running here or not like cronjobs.
* last written file in linux
* 