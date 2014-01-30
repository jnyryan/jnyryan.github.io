---
layout: post
title:  "RSA Public key Encryption with a toy example"
date:   2013-10-16 00:00:00
categories: forensics-and-security

---
There are countless papers already written on the history of RSA and it's usage in public key encryption. In this article i want to focus on the bare nuts and bolts - that is hw it works on a mathematical level.

RSA security is based on the Integer Factorization Problem which is what we call a very hard problem to solve. Loosely it's given two primes *p* and *q*, compute *N=pq*. The multiplication is easy however the inverse is difficult i.e. factoring *N* into *p* and *q*

###RSA Theory in 3 steps

Compute Totient(φ) of *N*

	N=pq
	φ(N)= (p–1)(q–1)

Select random integer *e* as the public key component with:

	1 < e < φ(N)
	where 1 ≡ gcd(e, φ(N)), 
	i.e. e is relatively prime to N
	
Use Eculids Extended Algorithm to compute the private key component *d*
	
	1 < d < φ(N)
	ed ≡ 1(mod φ(N))

From this we have

	Public Key = (e,N)
	Private Key = (d, N)

###A toy example

Choose primes 

	p=7 and q=11.

Key Generation:

Compute Totient of *N*

	N =77
	φ(N) = (p−1)(q−1) = 6×10 = 60.

Choose *e* 

	e = 37, which is valid since gcd(37,60) = 1.

Using the extended Euclidean algorithm

	compute d=13 since 37×13 ≡ 481 ≡ 1 (mod 60).

From this we have

	Public key = (37,77) 
	Private key = (13,77).

###Encryption

suppose m = 2 then:

c ≡ m<sup>e</sup>(mod N)≡237 (mod 77)≡51

###Decryption

to recover m compute:

m ≡ c<sup>d</sup> (mod N)≡5113 (mod 77)≡2

