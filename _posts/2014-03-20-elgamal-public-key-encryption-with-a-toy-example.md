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
1. Select a large random prime *p* and a generator *α* of Z<sup>∗</sup><sub>p</sub>
2. Generate a random integer x such that 1≤x≤p−2 
3. Compute y = α<sup>x</sup>mod p4. public key is ***(p, α, y)***5. private key is ***x***

### 2. Encryption

Given a message m such that 0 ≤ m < p, any user B can encrypt m as follows: 

1. Pick the integer k ∈ {1..p−2} uniformly at random.2. Compute c1 = α<sup>k</sup> mod p3. Compute c2 =m×y<sup>k</sup> (mod p)4. The ciphertext is the pair ***(c1, c2)***

### 3. Decryption

A can decrypt (c1, c2) as follows:
1. Compute m = (c<sup>p−1−x</sup>) × c (mod p)

##A Toy Example

Encrypt and decrypt a message *m* with ElGamal 

###Key Generation:

Select a prime p = *809*, then 809 - 1 = 808 is divisible by q = 101. 

	p = 809

Compute a generator *g* of the multiplicative group Z∗p.

	g = 3
Choose a random private key *a*
	
	a = 68

Compute 
	
	ga (mod p)≡368 (mod p)≡65
- Public key is ***(p = 809, g = 3, y = 65)***
- Private key is ***x = 68***

###Encryption

To encrypt the message 

	m = 100

Selects a random integer 

	k = 89 
	
Computes: 

> c1 =gk =345
> 
> c2 = m * x<sup>k</sup> =517The ciphertext is ***(c1||c2)***

###Decryption

To decrypt

First compute:
 >c1<sup>p−1−x</sup>(mod p)≡345740 
(mod809)≡720(mod809) 

Recover m by computing:
> m ≡ 720*517 (mod 809) ≡ 100 (mod 809)
