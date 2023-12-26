##### IP Address - LAYER 3

```bash
ip a
```
ipv4 config address -  Decimal notation  2^32
ipv6 address - hexa decimal notation      2^128

	128		64		32		16		8		4		2		1			=> 255
		0		0		0		0		0		0		0		0

NAT - network Address Translation 
Eg: computer devices , smart TVs, mobile devices 
Sign the private ip addresses


##### Classes
Class A - 10.0.0.0 - Big Organization network
Class B - 172.16. - 172.31. - college network devices
Class C - 192.168. - 192.168.255.255 - Physical devices IP address for home networks

IP address are layer 3 protocols - 
Layer 3 protocols are Routers

##### MAC Address - LAYER 2

Address Name for the physical devices

6 diff pair of two 

==00:0C:29==:0a:42:05 - 1st three address is identifier to identify which vendor has been used for the mac address.


##### Transport Layer - LAYER 4

#TCP - Transmission Control Protocol
#UDP - User Datagram Protocol

###### TCP 
Connection oriented protocol
Breaks data into small packets and ensure whether the packets has been sent or not.

###### UDP 
Connectionless protocol
Streaming Media
Online gaming
DNS - Domain Name System
VOIP - Voice over IP

Three way handshake
Syn - synchronize
Syn/Ack - 
Ack


Common ports and protocols
TCP                                     UDP		
FTP (21)                              DNS(53)
SSH (22)                             
HTTPS (443)


##### OSI Model - Open System Interconnection 
1) P - Physical layer - physical devices like data cables
2) D - Data link layer - Switching, Mac Address
3) N - Network layer - Routing, Address
4) T - Transport layer - TCP/UDP
5) S - Session layer - Session Management
6) P - Presentation layer - WMV, MOV, JPEG
7) A - Application layer - HTTP, SMTP

