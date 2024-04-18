# Elliptic Curves

Generally speaking, elliptic curves (EC) are geometric objects in projective planes over a given field, made up of points that satisfy certain equations. But in this lesson we are going to understand how EC works from the point of view of cryptography. 

![alt text](/Images/image-7.png)

The equation above is what is called Weierstrass normal form for elliptic curves. Depending on the value $a$ and $b$ , elliptic curves may assume different shapes on the plane. As it can be easily seen and verified, elliptic curves are symmetric about the x-axis.

We will also need a point at infinity (also known as ideal point) to be part of our curve and denote with the symbol 0 (zero).

In order for the set $G$ to be a group, an addition operation must satisfies Abelian Group Properties and for the next 4 properties:

- The elements of the group are the points of an elliptic curve.
- The identity element is the point at infinity 0, such that $a+0=0+a=a$
- The inverse of a point $P$ is the one symmetric about the x-axis.
- Addition operation is given by the following rule: given three aligned, non-zero points $P, Q, R$, their sum is $P+Q+R=0$. This means that, if $P,Q,R$ are aligned, then $P + (Q+R) = Q + (P+R) = R+(P+Q) = ... = 0$. This way, we proved that our operator is both associative and commutative, and we are in an abelian group.

![alt text](/Images/image-8.png)

If we want to perform point addition $P+Q+R=0$, then $P+Q = -R$. The corner cases are when we have symmetric points and one zero point, we already know that $P+(-P)=0$ and $P+0=0+P=P$.

![alt text](/Images/image-9.png)

Let’s remember that when we use modular math, we consider a set $Z_n$, this is the finite field or the set of integers module p. Now, we need to define how elliptic curve works over a finite field. 

The set of points that are described by the equation of a elliptic curve and the point at infinity, now becomes a set of points where $a$ and $b$ are two integers that belong to $Z_n$. Mathematically, is described as follows:

![alt text](/Images/image-10.png)

What previously was a continuous curve is now a set of disjoint points in the xy-plane. But even if we have restricted our domain, elliptic curves in an finite field still form an abelian group. For example:

![alt text](/Images/image-11.png)

Clearly, we need to change a bit our definition of addition in order to make it work in a finite field. With reals, we said that the sum of three aligned points was zero $(P + Q + R = 0)$. We can keep this definition, but what does it mean for three points to be aligned in a finite field? We can say that three points are aligned if there's a line that connects all of them. But lines if a finite field are not the same as lines in real field.

![alt text](/Images/image-12.png)

For example:
![alt text](/Images/image-13.png)

Given that we are in a group, point addition retains the properties we already know:

![alt text](/Images/image-14.png)

The equations for calculating point additions are exactly the same as in real field, except for the fact that we need to add "mod p" at the end of every expression.

![alt text](/Images/image-15.png)

In this lesson we learn the basis about elliptic curves. In the next lesson we are going to talk about a particular type ok ZKP, the Non-interactive Zero Knowledge Proof. 