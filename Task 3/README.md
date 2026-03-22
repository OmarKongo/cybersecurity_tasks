# Enumeration

### TT3.1 NetBIOS Enumeration

Target : Windows server (192.168.1.159)

```powershell
C:\Users\Omar>nbstat -a 192.168.1.159

Wi-Fi:
Node IpAddress: [192.168.1.8] Scope Id: []

           NetBIOS Remote Machine Name Table

       Name               Type         Status
    ---------------------------------------------
    WIN-5DQG5PCULQK<20>  UNIQUE      Registered
    WIN-5DQG5PCULQK<00>  UNIQUE      Registered
    WORKGROUP      <00>  GROUP       Registered

    MAC Address = 00-0C-29-77-BF-A0

```


### TT3.2 LDAP Enumeration



```bash
┌──(kali㉿kongo)-[~]
└─$ ldapsearch -H ldap://ldap.forumsys.com -x -D "cn=read-only-admin,dc=example,dc=com" -w password -b "dc=example,dc=com" "uid=*"
# extended LDIF
#
# LDAPv3
# base <dc=example,dc=com> with scope subtree
# filter: uid=*
# requesting: ALL
#

# newton, example.com
dn: uid=newton,dc=example,dc=com
sn: Newton
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
uid: newton
mail: newton@ldap.forumsys.com
cn: Isaac Newton

# einstein, example.com
dn: uid=einstein,dc=example,dc=com
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
cn: Albert Einstein
sn: Einstein
uid: einstein
mail: einstein@ldap.forumsys.com
telephoneNumber: 314-159-2653

# tesla, example.com
dn: uid=tesla,dc=example,dc=com
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
objectClass: posixAccount
cn: Nikola Tesla
sn: Tesla
uid: tesla
mail: tesla@ldap.forumsys.com
uidNumber: 88888
gidNumber: 99999
homeDirectory: home

# galileo, example.com
dn: uid=galileo,dc=example,dc=com
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
cn: Galileo Galilei
sn: Galilei
mail: galileo@ldap.forumsys.com
uid: galileo

# euler, example.com
dn: uid=euler,dc=example,dc=com
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
uid: euler
sn: Euler
cn: Leonhard Euler
mail: euler@ldap.forumsys.com

# gauss, example.com
dn: uid=gauss,dc=example,dc=com
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
cn: Carl Friedrich Gauss
sn: Gauss
uid: gauss
mail: gauss@ldap.forumsys.com

# riemann, example.com
dn: uid=riemann,dc=example,dc=com
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
cn: Bernhard Riemann
sn: Riemann
uid: riemann
mail: riemann@ldap.forumsys.com

# euclid, example.com
dn: uid=euclid,dc=example,dc=com
uid: euclid
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
cn: Euclid
sn: Euclid
mail: euclid@ldap.forumsys.com

# test, example.com
dn: uid=test,dc=example,dc=com
objectClass: posixAccount
objectClass: top
objectClass: inetOrgPerson
gidNumber: 0
givenName: Test
sn: Test
displayName: Test
uid: test
initials: TS
homeDirectory: home
cn: Test
uidNumber: 24601
o: Company

# curie, example.com
dn: uid=curie,dc=example,dc=com
uid: curie
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
cn: Marie Curie
sn: Curie
mail: curie@ldap.forumsys.com

# nobel, example.com
dn: uid=nobel,dc=example,dc=com
uid: nobel
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
mail: nobel@ldap.forumsys.com
sn: Nobel
cn: Alfred Nobel

# boyle, example.com
dn: uid=boyle,dc=example,dc=com
uid: boyle
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
cn: Robert Boyle
sn: Boyle
mail: boyle@ldap.forumsys.com
telephoneNumber: 999-867-5309

# pasteur, example.com
dn: uid=pasteur,dc=example,dc=com
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
sn: Pasteur
cn: Louis Pasteur
uid: pasteur
telephoneNumber: 602-214-4978
mail: pasteur@ldap.forumsys.com

# nogroup, example.com
dn: uid=nogroup,dc=example,dc=com
uid: nogroup
objectClass: inetOrgPerson
objectClass: organizationalPerson
objectClass: person
objectClass: top
cn: No Group
mail: nogroup@ldap.forumsys.com
sn: Group

# search result
search: 2
result: 0 Success

# numResponses: 15
# numEntries: 14


```

- 14 users & groups
- A **DN** is a sequence of relative distinguished names (RDN) connected by commas.
- An **RDN** is an attribute with an associated value in the form **attribute**=_value_; normally expressed in a UTF-8 string format. The following table lists typical RDN attribute types.

|String|Attribute type|
|---|---|
|**DC**|domainComponent|
|**CN**|commonName|
|**OU**|organizationalUnitName|
|**O**|organizationName|
|**STREET**|streetAddress|
|**L**|localityName|
|**ST**|stateOrProvinceName|
|**C**|countryName|
|**UID**|userid|

Example on dn from the above results

```bash
dn: uid=newton,dc=example,dc=com
```

### TT3.3 DNS Enumeration

```bash
┌──(kali㉿kongo)-[~]
└─$ dig ns www.certifiedhacker.com

; <<>> DiG 9.20.9-1-Debian <<>> ns www.certifiedhacker.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 36524
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 3

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;www.certifiedhacker.com.       IN      NS

;; ANSWER SECTION:
www.certifiedhacker.com. 14400  IN      CNAME   certifiedhacker.com.
certifiedhacker.com.    86400   IN      NS      ns2.bluehost.com.
certifiedhacker.com.    86400   IN      NS      ns1.bluehost.com.

;; ADDITIONAL SECTION:
ns2.bluehost.com.       1309    IN      A       162.159.25.175
ns1.bluehost.com.       1786    IN      A       162.159.24.80

;; Query time: 238 msec
;; SERVER: 163.121.128.134#53(163.121.128.134) (UDP)
;; WHEN: Sun Mar 22 02:32:33 EET 2026
;; MSG SIZE  rcvd: 143

```

Nameservers
- certifiedhacker.com.    86400   IN      NS      ns2.bluehost.com.
- certifiedhacker.com.    86400   IN      NS      ns1.bluehost.com.

Results from a kali machine

```bash
┌──(kali㉿kongo)-[~]
└─$ dig @ns1.bluehost.com www.certifiedhacker.com axfr

; <<>> DiG 9.20.9-1-Debian <<>> @ns1.bluehost.com www.certifiedhacker.com axfr
; (1 server found)
;; global options: +cmd
; Transfer failed.

```


Results from a windows machine

```powershell
C:\Users\Omar>nslookup
Default Server:  h188a
Address:  fe80::1

> set querytype=soa
> certifiedhacker.com
Server:  h188a
Address:  fe80::1

Non-authoritative answer:
certifiedhacker.com
        primary name server = ns1.bluehost.com
        responsible mail addr = dnsadmin.box5331.bluehost.com
        serial  = 2025100600
        refresh = 86400 (1 day)
        retry   = 7200 (2 hours)
        expire  = 3600000 (41 days 16 hours)
        default TTL = 300 (5 mins)
        
> ls -d ns1.bluehost.com
[h188a]
*** Can't list domain ns1.bluehost.com: Unspecified error
The DNS server refused to transfer the zone ns1.bluehost.com to your computer. If this
is incorrect, check the zone transfer security settings for ns1.bluehost.com on the DNS
server at IP address fe80::1.
```

- I cannot perform zone transfer on the primary host of certifiedhacker.com since i am not allowed to do so on this nameserver
- responsible mail addr = dnsadmin.box5331.bluehost.com


### TT3.4 SMTP Enumeration

```bash
┌──(kali㉿kongo)-[~]
└─$ nmap -p 25 --script=smtp-enum-users smtp.freesmtpservers.com
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-22 02:42 EET
Nmap scan report for smtp.freesmtpservers.com (104.237.130.88)
Host is up (0.20s latency).
rDNS record for 104.237.130.88: li806-88.members.linode.com

PORT   STATE    SERVICE
25/tcp filtered smtp

Nmap done: 1 IP address (1 host up) scanned in 2.85 seconds

┌──(kali㉿kongo)-[~]
└─$ nmap -p 25 --script=smtp-open-relay smtp.freesmtpservers.com
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-22 02:44 EET
Nmap scan report for smtp.freesmtpservers.com (104.237.130.88)
Host is up (0.16s latency).
rDNS record for 104.237.130.88: li806-88.members.linode.com

PORT   STATE    SERVICE
25/tcp filtered smtp

Nmap done: 1 IP address (1 host up) scanned in 2.08 seconds

┌──(kali㉿kongo)-[~]
└─$ nmap -p 25 --script=smtp-commands smtp.freesmtpservers.com 
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-22 02:44 EET
Nmap scan report for smtp.freesmtpservers.com (104.237.130.88)
Host is up (0.24s latency).
rDNS record for 104.237.130.88: li806-88.members.linode.com

PORT   STATE    SERVICE
25/tcp filtered smtp

Nmap done: 1 IP address (1 host up) scanned in 2.89 seconds

```


I tried both nmap and zenmap. I didn't get any results since this port is filtered. Also, i tried all the scripts that are relevant to smtp

```bash
┌──(kali㉿kongo)-[~]
└─$ nmap -p 25 --script=smtp* smtp.freesmtpservers.com
Starting Nmap 7.95 ( https://nmap.org ) at 2026-03-22 02:49 EET
Nmap scan report for smtp.freesmtpservers.com (104.237.130.88)
Host is up (0.17s latency).
rDNS record for 104.237.130.88: li806-88.members.linode.com

PORT   STATE    SERVICE
25/tcp filtered smtp

Nmap done: 1 IP address (1 host up) scanned in 2.22 seconds
```

<img width="629" height="248" alt="Pasted image 20260322025347" src="https://github.com/user-attachments/assets/d51d331f-e1cd-4ada-95a4-8c496dd62995" />

