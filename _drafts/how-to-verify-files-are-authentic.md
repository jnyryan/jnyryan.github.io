---
layout: post
title:  "how to verify file hashes and signatures"
date:   2014-01-16 00:00:00
categories: forensics-and-security playing-with-technology
description: 
categories: better-engineering-practices
tags: [practices, development, security, pgp]

---

It's very easy to ignore the hashes and signatures provided with downloads, but guess what - ***it's also very easy to check them!***

### Verify a sha1

First download a file like [pgp4win](http://www.gpg4win.org/download.html)

	openssl sha1 gpg4win-2.2.1.exe


### Validate an OpenPGP signature 

