---
layout: post
title:  "RSA Public Key Encryption with a toy example"
date:   2013-10-16 00:00:00
categories: forensics-and-security
tags: [security, encryption]

---
There are countless papers already written on the history of RSA and it's usage in public key encryption. In this article I want to focus on the bare nuts and bolts - that is how it works on a mathematical level.

RSA security is based on the ***Integer Factorization Problem***, which is what we call a very hard problem to solve. Loosely it's given two primes *p* and *q*, compute the modulus *N* and φ(N) . The multiplication is easy however given only *N* the inverse is difficult i.e. factoring *N* into *p* and *q*.
<linebreak>
##RSA Theory in 3 steps

###1. Key Generation

1. Generate 2 large distinct primes *p* and *q* of roughly the same size (e.g. 1024 each) 
2. Compute the modulus *N* where ```N=pq```
3. Compute Totient(φ) of *N* where ```φ(N)= (p–1)(q–1)```
4. Select random integer *e* as the public key component with ```1 < e < φ(N), where 1 ≡ gcd(e, φ(N))```
	- i.e. ***e*** is relatively prime to ***N*** and has an inverse so that decryption can occur.
Common values for e include 3,17 and 65537 as they only have 2 bits set and make calculation easy using the square and multiply rule.
5. Use Euclids Extended Algorithm to compute the inverse of *e*, private key component *d* where

```	
1 < d < φ(N)
ed ≡ 1(mod φ(N))
```

From this we have

```
Public Key = (e,N)
Private Key = (d, N)
```

Now *d,p* and *q* are kept private or even better *p* and *q* destroyed!!

### 2. Encryption

We can encrypt *m* such that ```0<=m<n ``` using

> c ≡ m<sup>e</sup>(mod N)

### 3. Decryption

We can encrypt *c* such that ```0<=c<n ``` using

> m ≡ c<sup>d</sup> (mod N)

##A Toy Example

Encrypt and decrypt a message *m* with RSA 

###Key Generation:

Choose primes 

	p=7 and q=11.

Compute the modulus

	N=pq=7x11=77

Compute Totient of *N*

	φ(N) = (p−1)(q−1) 
	= 6×10 
	= 60.

Choose Public Key Component *e* 

	e = 37, which is valid since gcd(37,60) = 1.

Create Private Key Component*d*

	ed ≡ 1(mod φ(N))
	since 37×13 ≡ 481 ≡ 1 (mod 60)
	d=13

From this we have

	Public key = (37,77) 
	Private key = (13,77).

###Encryption

Suppose m = 2 then:

> c ≡ m<sup>e</sup>(mod N)≡237 (mod 77)≡51

###Decryption

To recover m compute:

> m ≡ c<sup>d</sup> (mod N)≡5113 (mod 77)≡2

