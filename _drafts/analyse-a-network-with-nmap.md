---
layout: post
title:  "Analyse a network with nmap"
date:   2014-03-7 00:00:00
categories: forensics-and-security
description: 
tags: [security, networks]

---

http://en.wikibooks.org/wiki/Hacking/Tools/Network/Nmap

##Analyse the network architecture

The following will search silently for all ftp,telnet, web and DNS servers listening on the network
	
	nmap -sS -p:21-23,80,57 192.188.1.0-255 
