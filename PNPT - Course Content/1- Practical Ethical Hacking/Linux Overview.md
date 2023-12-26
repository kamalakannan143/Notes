##### User Privileges:

d - directory
r - read 
w - write
x - execute

drwxr-xr-x  2 kali kali      4096 Sep 19  2021  ONEPLUS
-rw-r--r--  1 kali kali  12920023 Jan  5  2021 'oneplus wifi data.txt'
-rw-r--r--  1 kali kali      1801 Apr  7 20:05  owasp_zap_root_ca.cer
drwxr-xr-x  8 kali kali     20480 Jun 25 14:46  Pictures

==drwx==r-xr-x  2 ==kali kali==    - which mentions the owner of the directory and his privileges for RWX
drwx==r-x==r-x  2 - which means the group's permission.
drwxr-x==r-x==  2 - which means permissions for other users.

``adduser #username``

![[Pasted image 20230808114951.png|500]]
##### Hard Links & Soft Links:
drwxr-xr-x  ==2== kali kali - indicates the number of hardlinks to the file.

Normally Links is a pointer to a file which refers to something.
#symboliclinks or #softlinks  - works like a create shortcut in windows
`ln -s [orgi filename] [link name]`

Eg: ==lrwx==rwxrwx 1 kali kali   12 Jun 27 10:13 newnet.txt -> noteword.txt


#hardlinks - just like copy &  paste the original file by renaming it.
`ln [orgi filename ] [link name]`
Also while creating hardlink, date modified also getting same from the original file
But it in another case of cp a original file. it will create another file with date and time modified.

#systrace - showing the system calls taken for the command and execution.


Three most important files:
/etc/shadow - which contains the password hashes
/etc/passwd - shows what are the services and users are in the machine
/etc/sudoers - contains who all having access to the sudo 


`grep 'sudo' /etc/group`

##### Starting & Stopping Services
`sudo service apache2 start`
`sudo systemctl enable ssh`
