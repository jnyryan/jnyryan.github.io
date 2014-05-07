---
layout: post
title:  "ElGamal Public Key Encryption with a toy example"
date:   2014-03-20 00:00:00
categories: forensics-and-security
tags: [security, encryption]

---

Having already looked a few months ago at RSA, it's time to kick the tyres on a ElGamal example of public key encryption. Like the last example, in this article I want to focus on the bare nuts and bolts - that is how it works on a mathematical level.

ElGamal security is based on the ***Discrete Log Problem***, which is what we call a very hard problem to solve. Loosely it's ...

<linebreak>

##Elgamal Theory in 3 steps

###1. Key Generation

Generate a key-pair as follows:

2. Generate a random integer x such that 1≤x≤p−2 
3. Compute y = α<sup>x</sup>mod p

### 2. Encryption

Given a message m such that 0 ≤ m < p, any user B can encrypt m as follows: 

1. Pick the integer k ∈ {1..p−2} uniformly at random.

### 3. Decryption

A can decrypt (c1, c2) as follows:


##A Toy Example

Encrypt and decrypt a message *m* with ElGamal 

###Key Generation:

Select a prime p = *809*, then 809 - 1 = 808 is divisible by q = 101. 

	p = 809

Compute a generator *g* of the multiplicative group Z∗p.

	g = 3

	
	a = 68

Compute 
	
	ga (mod p)≡368 (mod p)≡65

- Private key is ***x = 68***

###Encryption

To encrypt the message 

	m = 100

Selects a random integer 

	k = 89 
	
Computes: 

> c1 =gk =345
> 
> c2 = m * x<sup>k</sup> =517

###Decryption

To decrypt

First compute:
 
(mod809)≡720(mod809) 

Recover m by computing:
