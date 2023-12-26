
```Bash
#!/bin/bash
for ip in `seq 1 255`; do
ping -c 1 $1.$ip | grep "64 bytes" | cut -d " " -f 4 | tr -d ":" &
done
```

$1 represents the input get from user in first field.

`&` - represents threading and be fastest. all execution at single time.
`;` - represent one time execution. one loop completes then only other loop will start.
`./filename 127.0.0.1` 

Result:

```bash
PING 127.0.0.1 (127.0.0.1) 56(84) bytes of data.
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.038 ms

--- 127.0.0.1 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.038/0.038/0.038/0.000 ms
```


Statements:
if, then, for, do, else, done, fi

`initial` -> for, `execute`-> do, `completed` done

```bash
if [$1 == ""];
then 
echo 'Syntax error: give the identifier'
echo 'Give the parameter after the script'
else 
for i in `seq 1 244`; do
ping -c 3 127.0.0.1

```


```bash
for ip in $(cat ip.txt); do nmap $ip; done
```



Own scripts:
How to extract a words from paragraph to form a word list in linux ?
`echo "YOUR PARAGRAPH HERE" | tr -s '[:punct:][:space:]' '\n' | grep -Eo '[[:alpha:]]+' | sort -u > wordlist.txt `

How to remove 2 or 3 words in a document and filter out to new word list ?
`grep -vE '^[a-zA-Z0-9]{2,4}$' 100k-most-used-passwords-NCSC.txt | tee Filtered_wordlist`
