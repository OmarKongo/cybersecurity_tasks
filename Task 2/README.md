# Scanning

### TT2.1 Host Discovery

After performing an ARP scan we can interpret that Google Public DNS is UP :

```bash
┌──(kali㉿kongo)-[~]
└─$ nmap -sn -PR 8.8.8.8         
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-21 21:21 EET
Nmap scan report for dns.google (8.8.8.8)
Host is up (0.057s latency).
Nmap done: 1 IP address (1 host up) scanned in 0.14 seconds
```




We can use this command while troubleshooting our devices :

```bash
┌──(kali㉿kongo)-[~]
└─$ nmap -sn -PU 127.0.0.1 
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-21 21:24 EET
Nmap scan report for localhost (127.0.0.1)
Host is up.
Nmap done: 1 IP address (1 host up) scanned in 0.00 seconds
```



Pinging the offical site for Nmap & it is up and running :

```bash
┌──(kali㉿kongo)-[~]
└─$ nmap -sn -PE 45.33.32.156
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-21 21:27 EET
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.31s latency).
Nmap done: 1 IP address (1 host up) scanned in 0.54 seconds
```



This command will ping my whole network and responds back with the Up devices 

```bash
┌──(kali㉿kongo)-[~]
└─$ nmap -sn -PE 192.168.1.2-254
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-21 22:09 EET
Nmap scan report for 192.168.1.3 (192.168.1.3)
Host is up (0.10s latency).
MAC Address: BC:7A:BF:3F:F2:3E (Samsung Electronics)
Nmap scan report for 192.168.1.4 (192.168.1.4)
Host is up (0.10s latency).
MAC Address: 72:0D:7D:31:1C:A7 (Unknown)
Nmap scan report for 192.168.1.6
Host is up (0.0092s latency).
MAC Address: 1A:97:9E:58:76:BA (Unknown)
Nmap scan report for 192.168.1.8
Host is up (0.00023s latency).
MAC Address: F0:57:A6:04:8E:09 (Intel Corporate)
Nmap scan report for 192.168.1.21 (192.168.1.21)
Host is up (0.065s latency).
MAC Address: D4:86:60:BD:FC:FC (Arcadyan)
Nmap scan report for 192.168.1.144 (192.168.1.144)
Host is up (1.3s latency).
MAC Address: 9A:C7:C1:16:21:33 (Unknown)
Nmap scan report for 192.168.1.160
Host is up.
MAC Address: 48:68:4A:19:94:DE (Intel Corporate)
Nmap scan report for 192.168.1.11 (192.168.1.11)
Host is up.
Nmap done: 253 IP addresses (8 hosts up) scanned in 30.58 seconds
```


```bash
┌──(kali㉿kongo)-[~]
└─$ nmap -sn -PP 192.168.1.2-254
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-21 22:02 EET
Nmap scan report for 192.168.1.3 (192.168.1.3)
Host is up (0.096s latency).
MAC Address: BC:7A:BF:3F:F2:3E (Samsung Electronics)
Nmap scan report for 192.168.1.4 (192.168.1.4)
Host is up (0.100s latency).
MAC Address: 72:0D:7D:31:1C:A7 (Unknown)
Nmap scan report for 192.168.1.6
Host is up (0.11s latency).
MAC Address: 1A:97:9E:58:76:BA (Unknown)
Nmap scan report for 192.168.1.8
Host is up (0.00024s latency).
MAC Address: F0:57:A6:04:8E:09 (Intel Corporate)
Nmap scan report for 192.168.1.21 (192.168.1.21)
Host is up (0.017s latency).
MAC Address: D4:86:60:BD:FC:FC (Arcadyan)
Nmap scan report for 192.168.1.144 (192.168.1.144)
Host is up (0.018s latency).
MAC Address: 9A:C7:C1:16:21:33 (Unknown)
Nmap scan report for 192.168.1.160
Host is up.
MAC Address: 48:68:4A:19:94:DE (Intel Corporate)
Nmap scan report for 192.168.1.11 (192.168.1.11)
Host is up.
Nmap done: 253 IP addresses (8 hosts up) scanned in 5.24 seconds

```



Here i tried to perform an ICMP address Mask Ping Scan to a certain web server which blocks ICMP echo ping

```bash
┌──(kali㉿kongo)-[~]
└─$ nmap -sn -PM 54.203.230.42  
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-21 22:12 EET
Note: Host seems down. If it is really up, but blocking our ping probes, try -Pn
Nmap done: 1 IP address (0 hosts up) scanned in 2.08 seconds
```


Here's a TCP Handshake scan to the same web server

```bash
┌──(kali㉿kongo)-[~]
└─$ nmap -sn -PS 54.203.230.42
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-21 22:15 EET
Nmap scan report for ec2-54-203-230-42.us-west-2.compute.amazonaws.com (54.203.230.42)
Host is up (0.24s latency).
Nmap done: 1 IP address (1 host up) scanned in 0.61 seconds

┌──(kali㉿kongo)-[~]
└─$ nmap -sn -PA 54.203.230.42
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-21 22:18 EET
Nmap scan report for ec2-54-203-230-42.us-west-2.compute.amazonaws.com (54.203.230.42)
Host is up (0.23s latency).
Nmap done: 1 IP address (1 host up) scanned in 0.38 seconds
```

We can interpret from this results that this ip is hosted by AWS

```bash
┌──(kali㉿kongo)-[~]
└─$ nmap -sn -PO 54.203.230.42
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-21 22:19 EET
Note: Host seems down. If it is really up, but blocking our ping probes, try -Pn
Nmap done: 1 IP address (0 hosts up) scanned in 3.09 seconds
```

That's a proof that this server is blocking any ping request



```bash
┌──(kali㉿kongo)-[~]
└─$ ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0c:29:e5:77:7f brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.11/24 brd 192.168.1.255 scope global dynamic noprefixroute eth0
       valid_lft 82852sec preferred_lft 82852sec
    inet6 fe80::8b34:7eb8:7ef3:7693/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```

- IPv4 Address : 192.168.1.11/24 with subnet mask 255.255.255.0

- There are 8 up & running hosts on my network subnet


```bash
┌──(kali㉿kongo)-[~]
└─$ nmap -sn scanme.nmap.org 
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-21 23:24 EET
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.24s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Nmap done: 1 IP address (1 host up) scanned in 0.77 seconds

```

- IPv4 Address : 45.33.32.156


### TT2.2 Port & Service Discovery

```bash
nmap -sT -v 45.33.32.156
```

<img width="961" height="744" alt="Pasted image 20260321230713" src="https://github.com/user-attachments/assets/97d188ab-991f-414a-9973-8756f53743c4" />




```bash
nmap -sS -v 192.168.1.159
```

<img width="671" height="334" alt="Pasted image 20260321231545" src="https://github.com/user-attachments/assets/8a64a17d-d02e-4845-aed4-e9b6702060b0" />
<img width="504" height="420" alt="Pasted image 20260321231647" src="https://github.com/user-attachments/assets/ca1c434c-735f-4088-bfa2-a65ebd9ea73b" />



```bash
nmap -sX -v 192.168.1.159
```

<img width="656" height="343" alt="Pasted image 20260321231934" src="https://github.com/user-attachments/assets/7693d8c1-7c65-4baa-bac7-3253e42a4038" />



```bash
nmap -sT -v scanme.nmap.org
```
<img width="747" height="776" alt="Pasted image 20260321232134" src="https://github.com/user-attachments/assets/ebaaf4ce-2de5-492a-ab4e-724969ec5576" />
<img width="452" height="422" alt="Pasted image 20260321232159" src="https://github.com/user-attachments/assets/1816833d-3bda-4fb9-aeca-6c2709979aa2" />


Total 1000 ports are scanned
- 13 ports are open
- 1 port is filtered
- rest of the ports are closed


### TT2.3 OS Discovery

After scanning the whole network subnet *192.168.1.0/24* i got a huge overview about the Up and down hosts, also more info about those Up and running devices one of them was 192.168.1.144 which we will focus on it

<img width="366" height="330" alt="Pasted image 20260321234230" src="https://github.com/user-attachments/assets/05de4000-58b1-4931-93dd-1fc9dc9ea7da" />


```
Nmap scan report for 192.168.1.144
Host is up (0.019s latency).
Not shown: 998 closed tcp ports (reset)
PORT      STATE SERVICE    VERSION
49152/tcp open  tcpwrapped
62078/tcp open  tcpwrapped
MAC Address: 9A:C7:C1:16:21:33 (Unknown)
Device type: phone
Running: Apple iOS 15.X
OS CPE: cpe:/o:apple:iphone_os:15
OS details: Apple iOS 15.0 - 15.6 (Darwin 21.1.0 - 21.6.0)
Uptime guess: 0.001 days (since Sat Mar 21 23:36:27 2026)
Network Distance: 1 hop
TCP Sequence Prediction: Difficulty=257 (Good luck!)
IP ID Sequence Generation: All zeros

TRACEROUTE
HOP RTT      ADDRESS
1   19.20 ms 192.168.1.144
```
<img width="471" height="93" alt="Pasted image 20260321234527" src="https://github.com/user-attachments/assets/1f32ac62-8729-4bfb-a39e-e3c115db76ea" />


