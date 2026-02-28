# Reconnaissance & Footprinting

## Target : https://hackthissite.org/

### TT1.1 Google Dorking | Passive Reconn

Search Query : 

```
intitle:login site:https://hackthissite.org/
```

<img width="1658" height="700" alt="Pasted image 20260226155342" src="https://github.com/user-attachments/assets/e864bbc2-82cd-43f6-a24e-5bedb9f78762" />


##### More operators in advanced search engines


| Command     | Function                                                                     |
| ----------- | ---------------------------------------------------------------------------- |
| cache       | Displays cached versions of web pages.                                       |
| allinurl    | Finds pages with multiple keywords in the URL.                               |
| inurl       | Searches for specific text within URLs.                                      |
| inanchor    | Searches for keywords within the anchor text of links on a webpage.          |
| allinanchor | Find pages with multiple keywords within the text of links pointing to them. |
| link        | Find web pages linking to a specific URL.                                    |
| related     | Displays pages related to a spcific URL.                                     |
| info        | Provides details about a website including cache and similar pages           |
| location    | It helps narrow down results to a specific area for better local relevance.  |


### TT1.2 Footprinting | Passive Reconn

#### Info gathered from **netcraft** 

- Top Level Domain : Organization Entities (.org)
- Hosting company : OVH Cloud (hosted on a dedicated server)
- Hosting country : NL
- Domain : hackthissite.org
- IPv4 address : 137.74.187.100
- Nameserver : c.ns.buddyns.com

Domain's Network : 137.74.0.0/16
##### Netblock
	IPv4 Address (137.74.187.100)

| IP range start            | End             | Country | Description   |
| ------------------------- | --------------- | ------- | ------------- |
| ::ffff.0.0.0/96           |                 | US      | IANA          |
| -->137.0.0.0              | 137.255.255.255 | US      | ARIN          |
| --->137.74.0.0            | 137.74.255.255  | FR      | OVH SAS       |
| ------>137.74.187.96      | 137.74.187.127  | NL      | OVH Static IP |
| ---------->137.74.187.100 |                 | NL      | OVH Static IP |

##### Subdomains

| Host                         | OS      | IPv4 Address   |
| ---------------------------- | ------- | -------------- |
| www.hackthissite.org         | FreeBSD | 137.74.187.103 |
| legal.hackthissite.org       | FreeBSD | 137.74.187.183 |
| mirror.hackthissite.org      | FreeBSD | 137.74.187.134 |
| www.irc.hackthissite.org<br> | FreeBSD | 137.74.187.153 |

*FreeBSD* : is a powerful, open-source Unix like operating system derived from **BSD**, designed for stability, performance, and advanced networking. Used to **power modern servers**, **desktops**, and **embedded platforms**.

More Info about FreeBSD
	Difference from Linux : While sharing a Unix-like experience, **FreeBSD** is not **Linux**. It doesn't use **systemd**, instead relying on **rc** scripts for system initialization. It also offers binary compatibility with Linux, allowing many Linux programs to run directly, but it is not built on the Linux kernel.

#### Info gathered from **DNSDumpster** 


<img width="1776" height="511" alt="Pasted image 20260226171602" src="https://github.com/user-attachments/assets/86c79502-8993-430e-826a-95103e2d8b5d" />



##### Tree Map of the Domain that includes DNS Servers & MX (Mail-exchange) Servers


<img width="3270" height="765" alt="Pasted image 20260226175505" src="https://github.com/user-attachments/assets/fcde4bf9-e167-4328-afd8-a86c8804a9a1" />



There are 3 DNS Servers for the target
- f.ns.buddyns.com (5.223.55.119)
- c.ns.buddyns.com (116.203.6.3)
- j.ns.buddyns.com (37.143.161.179)




##### A records (Subdomains from dataset)

| Host                       | Reverse DNS                                                  | IP              | Netblock Owner                                                       |
| -------------------------- | ------------------------------------------------------------ | --------------- | -------------------------------------------------------------------- |
| api.hackthissite.org       | api.hackthissite.org                                         | 137.74.187.115  | OVH, FR<br>16276 / France                                            |
| ctf.hackthissite.org       |                                                              | 185.199.108.153 | FASTLY - Fastly, Inc.<br>54113 / United States                       |
| email.hackthissite.org     | k8s-svc-lander-namecheap-<br>expired-01.us-ord.parklogic.net | 172.239.57.117  | AKAMAI-LINODE-AP Akamai Connected Cloud, SG<br>63949 / United States |
| forums.hackthissite.org    | hackthissite.org                                             | 137.74.187.100  | OVH, FR<br>16276 / France                                            |
| git.hackthissite.org       |                                                              | 137.74.187.145  | OVH, FR<br>16276 / France                                            |
| h5ai.hackthissite.org      | cdn-185-199-111-153.github.com                               | 185.199.111.153 | FASTLY - Fastly, Inc.<br>54113 / United States                       |
| hp.hackthissite.org        | hackthissite.org                                             | 137.74.187.100  | OVH, FR<br>16276 / France                                            |
| irc.hackthissite.org       | wolf.irc.hackthissite.org                                    | 185.24.222.13   | TILAA, NL<br>196752 / Netherlands                                    |
| irc-hub.hackthissite.org   | customer.sharktech.net                                       | 198.148.81.169  | SHARKTECH - Sharktech<br>46844 / United States                       |
| irc-www.hackthissite.org   | www.irc.hackthissite.org                                     | 137.74.187.153  | OVH, FR<br>16276 / France                                            |
| lille.irc.hackthissite.org |                                                              | 137.74.187.151  | OVH, FR<br>16276 / France                                            |
| wolf.irc.hackthissite.org  | wolf.irc.hackthissite.org                                    | 185.24.222.13   | TILAA, NL<br>196752 / Netherlands                                    |
| www.irc.hackthissite.org   | www.irc.hackthissite.org                                     | 137.74.187.153  | OVH, FR<br>16276 / France                                            |
| legal.hackthissite.org     | legal.hackthissite.org                                       | 137.74.187.138  | OVH, FR<br>16276 / France                                            |
| mirror.hackthissite.org    | mirror.hackthissite.org                                      | 137.74.187.134  | OVH, FR<br>16276 / France                                            |
| psrp.hackthissite.org      | k8s-svc-lander-namecheap-<br>expired-01.us-ord.parklogic.net | 172.239.57.117  | AKAMAI-LINODE-AP Akamai Connected Cloud, SG<br>63949 / United States |
| qdb.hackthissite.org       | www.irc.hackthissite.org                                     | 137.74.187.153  | OVH, FR<br>16276 / France                                            |
| stats.hackthissite.org     | stats.hackthissite.org                                       | 137.74.187.136  | OVH, FR<br>16276 / France                                            |
| status.hackthissite.org    |                                                              | 89.106.200.1    | ENFLOW, NL<br>209626 / Netherlands                                   |
| www.hackthissite.org       | hackthissite.org                                             | 137.74.187.100  | OVH, FR<br>16276 / France                                            |


### TT1.3 Social Media & Professional Networking Footprinting | Passive Reconn

#### Results from sherlock tool

Focusing here on username **Minar El-Aasser**  ONLY:

```bash
aei@ip-172-26-4-45:~$ sudo docker run -it --rm sherlock/sherlock "Minar El-Aasser" -v
[sudo] password for aei:
[*] Checking username Minar El-Aasser on:

[+] [180ms] AniWorld: https://aniworld.to/user/profil/Minar%20El-Aasser
[+] [855ms] BoardGameGeek: https://boardgamegeek.com/user/Minar%20El-Aasser
[+] [1501ms] Discord: https://discord.com
[+] [2607ms] Hive Blog: https://hive.blog/@Minar%20El-Aasser
[+] [4276ms] Odysee: https://odysee.com/@Minar%20El-Aasser
[+] [8547ms] minds: https://www.minds.com/Minar%20El-Aasser/
[+] [8867ms] omg.lol: https://Minar%20El-Aasser.omg.lol

[*] Search completed with 7 results
```




The results from this username were false positive. so i had to try other usernames

```bash
aei@ip-172-26-4-45:~$ sudo docker run -it --rm sherlock/sherlock  minar-el-asser Minar_El-Asser minar.elaasser minar_elaasser Minar-El-Aasser minar.el.aasser -v
[*] Checking username minar-el-asser on:

[+] [190ms] AniWorld: https://aniworld.to/user/profil/minar-el-asser
[+] [711ms] BoardGameGeek: https://boardgamegeek.com/user/minar-el-asser
[+] [1825ms] Discord: https://discord.com
[+] [14733ms] hackster: https://www.hackster.io/minar-el-aasser

[*] Checking username Minar_El-Asser on:

[+] [172ms] AniWorld: https://aniworld.to/user/profil/Minar_El-Asser
[+] [445ms] BoardGameGeek: https://boardgamegeek.com/user/Minar_El-Asser
[+] [1575ms] Discord: https://discord.com
[+] [7440ms] omg.lol: https://Minar_El-Asser.omg.lol

[*] Checking username minar.elaasser on:

[+] [156ms] AniWorld: https://aniworld.to/user/profil/minar.elaasser
[+] [429ms] BoardGameGeek: https://boardgamegeek.com/user/minar.elaasser
[+] [1056ms] Cracked Forum: https://cracked.sh/minar.elaasser
[+] [1325ms] Cults3D: https://cults3d.com/en/users/minar.elaasser/creations
[+] [2550ms] Medium: https://medium.com/@minar.elaasser
[+] [4565ms] Snapchat: https://www.snapchat.com/add/minar.elaasser
[+] [5662ms] Wikipedia: https://en.wikipedia.org/wiki/Special:CentralAuth/minar.elaasser?uselang=qqx
[+] [6746ms] minds: https://www.minds.com/minar.elaasser/
[+] [6840ms] omg.lol: https://minar.elaasser.omg.lol

[*] Checking username minar_elaasser on:

[+] [169ms] AniWorld: https://aniworld.to/user/profil/minar_elaasser
[+] [49628ms] ReverbNation: https://www.reverbnation.com/minar_elaasser
[+] [7606ms] omg.lol: https://minar_elaasser.omg.lol

[*] Checking username Minar-El-Aasser on:

[+] [136ms] AniWorld: https://aniworld.to/user/profil/Minar-El-Aasser
[+] [502ms] BoardGameGeek: https://boardgamegeek.com/user/Minar-El-Aasser
[+] [1404ms] Discord: https://discord.com
[+] [49538ms] ReverbNation: https://www.reverbnation.com/Minar-El-Aasser
[+] [7021ms] hackster: https://www.hackster.io/Minar-El-Aasser

[*] Checking username minar.el.aasser on:

[+] [145ms] AniWorld: https://aniworld.to/user/profil/minar.el.aasser
[+] [564ms] Blitz Tactics: https://blitztactics.com/minar.el.aasser
[+] [631ms] BoardGameGeek: https://boardgamegeek.com/user/minar.el.aasser
[+] [1256ms] Cracked Forum: https://cracked.sh/minar.el.aasser
[+] [1551ms] Cults3D: https://cults3d.com/en/users/minar.el.aasser/creations
[+] [5857ms] mastodon.cloud: https://mastodon.cloud/@minar.el.aasser
[+] [6047ms] mastodon.social: https://mastodon.social/@minar.el.aasser
[+] [6351ms] mastodon.xyz: https://mastodon.xyz/@minar.el.aasser
[+] [6375ms] mstdn.social: https://mstdn.social/@minar.el.aasser
[+] [6104ms] mstdn.io: https://mstdn.io/@minar.el.aasser
[+] [6074ms] omg.lol: https://minar.el.aasser.omg.lol
[+] [7034ms] social.tchncs.de: https://social.tchncs.de/@minar.el.aasser

[*] Search completed with 37 results
aei@ip-172-26-4-45:~$ sudo docker run -it --rm sherlock/sherlock  minar-el-aasser Minar_El-Aasser -v
[*] Checking username minar-el-aasser on:

[+] [229ms] AniWorld: https://aniworld.to/user/profil/minar-el-aasser
[+] [641ms] BoardGameGeek: https://boardgamegeek.com/user/minar-el-aasser
[+] [1629ms] Discord: https://discord.com
[+] [7960ms] hackster: https://www.hackster.io/minar-el-aasser

[*] Checking username Minar_El-Aasser on:

[+] [164ms] AniWorld: https://aniworld.to/user/profil/Minar_El-Aasser
[+] [400ms] BoardGameGeek: https://boardgamegeek.com/user/Minar_El-Aasser
[+] [1292ms] Discord: https://discord.com
[+] [7168ms] omg.lol: https://Minar_El-Aasser.omg.lol

[*] Search completed with 8 results

```

From this further Look up, I got 3 real profiles for Dr. Minar the other 42 were false positive
- Medium : https://medium.com/@minar.elaasser
- Snapshat : https://www.snapchat.com/@minar.elaasser (I'm in doubt with this one 😅)
- Hackster : https://www.hackster.io/minar-el-aasser


Searching for these usernames on SlideShare

```bash
aei@ip-172-26-4-45:~$ sudo docker run -it --rm sherlock/sherlock  "Minar El-Aasser" minar-el-asser Minar_El-Asser minar.elaasser minar-el-aasser Minar_El-Aasser -v --site SlideShare
[sudo] password for aei:
[*] Checking username Minar El-Aasser on:

[+] [536ms] SlideShare: https://slideshare.net/Minar%20El-Aasser

[*] Checking username minar-el-asser on:


[*] Checking username Minar_El-Asser on:


[*] Checking username minar.elaasser on:


[*] Checking username minar-el-aasser on:


[*] Checking username Minar_El-Aasser on:


[*] Search completed with 1 results

aei@ip-172-26-4-45:~$ sudo docker run -it --rm sherlock/sherlock  "Minar El-Aasser" minar-el-asser Minar_El-Asser minar.elaasser minar-el-aasser Minar_El-Aasser -v --site SlideShare --dump-response
[*] Checking username Minar El-Aasser on:

+++++++++++++++++++++
TARGET NAME   : SlideShare
USERNAME      : Minar El-Aasser
TARGET URL    : https://slideshare.net/Minar%20El-Aasser
TEST METHOD   : message
Results...
RESPONSE CODE : 404
ERROR TEXT    : <title>Page no longer exists</title>
>>>>> BEGIN RESPONSE TEXT
HTML Response
<<<<< END RESPONSE TEXT
VERDICT       : Available
+++++++++++++++++++++

[*] Search completed with 1 results
```

We got one result but it was false positive



Searching for these usernames on Facebook

```bash
aei@ip-172-26-4-45:~$ sudo docker run -it --rm sherlock/sherlock  "Minar El-Aasser" minar-el-asser Minar_El-Asser minar.elaasser minar-el-aasser Minar_El-Aasser -v --site facebook
Error: Desired sites not found: 'facebook'.
aei@ip-172-26-4-45:~$ sudo docker run -it --rm sherlock/sherlock  "Minar El-Aasser" minar-el-asser Minar_El-Asser minar.elaasser minar-el-aasser Minar_El-Aasser -v --site Facebook
Error: Desired sites not found: 'Facebook'
```

We got an error stating that Facebook doesn't exist in the 400+ social websites.





##### Another practical way to gather info using Google Dorks

I tried another method in order to gather more info about Dr. Minar from Social Media using Google Dorks

Using this search query

```
"Minar El-Aasser" intitle:Minar El-Aasser
```

Actually this way was much more better than using sherlock. Always there is no one path for reaching anything so, i had to try something different other than sherlock & Here's what i found :

| Site              | URL                                                                                             |
| ----------------- | ----------------------------------------------------------------------------------------------- |
| Google Scholar    | https://scholar.google.com/citations?user=Qk6jyhoAAAAJ&hl=en                                    |
| ResearchGate      | https://www.researchgate.net/profile/Minar-El-Aasser                                            |
| LinkedIn          | https://www.linkedin.com/in/minar-el-aasser/                                                    |
| OpenReview        | https://openreview.net/profile?id=~Minar_El-Aasser1                                             |
| Instagram         | https://www.instagram.com/minarelaasser/?hl=en                                                  |
| Facebook          | https://www.facebook.com/minar.elaasser                                                         |
| ACADEMIA          | https://independent.academia.edu/ElAasserMinar                                                  |
| SciProfiles       | https://sciprofiles.com/profile/author/WkpVcGlJSHpwaXozaXo1RU9MUjZ0UT09                         |
| dagstuhl.de       | https://dblp.dagstuhl.de/pid/254/8557.html                                                      |
| RocketReach       | https://rocketreach.co/minar-el-aasser-email_720466024                                          |
| x (twitter)       | https://x.com/minar_elaasser                                                                    |
| Tableau Public    | https://public.tableau.com/app/profile/minar.el.aasser                                          |
| Kaggle            | https://www.kaggle.com/minarelaasser                                                            |
| stackoverflow     | https://stackoverflow.com/users/8255633/minar-el-aasser                                         |
| prezi             | https://prezi.com/user/rtcb7jc_myyx/                                                            |
| adscientificindex | https://adscientificindex.com/scientist/scientist-education-information/minar-el-aasser/5780943 |
| SoundCloud        | https://soundcloud.com/minar-el-aasser                                                          |




### TT1.4 WHOIS & DNS LOOKUP | Passive Reconn

##### Target : https://hackthissite.org/

This target URL created on 2003-08-10
Registrar: Porkbun LLC
Registrar URL: https://porkbun.com

DNS Registrar is a bussiness that handles reservation of domain names as well as the assignment of IP addresses for those domain names. Domain names are alphanumeric aliases used to access websites; for example, Cloudflare's domain name is 'cloudflare.com' and the IP address would be something like 192.0.2.1. Domain names make it easier to access websites without having to memorize and enter alphanumeric IP addresses. 


### TT1.5 Domain Name Services Footprinting | Passive Reconn


```powershell
C:\Users\Omar>nslookup
Default Server:  h188a # Default Server
Address:  fe80::1 # Assigned IPv6 address

> set type=a
> www.hackthissite.org
Server:  h188a
Address:  fe80::1

Non-authoritative answer:
Name:    www.hackthissite.org
Addresses:  137.74.187.101
          137.74.187.102
          137.74.187.103
          137.74.187.104
          137.74.187.100 # Target's Main IP

> set type=cname
> www.hackthissite.org
Server:  h188a
Address:  fe80::1

hackthissite.org
        primary name server = c.ns.buddyns.com # DNS of target URL
        responsible mail addr = admin.hackthissite.org # Mail Server address
        serial  = 2025032501
        refresh = 3600 (1 hour)
        retry   = 900 (15 mins)
        expire  = 1209600 (14 days)
        default TTL = 3600 (1 hour)

> server c.ns.buddyns.com
Default Server:  c.ns.buddyns.com
Addresses:  2a01:4f8:1c0c:8115::3
          116.203.6.3 # Primary Address

```

##### Results from kloth.net

<img width="3730" height="1543" alt="Pasted image 20260228041023" src="https://github.com/user-attachments/assets/021c819d-b577-415e-b55c-268280b39422" />
<img width="3710" height="754" alt="Pasted image 20260228041213" src="https://github.com/user-attachments/assets/e89d9481-1433-4223-a1a8-07372e86965a" />



More options other than A (IPv4) & AAAA (IPv6)

- CNAME (Canonical Name) record is a type of DNS record that maps an alias name to a true canonical domain name. 

- NS (Name Server) record indicates which DNS server is authoritative for that domain. Basically, NS records tell the Internet where to go to find out a domain's IP addresss. 

- MX (Mail Exchange) record directs email to a mail server. The MX record indicates how email messages should be routed in accordance with the SMTP.



### TT1.6 Network Mapping | Active Reconn


```powershell
PS C:\Users\Omar> tracert www.hackthissite.org

Tracing route to www.hackthissite.org [137.74.187.100]
over a maximum of 30 hops:  # Maximum hops : 30 (default)

  1     1 ms    <1 ms     1 ms  h188a [192.168.1.1] # This is my Default Gateway
  2     4 ms     3 ms     3 ms  156.204.0.1 # ISP's first public router
  3     4 ms     3 ms     3 ms  10.35.14.1 [10.35.14.1] # Private IP in ISP network, NAT/router hop
  4     4 ms     3 ms     3 ms  10.35.14.2 [10.35.14.2] # Another internal ISP router
  5    19 ms     4 ms    92 ms  10.45.28.66 [10.45.28.66] # Another internal or transit hop. The 92ms shows variable latency
  6    10 ms     8 ms     7 ms  host-80.81.193.140.tedata.net [80.81.193.140] # First Public IP outside local ISP network
  7    78 ms   102 ms    97 ms  decix2.ovhcloud.com [80.81.193.209] # Interconnection point to OVH network
  8     *        *        *     Request timed out. # Routers may block ICMP or, firewall prevents responses
  9     *        *        *     Request timed out. # Routers may block ICMP or, firewall prevents responses
 10    66 ms    54 ms    98 ms  fra1-lim3-vac-1-firewall.de.eu [178.33.99.161] # Firewall in OVH Germany network
 11    71 ms   100 ms   100 ms  37.59.16.44 # Transit router inside OVH or upstream provider
 12     *        *        *     Request timed out. # Router blocking ICMP replies
 13   130 ms   100 ms   100 ms  be104.lil1-rbx1-sbb1-nc5.fr.eu [178.33.100.158] # Router in France (OVH Datacenter)
 14   131 ms   102 ms   100 ms  37.59.16.20 # Another transit router near the final destination
 15     *        *        *     Request timed out. # Some routers/firewalls not replying to ICMP
 16     *        *        *     Request timed out. # Some routers/firewalls not replying to ICMP
 17     *        *        *     Request timed out. # Some routers/firewalls not replying to ICMP
 18    62 ms    94 ms    98 ms  hackthissite.org [137.74.187.100] # **Destination reached**

Trace complete.
```

Total **18** hops to reach the target

Here're the first 3 hops using -h option

```powershell
PS C:\Users\Omar> tracert /?

Usage: tracert [-d] [-h maximum_hops] [-j host-list] [-w timeout]
               [-R] [-S srcaddr] [-4] [-6] target_name

Options:
    -d                 Do not resolve addresses to hostnames.
    -h maximum_hops    Maximum number of hops to search for target.
    -j host-list       Loose source route along host-list (IPv4-only).
    -w timeout         Wait timeout milliseconds for each reply.
    -R                 Trace round-trip path (IPv6-only).
    -S srcaddr         Source address to use (IPv6-only).
    -4                 Force using IPv4.
    -6                 Force using IPv6.
PS C:\Users\Omar> tracert -h 3 www.hackthissite.org

Tracing route to www.hackthissite.org [137.74.187.100]
over a maximum of 3 hops:

  1    27 ms     1 ms    <1 ms  h188a [192.168.1.1]
  2     4 ms     3 ms     3 ms  156.204.0.1
  3     4 ms     3 ms     3 ms  10.35.14.1 [10.35.14.1]

Trace complete.

```


##### Tracing certifiedhacker.com from Kali Machine

```bash
┌──(kali㉿kongo)-[~]
└─$ traceroute www.certifiedhacker.com
traceroute to www.certifiedhacker.com (162.241.216.11), 30 hops max, 60 byte packets
 1  192.168.1.1 (192.168.1.1)  1.499 ms  1.207 ms  1.309 ms
 2  156.204.0.1 (156.204.0.1)  4.077 ms  4.023 ms  4.318 ms
 3  10.45.10.53 (10.45.10.53)  4.403 ms  5.497 ms  5.440 ms
 4  10.35.14.2 (10.35.14.2)  5.388 ms  5.791 ms  5.697 ms
 5  10.45.28.66 (10.45.28.66)  6.233 ms  6.161 ms  6.466 ms
 6  TELECOM-EGY.edge1.Marseille3.Level3.net (213.19.202.134)  8.067 ms  4.514 ms  5.470 ms
 7  et-4-0-11.edge1.Marseille3.Level3.net (213.19.202.133)  74.435 ms  74.317 ms  74.224 ms
 8  * * ae2.3601.edge2.Phoenix1.net.lumen.tech (4.69.219.218)  195.233 ms
 9  4.18.104.126 (4.18.104.126)  184.238 ms  184.144 ms  184.033 ms
10  140.91.194.247 (140.91.194.247)  184.280 ms 140.91.194.130 (140.91.194.130)  183.853 ms 140.91.195.11 (140.91.195.11)  183.768 ms
11  * * *
12  box5331.bluehost.com (162.241.216.11)  183.659 ms  199.596 ms  199.468 ms

```

##### First Entry breakdown
- The 1st hop indicates my default gateway (Local Router) **192.168.1.1**
- Traceroute sends **3 probes (packets)** to each hop. 
- Each number is the **round-trip time (RTT)** for one packet.
	 Packet 1 → 1.499 ms
	 Packet 2 → 1.207 ms
	 Packet 3 → 1.309 ms

##### Target IP : 162.241.216.11



### TT1.7 Perform Email Footprinting | Passive Reconn


#### Headers from a suspicious email

```
Delivered-To: omarm.shaalan@gmail.com
Received: by 2002:a05:6802:66c6:b0:619:5591:96c1 with SMTP id o6csp409873occ;
        Thu, 26 Feb 2026 07:40:37 -0800 (PST)
X-Received: by 2002:a05:622a:b:b0:506:70e:96fe with SMTP id d75a77b69052e-50741f03403mr67860561cf.18.1772120437064;
        Thu, 26 Feb 2026 07:40:37 -0800 (PST)
ARC-Seal: i=1; a=rsa-sha256; t=1772120437; cv=none;
        d=google.com; s=arc-20240605;
        b=SdD0+EYbgQAx6wvt9AC+jJ9ChuMxHcFLNtD/ZN7tUlyTIG+QQEEDnUzMKI1U62cUlt
         ArLYuBwDAUnJiJXZSTpD2AILQ5ZwEVOp2OLhMzia30qi2OV6CA6zpwCfzL4aMXsuSjkH
         FVfrR2pYUBA/m+D4nZlvikFMwCu1EYNuX0XXG1E10U9tPgX5adeDgsTaCscptLQdCuCI
         0X6R7t1H5xWGe26r9Tcfmel3sSNC9nrZFwB0uPy9rso8uxlEoXm65XOzDRspIJpymcZs
         Zg1KJK3/gHi7pNA+rkLVPy89NvqPRUgoPMjcQLvDTUtokb/gQaEzC4+n3uqhryEV79F/
         QeUA==
ARC-Message-Signature: i=1; a=rsa-sha256; c=relaxed/relaxed; d=google.com; s=arc-20240605;
        h=to:sid:list-unsubscribe-post:list-unsubscribe:feedback-id:reply-to
         :subject:message-id:mime-version:from:date:dkim-signature
         :dkim-signature;
        bh=Rd3hQciPsit6GnCwgksRNoZJi0oI+G5sRpayxNOoF28=;
        fh=YwahPXNWtdG6z0gNGeoH51dK0OzJ4UBl6y9zZCtD8sM=;
        b=kgoYKEEgeEC/r5NCX+XhX+JxUNKmZQ8XzM3C/Jl72vPHLNvbJ5Yfyq0MXHEM87mWcu
         v22hC1DFSjQDxqN2KosqXmzavfEdLrPkacXd1o6fK2E3n34lil8cTBLDGUGj95Kax/bL
         MyVswMLUXD2I3HsQmkSaF1JyH9y3zwUEI1clVuHKxEDJtouQWfxuAdgAvM+kvgupWpQv
         PtLazxXnrvKrX6LbHaALhQE1wGiHipyyZxelx9cjGq9UgUepXTOx3uTptlZV85RXT+qq
         HmJzaTLuQmAH0m+hfq3Hzgjfd48hBP+TjWa2NL3e2B4cs9YK5EyAIfPX0Y7OICHrKUcL
         kQ/Q==;
        dara=google.com
ARC-Authentication-Results: i=1; mx.google.com;
       dkim=pass header.i=@mail.beehiiv.com header.s=s1 header.b=RamttR9P;
       dkim=pass header.i=@sendgrid.info header.s=smtpapi header.b=HXyMztxr;
       spf=pass (google.com: domain of bounces+45085160-a3dd-omarm.shaalan=gmail.com@em2003.mail.beehiiv.com designates 159.183.140.172 as permitted sender) smtp.mailfrom="bounces+45085160-a3dd-omarm.shaalan=gmail.com@em2003.mail.beehiiv.com";
       dmarc=pass (p=REJECT sp=REJECT dis=NONE) header.from=beehiiv.com
Return-Path: <bounces+45085160-a3dd-omarm.shaalan=gmail.com@em2003.mail.beehiiv.com>
Received: from o170.ptr9231.mail.beehiiv.com (o170.ptr9231.mail.beehiiv.com. [159.183.140.172])
        by mx.google.com with ESMTPS id d75a77b69052e-50745180235si23525751cf.219.2026.02.26.07.40.36
        for <omarm.shaalan@gmail.com>
        (version=TLS1_3 cipher=TLS_AES_128_GCM_SHA256 bits=128/128);
        Thu, 26 Feb 2026 07:40:37 -0800 (PST)
Received-SPF: pass (google.com: domain of bounces+45085160-a3dd-omarm.shaalan=gmail.com@em2003.mail.beehiiv.com designates 159.183.140.172 as permitted sender) client-ip=159.183.140.172;
Authentication-Results: mx.google.com;
       dkim=pass header.i=@mail.beehiiv.com header.s=s1 header.b=RamttR9P;
       dkim=pass header.i=@sendgrid.info header.s=smtpapi header.b=HXyMztxr;
       spf=pass (google.com: domain of bounces+45085160-a3dd-omarm.shaalan=gmail.com@em2003.mail.beehiiv.com designates 159.183.140.172 as permitted sender) smtp.mailfrom="bounces+45085160-a3dd-omarm.shaalan=gmail.com@em2003.mail.beehiiv.com";
       dmarc=pass (p=REJECT sp=REJECT dis=NONE) header.from=beehiiv.com
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed; d=mail.beehiiv.com; h=content-type:date:from:mime-version:subject:reply-to:feedback-id: list-unsubscribe:list-unsubscribe-post:to:cc:content-type:date:feedback-id:from: subject:to; s=s1; bh=Rd3hQciPsit6GnCwgksRNoZJi0oI+G5sRpayxNOoF28=; b=RamttR9PAGyHTCuqIzG+5H/aE3SvJunz47pLjELqJU+WghxEp2e1jA5RbFkpbMvKT6TG 5KkcTsR0VGC9XdA6pMhfg1SgeU8ZODfqZzYRb79C76qE9djaQKzURVxG2t0o212NBnXER4 kbIgR7s2VrzKxBabPh2jxm6laQ93NJpiSZzyeHATW1HgBv8G/+Y1PAWh0frG1ajIqrg1zP nEJsetDD8USPNHoQzEYv0raWxcu1PlJdZuvg8I/Ri3y+ThIVL58tWZ3Xi32JBz7Tti6U6z kUxNtTRU4crdI+Q0sUE3l8I8pVGoX9Y2fNv2yo9pWIUkrphmy6vxCbuQ5UKRhSpw==
DKIM-Signature: v=1; a=rsa-sha256; c=relaxed/relaxed; d=sendgrid.info; h=content-type:date:from:mime-version:subject:reply-to:feedback-id: list-unsubscribe:list-unsubscribe-post:to:cc:content-type:date:feedback-id:from: subject:to; s=smtpapi; bh=Rd3hQciPsit6GnCwgksRNoZJi0oI+G5sRpayxNOoF28=; b=HXyMztxrWiLqEKMELLzbF8Rvic2Da3O8iSNSejfK3mKW69QNDWD7kZmCZBd3TJj+E8K9 wsjcC8wtgZ5LCDJ/EsrpEGHQFYX8ZJeU+P+Zn59R9J2geMfcDp/lYdA1L5BhV+Dr5ya3Dy Uu5aZTwLaaEAdbRXJk4zUX+O33eWTSEUw=
Received: by recvd-fc9cdddfd-ktrd2 with SMTP id recvd-fc9cdddfd-ktrd2-1-69A0696F-107 2026-02-26 15:40:31.914352434 +0000 UTC m=+6111245.648131086
Received: from NDUwODUxNjA (unknown) by geopod-ismtpd-40 (SG) with HTTP id PDbHzXEPTCiHnPnTNN34DA Thu, 26 Feb 2026 15:40:31.894 +0000 (UTC)
Content-Type: multipart/alternative; boundary=ea150e9e1f981ef6d50f48b023fbdb15c63834363b03944572ee930e9d08
Date: Thu, 26 Feb 2026 15:40:36 +0000 (UTC)
From: Aiden Ng <unemployed@mail.beehiiv.com>
Mime-Version: 1.0
Message-ID: <PDbHzXEPTCiHnPnTNN34DA@geopod-ismtpd-40>
Subject: Summer 2026 Internships + Jobs
Reply-To: David <dchen0902@gmail.com>
Feedback-ID: 859548da-f09d-4b10-bff8-8563522bfa3f:newsletter:9b9de07b-c455-43a1-baaa-1d7ebcb05009:e65db6516d371c4
List-Unsubscribe: <mailto:9b9de07b-c455-43a1-baaa-1d7ebcb05009+d377cb98-0a79-4f3c-bdcc-79e16ce6700b+859548da-f09d-4b10-bff8-8563522bfa3f@unsub.beehiiv.com>, <https://unemployed.beehiiv.com/unsubscribe/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWJzY3JpYmVyX2lkIjoiZDM3N2NiOTgtMGE3OS00ZjNjLWJkY2MtNzllMTZjZTY3MDBiIiwicG9zdF9pZCI6Ijg1OTU0OGRhLWYwOWQtNGIxMC1iZmY4LTg1NjM1MjJiZmEzZiIsImxhc3RfcmVzb3VyY2VfZ3VpZCI6IlBvc3Q6ODU5NTQ4ZGEtZjA5ZC00YjEwLWJmZjgtODU2MzUyMmJmYTNmIn0.Cr4IKG1r35OmXtXWkJnvnZpq7sc6AFCV2_4JYBOOpo8>
List-Unsubscribe-Post: List-Unsubscribe=One-Click
sId: 9b9de07b-c455-43a1-baaa-1d7ebcb05009
x-beehiiv-ids: {"account_name":"https://unemployed.beehiiv.com/","campaign_id":"859548da-f09d-4b10-bff8-8563522bfa3f","category":"newsletter","email_generated_at":1772120431,"user_id":"9b9de07b-c455-43a1-baaa-1d7ebcb05009"}
x-beehiiv-type: newsletter
x-list-id: 9b9de07b-c455-43a1-baaa-1d7ebcb05009
x-list-owner: <mailto:dchen0902@gmail.com>
x-newsletter: https://unemployed.beehiiv.com/p/summer-2026-internships-jobs-5f61
x-newsletter-id: https://unemployed.beehiiv.com/
x-newsletter-signup: https://unemployed.beehiiv.com/subscribe
X-SG-EID: u001.x/TvG18e2DBnWVColOBxHCYV6R3XjLeJTzHGERtbRgsdK9AfndmT51FuUtd+DD8lvCVcr5f3AdC/O40PoOKXea9+2TsfZrAJ3gOS3kcRHFbODXTIfkc13EjBTIDGY0sLg6P1Y+VkCV7BYYW1VeueImIjHPAoGbiQ1MTvHrX9bikoXoasnYIUPIre58pgWlDOQFOM4+LpokzoYfSO0yh5K9JCTrW7Zx3tuWj6VFBWkv1CYbZkJ9nr1yByo9pcoeNg
X-SG-ID: u001.SdBcvi+Evd/bQef8eZF3BpTL9BgbK5wfSJMJGMsmprD1ZcmFObA4po1bGaUE6gycYYdT0r6pV5dYgz3HN6x6AQ94dTlYnWOe4wgSyCVCaDYCx6xv6zIbeMIVdllmDw/Cy1by2XNsPFFVzA8WbNeBLsRJLh3QXyaFOZo5wcc5su9yK4hPCQRM2k+xjrdyGxIglBGaGRjNngrcqonU+XL5nc6YCrEBV1cOf8CPKnZkUHmavZ+d70TLjL3s2rFdL/AQJ9iTTiwMJ9i8FaVBK1ZDK5nZYA0yYoftksyx6AdL23/SBciyaH1OEs8cpqdO+cY3vBL1U41e1eONMA8j5q/en2VcKjCcuU5nXYY55bM7EzM=
To: "omarm.shaalan@gmail.com" <omarm.shaalan@gmail.com>
X-Entity-ID: u001.JpuMGkTkD8PwBFu6+mygNQ==

--ea150e9e1f981ef6d50f48b023fbdb15c63834363b03944572ee930e9d08
Content-Transfer-Encoding: quoted-printable
Content-Type: text/plain; charset=utf-8
Mime-Version: 1.0
```

<img width="3666" height="1479" alt="Pasted image 20260228165919" src="https://github.com/user-attachments/assets/d821077d-b62c-447c-a993-f32a47655f4f" />


From this screenshot we can interpret that the total delay from sender to recipient was **0 sec** 

The traffic passed by **4 hops**
- 1st Hop
	The email was submitted via an **HTTP-based API**
	The **Form** value looks base64-encoded
- 2nd Hop 
	Internal mail transfer within the sending provider's infrastructure
- 3rd Hop
	The sending server belongs to **Beehiiv.com**
	The receiving server is **Google** (mx.google.com)
	ESMTPS = **Encrtpyed** SMTP (TLS)
	The IP **159.183.140.172** was not blacklisted
	The email was successfully delivered to Google's mail infrastructure **(Gmail)**
- 4th Hop
	**2002:a05:6802:66c6:b0:619:5591:96c1** is an internal IPv6 routing inside Google's infrastructure after receipt

The sender IP address : 159.183.140.172

I checked this IP and it seemed that this traffic was coming from California,US


### GG✌️


