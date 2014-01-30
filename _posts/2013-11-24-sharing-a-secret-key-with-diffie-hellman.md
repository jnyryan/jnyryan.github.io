---
layout: post
title:  "Sharing a secret key with Diffie-Hellman"
date:   2013-11-24 00:00:00
categories: forensics-and-security

---
One of the major problems to overcome in synchronious cryptography is the distribution of keys. For each message encrypted the key along with the message must be communicated to the desired recpient. In  1976 Diffie and Hellman came up with a method for establishing a shared secret key over an insecure communication channel, and it's known as the **Diffie-Hellman key exchange**
 
As an aside, this method was already discovered by the British Secret Service at UK GCHQ but was subject to the official secrets act. 

The security here is based on the Integer Factorization Problem which is what we call a **very hard problem** to solve. Loosely it's given two primes *p* and *q*, compute *N=pq*. The multiplication is easy however the inverse is difficult i.e. factoring *N* into *p* and *q* 

###Diffie-Hellman Key Exchange Theory
For Diffie-Hellman, we select:

- a large prime *p*(> 2<sup>400</sup>) 
- a generator *g* 

Then using these as a base the two parties (A and B) who want to communicate create a private key

1. A chooses a random **x** such that **1 < x < p−1**2. A → B:g<sup>x</sup>(mod p)3. B chooses a random **y** such that **1 < y < p−1**.
4. B→A: g<sup>y</sup> (mod p)5. A computes K = (g<sup>y</sup>)<sup>x</sup> (mod p).6. B computes K = (g<sup>x</sup>)<sup>y</sup> (mod p).7. A and B now share the secret K.###Diffie-Hellman Key Exchange Toy ExampleA toy example (p = 11, g = 5). 

**Choose Private keys**

- x=3- y=4 

**Generate Public keys**
A and B each generate a public key(X and Y) that they share to the other
- X =g<sup>x</sup> (mod p)=53 (mod 11)=125 (mod 11)=4- Y =g<sup>y</sup> (mod p)=54 (mod 11)=625 (mod 11)=9 

Determine the Shared Secret:A and B then use the known public key, generator and prime to generate a shared key:
- Y<sup>x</sup> (mod p)=9<sup>3</sup> (mod 11)=729 (mod 11)=3 
- X<sup>y</sup> (mod p)=4<sup>4</sup> (mod 11)=256 (mod 11)=3

Now in this example, *3* is the shared secret that can be used as the key/password for whatever encryption algorithm A and B want to use to communicate securely.