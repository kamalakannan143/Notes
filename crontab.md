Job scheduler in linux/unix

```
Field    Description    Allowed Value
MIN      Minute field    0 to 59
HOUR     Hour field      0 to 23
DOM      Day of Month    1-31
MON      Month field     1-12
DOW      Day Of Week     0-6
CMD      Command         Any command to be executed.
```

#References:
https://www.geeksforgeeks.org/crontab-in-linux-with-examples/
https://www.youtube.com/watch?v=UlVqobmcPuM

Steps:
1) `crontab -e`  will create a schedule table for the scripts 
(or) `cat /etc/crontab`
similar to systemd timers `systemctl list-timers -all`

` MIN HOUR DOM MON DOW CMD ` - refer the expansion above

2) `19 9 10 7 2 /home/kali/somescripts.sh`
Defn: somescripts will executes at 9:19AM 10th july tuesday.

3) `19 9 * * 2 /home/kali/somescripts.sh`
Defn: somescripts will executes at 9:19AM every month tuesday.

4) * * * * * /home/kali
