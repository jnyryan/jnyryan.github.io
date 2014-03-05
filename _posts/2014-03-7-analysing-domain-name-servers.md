---
layout: post
title:  "Analysing Domain Name Servers"
date:   2014-03-7 00:00:00
categories: forensics-and-security
description: 
tags: [security, networks]

---
An important part of any security setup is to know your network surroundings. The ***dig*** tool (Domain Information Groper) is ideal for this and allow you analyse the Domain Name Servers available to you network. This combined with ***nmap*** can reveal much that is interesting. 

##Analyse the DNS

Use dig to query the "." (the root) name servers. What we see in the query below is the results of what servers will supply data on all top level domains e.g. countries (.ie), generics
(.com), sponsored (.aero) and infrastructure (.arpa). 

```
# The command is of the form :
	dig @server name type	

~$ dig

; <<>> DiG 9.8.3-P1 <<>>
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 17257
;; flags: qr rd ra; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 2

;; QUESTION SECTION:
;.				IN	NS

;; ANSWER SECTION:
.			28237	IN	NS	j.root-servers.net.
.			28237	IN	NS	f.root-servers.net.
.			28237	IN	NS	e.root-servers.net.
.			28237	IN	NS	i.root-servers.net.
.			28237	IN	NS	c.root-servers.net.
.			28237	IN	NS	b.root-servers.net.
.			28237	IN	NS	a.root-servers.net.
.			28237	IN	NS	m.root-servers.net.
.			28237	IN	NS	h.root-servers.net.
.			28237	IN	NS	k.root-servers.net.
.			28237	IN	NS	l.root-servers.net.
.			28237	IN	NS	g.root-servers.net.
.			28237	IN	NS	d.root-servers.net.

;; ADDITIONAL SECTION:
i.root-servers.net.	86400	IN	A	192.36.148.17
d.root-servers.net.	28237	IN	A	199.7.91.13

;; Query time: 98 msec
;; SERVER: 10.131.50.50#53(10.131.50.50)
;; WHEN: Wed Mar  5 09:43:37 2014
;; MSG SIZE  rcvd: 273

```

### Use dig to query the IP of a Host Name

This query will resolve the host to an IP address.

```
~$ dig www.cfii.ie

; <<>> DiG 9.8.3-P1 <<>> www.cfii.ie
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 41664
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;www.cfii.ie.			IN	A

;; ANSWER SECTION:
www.cfii.ie.		3555	IN	A	81.17.250.59

;; Query time: 134 msec
;; SERVER: 10.20.130.20#53(10.20.130.20)
;; WHEN: Wed Mar  5 11:59:58 2014
;; MSG SIZE  rcvd: 45

```

### Tracing a NS query

This query will do the same as above but the TRACE will show the iterative steps taken to resolve the IP across the various Name Servers that had to be quizzed.

```
~$ dig +trace www.cfii.ie

; <<>> DiG 9.8.3-P1 <<>> +trace www.cfii.ie
;; global options: +cmd
.			20051	IN	NS	e.root-servers.net.
.			20051	IN	NS	i.root-servers.net.
.			20051	IN	NS	c.root-servers.net.
.			20051	IN	NS	b.root-servers.net.
.			20051	IN	NS	a.root-servers.net.
.			20051	IN	NS	m.root-servers.net.
.			20051	IN	NS	h.root-servers.net.
.			20051	IN	NS	k.root-servers.net.
.			20051	IN	NS	l.root-servers.net.
.			20051	IN	NS	g.root-servers.net.
.			20051	IN	NS	d.root-servers.net.
.			20051	IN	NS	j.root-servers.net.
.			20051	IN	NS	f.root-servers.net.
;; Received 373 bytes from 10.131.50.50#53(10.131.50.50) in 1177 ms

ie.			172800	IN	NS	gns1.domainregistry.ie.
ie.			172800	IN	NS	ns-ie.nic.fr.
ie.			172800	IN	NS	gns2.domainregistry.ie.
ie.			172800	IN	NS	b.iedr.ie.
ie.			172800	IN	NS	a.iedr.ie.
ie.			172800	IN	NS	ns3.ns.esat.net.
ie.			172800	IN	NS	c.iedr.ie.
ie.			172800	IN	NS	d.iedr.ie.
;; Received 418 bytes from 192.203.230.10#53(192.203.230.10) in 873 ms

cfii.ie.		172800	IN	NS	ns1.blacknight.com.
cfii.ie.		172800	IN	NS	ns2.blacknight.com.
;; Received 79 bytes from 192.93.0.4#53(192.93.0.4) in 198 ms

www.cfii.ie.		3600	IN	A	81.17.250.59
cfii.ie.		3600	IN	NS	ns1.blacknight.com.
cfii.ie.		3600	IN	NS	ns2.blacknight.com.
;; Received 127 bytes from 78.153.212.176#53(78.153.212.176) in 6 ms

```

### Query a NS directly

To see what name servers control .ie domains, query a root NS. These Authorities are deligated to administer the specified zone by the parent. The ADDITIONAL SECTION sepcifies who the query should be passed onto as these servers do not support recursive queries. 

``` bash

dig @m.root-servers.net dit.ie

; <<>> DiG 9.8.3-P1 <<>> @m.root-servers.net dit.ie
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 20405
;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 8, ADDITIONAL: 11
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;dit.ie.				IN	A

;; AUTHORITY SECTION:
ie.			172800	IN	NS	c.iedr.ie.
ie.			172800	IN	NS	d.iedr.ie.
ie.			172800	IN	NS	gns1.domainregistry.ie.
ie.			172800	IN	NS	b.iedr.ie.
ie.			172800	IN	NS	a.iedr.ie.
ie.			172800	IN	NS	ns-ie.nic.fr.
ie.			172800	IN	NS	ns3.ns.esat.net.
ie.			172800	IN	NS	gns2.domainregistry.ie.

;; ADDITIONAL SECTION:
a.iedr.ie.		172800	IN	A	77.72.72.44
b.iedr.ie.		172800	IN	A	77.72.72.34

```

###Determine your local DNS

	scutil --dns | grep nameserver\[[0-9]*\]


###Additional DNS Queries

``` bash
# 	Determine your local DNS
scutil --dns | grep nameserver\[[0-9]*\]
#	Query for Name Server Records for a domain
dig NS dcu.ie
#	Query for Mail Exchange Records for a domain
dig MX dcu.ie

# Query the name server for public website
dig @ns2-ext.dcu.ie www.dcu.ie

```

*Add results here and table to explain the headers

##Request a Zone Transfer

This is a request that is made by DNS servers to an authority to refresh their cache
	
	dig @heanet.ie dit.ie axfr

##Analyse a mail exchange to see if it's an open relay


Check whether any of the mail servers you discovered earlier can act as 
an open mail relay. To conduct the test, connect to a mail server from the 
command line:

``` bash
$ telnet mailhost.computing.dcu.ie 25
...
HELO world
...
HELP...
EHLO world
...
MAIL FROM: joe@happyplace.com
...
RCPT TO: youremailaddress
...
DATA
This is a message to you.
.
```

The above will succeed in sending a message to yourself from a spoofed e-mail 
address (note how the mail server does not request authentication). If you 
can do the same from outside DCU then the mail server is not securely 
configured and is acting as an “open mail relay”.

##Analyse the network architecture

The following will search silently for all ftp,telnet, web and DNS servers listening on the network
	
	nmap -sS -p:21,23,80,57 192.188.1.0-255 

