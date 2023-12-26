 Managing Process:
 * SIGTERM - It will kill the process and it will perform some cleanup tasks before in hand
 * SIGKILL - It will kill the process and it will not perform any cleanup activity.
 * SIGSTOP - Stops/Suspends the processes.

NameSpaces are great for security as it a way of isolating into one processes to another.

To start the service while boot-up the machine.
`Systemctl enable "ServiceName"`

|Debian | RHEL| 
| :---- |-----|
| Debian is a APT management | RHEL is properiatory management|

