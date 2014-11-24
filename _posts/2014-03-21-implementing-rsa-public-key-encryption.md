---
layout: post
title:  "Implementing classic RSA Encryption"
date:   2014-03-21 00:00:00
categories: forensics-and-security
description:
tags: [development, cryptography, security]

---

I figure the best way to get to know something is to do it, and now i want to know how basic RSA Cryptography works. In this post, i'm going to implement the methods required for RSA. Taking a top down approach and will implement the required functions as needed.

The important thing to remember is that these are designed to work on large numbers, i tested these on numbers with 300 digits!

### Encrypt/Decrypt and Key Generation methods

These are the main methods used to turn plaintext into ciphertext. not much too them, but as you can see we do not have the public key values (e,n) and private key values (d,n) yet.

```python
#encrypt a message m, with public key e using modulus n
def rsaEnc(n,e,m):
	return expm(m, e, n)
```

<linebreak>

``` python
#decrypt a cipher c, with private key d using modulus n
def rsaDec(n,d,c):
	return expm(c, d, n)
```

This is the function that does the magic. It creates out public and private key pairs.

```python
#Generate the keys needed for encryption of size s bites
def rsaKey(s):
	#create 2 large primes of size s
	p=create_prime(s)
	q=create_prime(s)
	#calculate their modulus
	n=p*q
	#calculate their totient
	phi=(p-1)*(q-1)
	#choose a encryption exponent e such that, 1<e<phi and 1=gcd(e,phi)
	e=1
	while e < phi:
		if(1==gcd(e,p))
			break
		e=e+1
	#determine the decryption exponent d, which is the modular inverse of e
	d=p3_invm.invm(phi,e)
	return n,e,d
```

### Calculate the exponents... fast

Use the ***square and multiply*** method to do the exponentiation. A fast method of raising to a power is required as this is how every block is encrypted and decrypted. Imagine raising to a power that's 1024 digits in length - you will have to be efficient.

``` python
#Calulate a**k modulo m.
def expm( a, k, n):
	r = 1
	bits = list(bin(k)[2:])
	for bit in bits:
		r = (r * r) % n
		if int(bit) == 1:
			r = (r * a) % n
	return r
```

### Create the Primes

Generate the primes used to base the encryption on. This will give a prime with a probability of 1/2**30

``` python
import random
# Generate a Prime using Fermats Theorem of d bits
def prime(d):
	isprime = False
	while isprime ==  False:
		r = random.getrandbits(d)
		isprime = is_prime(r, 30)
	return r
```

```python
import random
def is_prime(n, t):
	for i in xrange(1, t):
    		a = random.randint(2, n-1)
    		r = p5_expm.expm(a, n-1, n)
    		if r != 1:
    			return False
    return True
```

### Calculate the greatest common divisor

``` python
# Use Euclid's algorithm to implement the routine to the calculate the Greatest Common Divisor of a and b.
def gcd(a, b):
    while b > 0:
        a, b = b, a%b
    return a
```

### Calculate the modular inverse

``` python
"""
Use the Extended Euclidean Algorithm to implement the routine where a call gcde(a, b) will return a tuple (g; x; y) of three integers such that:
- g = gcd(a; b)
- a  x + b  y = g
"""
def egcd(a, b):
    x,y, u,v = 0,1, 1,0
    while a != 0:
        q, r = b//a, b%a
        m, n = x-u*q, y-v*q
        b,a, x,y, u,v = a,r, u,v, m,n
    return b, x, y
```

``` python
"""
Implement the routine that computes the inverse of a modulo m.
"""
def invm(m, a):
	g, x, y = egcd(a, m)
	if g != 1:
		return None  # modular inverse does not exist
	else:
		return x % m
```

With all these done, you should have a working version of RSA. It's not very robust and will be slow at very large numbers - but the theory is there.
