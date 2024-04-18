# Chapter 1. Math and Review

In this chapter, we  provide a comprehensive introduction to the mathematical and cryptography foundations involved in the construction of Zero-Knowledge proof (ZKP). Why? Because some parts of ZKP, such as, public instances and witnesses are numbers modulo a cryptographic prime.

## Modular arithmetic 

Modular math is a fundamental component of cryptographic. The idea is essentially very simple and is identical to the “clock arithmetic” you learn in school. 

More formally, let $n$ be a positive integer. We denote the set $[0..n−1]$ by $Z_n$. We say that two integers $x$ and $y$ are the same (congruent) if differ by a multiple of n.  Mathematically, we write this as $x=y(mod\; n)$. 

We may omit ($mod\; n$) when it is clear from context. Every integer $x$ is congruent to some $y$ in $Z_n$. When we add or subtract multiples of $n$ from an integer $x$ to reach some $y ∈ Z_n$, we say are reducing $x\; module\; n$, and $y$ is the residue. For example:

![alt text](/Images/image-1.png)

## Polynomial constraints 

A polynomial is an expression consisting of variables (also called indeterminates) and coefficients that involves only the operations of addition, subtraction and multiplication. All coefficients of a polynomial must have the same type, e.g. they must all be integers or they must all be rational numbers, etc. In a ZKP, the constraint must be polynomial. 

A constraint is a set of conditions, namely linear equations and inequalities, that represent an input or output value. These equations and inequalities describe the limiting conditions of the computation, implying that satisfying these conditions correctly calculates the corresponding output result for the given input sequence. Example of valid polynomials:
$$a+b * c = d$$
$$x^2 + y^2 = z^2$$

Not valid polynomials: division, equality check and branching.

## Diffie - Hellman algorithm.

One of the first practical implementations of public-key cryptography was Diffie - Hellman Algorithm (DHA). This algorithm was published in 1976 by Whitfield Diffie and Martin Hellman. It is a key - exchange protocol that enables two parties communicating over public channel to establish a mutual secret without it being transmitted over the Internet. Let's consider the following example:

![alt text](/Images/image-2.png)

Now Alice and Bob know to encrypt/decrypt their messages using the shared secret key 10.

DHA uses a private-public key pair to establish a shared secret, typically a symmetric key, is not a symmetric algorithm – it is an asymmetric algorithm used to establish a shared secret for a symmetric key algorithm. As you notice, this algorithm is based on some modular math.

## RSA Key Generation

RSA encryption algorithm relies on a concept of public and private keys and the idea of factoring large numbers using prime numbers. Public key is used to encrypt the message and private key is uses to decrypt the message.

To obtain the keys, we need to follow the next steps:

![alt text](/Images/image-3.png)

The idea of RSA is based on the fact that it is difficult to factorize a large integer. The public key consists of two numbers where one number is multiplication of two large prime numbers. A private key is also derived from the same two prime numbers. So if somebody can factorize the large number, the private key is compromised.

Therefore encryption strength totally lies on the key size and if we double or triple the key size, the strength of encryption increases exponentially. RSA keys can be typically 1024 or 2048 bits long, but experts believe that 1024 bit keys could be broken in the near future. But till now it seems to be an infeasible task.

To encrypt and decrypt a message, we consider the following:

![alt text](/Images/image-4.png)

![alt text](/Images/image-5.png)

## Fiat - Shamir Algorithm 

One of the first interactive proof of knowledge algorithm is Fiat - Shamir, which is consider the "grandfather" of ZKPs because allows one to prove information about a number, without revealing the number. The algorithm work as follow:

![alt text](/Images/image-6.png)

For the method to work, the original interactive proof must have the property of being public-coin, i.e. verifier's random coins are made public throughout the proof protocol.

The Fiat–Shamir Algorithm may also be viewed as converting a public-coin interactive proof of knowledge into a non-interactive proof of knowledge. If the interactive proof is used as an identification tool, then the non-interactive version can be used directly as a digital signature by using the message as part of the input to the random oracle.

A random oracle is an oracle (a theoretical black box) that responds to every unique query with a (truly) random response chosen uniformly from its output domain. If a query is repeated, it responds the same way every time that query is submitted.


In the next lesson we are going to talk about Elliptic Curve Cryptography (ECC) and how this concept involved with ZKP. 