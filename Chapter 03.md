# Non - Interactive Zero knowledge Proof (NIZK)

NIZK are very suitable for Ethereum blockchain applications because they allow a smart contract to act as a verifier. This way, anyone can generate a proof and send it as part of a transaction to the smart contract, which can perform some action depending on whether the proof is valid or not. Also, this protocol can verify one’s statement to a larger group of people.

The most preferable NIZK is Zero-knowledge Succinct Non-Interactive Argument of Knowledge (zk-SNARK) proof. This protocol add the following features: 

![alt text](/Images/image-16.png)

These properties make zk-SNARK especially suitable for blockchains, where on-chain storage and computation can be expensive and senders often go offline after sending a transaction.

This protocol uses three algorithms: key generation, prover function, verifier function.

![alt text](/Images/image-17.png)

![alt text](/Images/image-18.png)

![alt text](/Images/image-19.png)

When zk-SNARKs are used in blockchains, both the key and proof generation are executed off-chain. Only the general verification algorithm is run inside a smart contract on chain. Also, if we want to use a non-interactive protocol, we need to use a trusted setup. The trusted setup is the process which generates part of the public data used by a prover when computing her proof.

Non-interactivity is only useful if we want to allow multiple independent verifiers to verify a given proof without each one having to individually query the prover. Succinctness is necessary only if the medium used for storing the proofs is very expensive and/or if we need very short verification times.

## Transformation for ZK - SNARK

To apply zk-SNARK, a computation needs to be expressed in terms of algebraic circuit, converted to a constraint system called R1CS, and then finally a form called “quadratic arithmetic program” (QAP). Eran Tromer describe the steps of transformation for zk-SNARK as follows:

![alt text](/Images/image-20.png)
![alt text](/Images/image-21.png)

Transforming the code of a function into a QAP is itself highly nontrivial and is another process that can be run alongside so that if you have an input to the code you can create a corresponding solution (sometimes called “witness” to the QAP). After this, there is another fairly intricate process for creating the actual “zero knowledge proof” for this witness, and a separate process for verifying a proof that someone else passes along to you.

### Computation and algebraic circuit

 We are going to focus on the first step: turning a function into a mathematical representation is to break down the logical steps into the smallest possible oprations, creating an "arithmetic circuit".

Any computation at it is core consists of elemental operations of the form:

![alt text](/Images/image-22.png)

This step is know as "flattening" procedure, where we convert the original code, which may contain arbitrarily complex statements and expressions, into a sequence of statements that are represented as a single operation or x = y form. For example, consider the following computation and the result flattening:

![alt text](/Images/image-23.png)
![alt text](/Images/image-24.png)

The arithmetic circuit is similar to a boolean circuit. Here is an example of what an arithmetic circuit looks like for computing the example above:

![alt text](/Images/image-25.png)

The next step is to convert the above to a R1CS.

# R1CS

Once that we have the flattening of a function and the arithmetic circuit, our next step is to build what is called a Rank 1 Constraint System, or R1CS.

![alt text](/Images/image-26.png)

There is a natural way to transform the flattened version of our code to a R1CS. First we are going to have many constraints: one for each logic gate.We need to convert a logic gate into a (a,b,c) triple depending on what the operation is and whether the arguments are variables or numbers. Then, we define a vector, which will hold the state of our program, i.e. all variables which are used in the program. Each component of this vector will be one variable and the solution s will be an assignment to each variable.

Using the example same example as above, we have:

![alt text](/Images/image-27.png)
![alt text](/Images/image-28.png)
![alt text](/Images/image-29.png)
![alt text](/Images/image-30.png)
![alt text](/Images/image-31.png)
![alt text](/Images/image-32.png)

# Quadratic Arithmetic Program 

Once that we have our R1CS constraints, we need to transform into Quadratic Arithmetic Program using Lagrange Interpolation. Lagrange interpolating is the unique polynomial of lowest degree that interpolates a given set of data.

We will transform the system of 3 vectors (A, B, C) with length 4x6, into six groups of 3 degree polynomials, where evaluating the polynomials at each x coordinate represent a constraint. To understand how to do it, first let's see a simple example:

![alt text](/Images/image-33.png)
![alt text](/Images/image-34.png)
![alt text](/Images/image-35.png)
![alt text](/Images/image-36.png)

Now, the same strategy will apply to our R1CS. What we are gonna do is to take the first value of every vector a, apply lagrange interpolation to make a polynomial for it. We then will repeat the same process for vectors b and c. We will also apply the same methods on vector's second values, third values and so on.

![alt text](/Images/image-37.png)
![alt text](/Images/image-38.png)

What’s the point of this crazy transformation? The answer is that instead of checking the constraints in the R1CS individually, we can now check all of the constraints at the same time by doing the dot product check on the polynomials. 

# Checking the Quadratic Arithmetic Program 

Once that we have the QAP from our R1CS, we can chek all the constraints at the same time by doing the dot product check on the polynomials. Because in this case the dot product check is a series of additions and multiplications of polynomials, the result is itself going to be a polynomial. As follows:

![alt text](/Images/image-39.png)
![alt text](/Images/image-40.png)
![alt text](/Images/image-41.png)

And so we have the solution for the QAP. If we try to falsify any of the variables in the R1CS solution that we are deriving this QAP solution from — say, set the last one to 31 instead of 30, then we get a t polynomial that fails one of the checks, and furthermore $t$ would not be a multiple of $Z$; rather, dividing $t / Z$ would give a remainder of $[-5.0, 8.833, -4.5, 0.666]$.

As we notice, zk-SNARK permits proving computational statement, but they cannot be applied to the computational problem directly, the statement first needs to be converted into the right form, for example: a QAP. The nice thing about arithmetic circuits and QAP, is that although most ZK protocols have an inherent complexity that can be overwhelming, the design of arithmetic circuits is clear and neat.

Now we are capable to build a ZK proof, but we need a language for expressing the property you want to prove. For example, circom allow to express the arithmetic circui and using snarkjs we can generate the proof and the verifier.

There are many other language options, such as Cairo, Noir or RISC Zero.

