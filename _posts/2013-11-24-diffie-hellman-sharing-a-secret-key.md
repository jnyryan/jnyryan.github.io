---
layout: post
title:  "Diffie-Hellman: Sharing a secret key"
date:   2013-11-24 00:00:00
categories: forensics-and-security

---
One of the major problems to overcome in synchronious cryptography is the distribution of keys. For each message encrypted the key along with the message must be communicated to the desired recpient. In  1976 Diffie and Hellman came up with a method for establishing a shared secret key over an insecure communication channel, and it's known as the **Diffie-Hellman key exchange**
 
As an aside, this method was already discovered by the British Secret Service at UK GCHQ but was subject to the official secrets act. 

###Diffie-Hellman Key Exchange Theory


- a large prime *p*(> 2<sup>400</sup>) 
- a generator *g* 

Then using these as a base the two parties (A and B) who want to communicate create a private key

1. A chooses a random **x** such that **1 < x < p−1**
4. B→A: g<sup>y</sup> (mod p)

**Choose Private keys**

- x=3

**Generate Public keys**



**Determine the Shared Secret:**


- X<sup>y</sup> (mod p)=4<sup>4</sup> (mod 11)=256 (mod 11)=3

Now in this example, *3* is the shared secret that can be used as the key/password for whatever encryption algorithm A and B want to use to communicate securely.

**How secure is it?**

A and B useg<sup>xy</sup> (mod p) as a shared key. 

An attacker can see g<sup>x</sup> (mod p) and g<sup>y</sup> (mod p)