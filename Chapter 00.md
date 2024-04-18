# Introduction

In this chapter, we introduce the concept of what Zero-Knowledge proof (ZKP) are. We intended to provide a comprehensive introduction to the mathematical foundations and implementatios of these proof systems, aimed at individuals with limited prior exposure to this area of research.

A ZKP is a protocol that enables one party, called the prover, to convince another, the verifier, that a statement is true without revealing any information beyond the veracity of the statement. The main idea behind this concept is to prove possession of knowledge without revealing it. 

Let's use the most common example, Alice and Bob are racing to find Waldo. Alice claim that she already know where waldo is, she wants to proof this without reveal the answer to Bob, so she use a ZK proof. 

![alt text](/Images/image.png)

Usually, we think that a ZKP is equal to privacy, but this is a misconception; they are equal to honest computation. 

There are three properties that every ZKP must satisfy: completeness, soundness and zero-knowledge.

- Completeness: If the statement is really true and both users follow the rules properly, then the verifier would be convinced without any artificial help.
- Soundness: If the statement is false, the verifier would not be convinced in any scenario.
- Zero-knowledge: the verifier in every case would not know any more information.

ZKP can be interactive and non-interactive.

- Interactive: in this form, the prover, had to perform a serious of actions to convince the verifier of a certain fact. However, there is one drawback to this technique: The proof is limited and transferability, this means that we have to repeat the entire process if we want to convince a new verifier.
- Non - interactive. Allow you to deliver a proof that anyone can verify by themselves, i.e, ZK - SNARK (Succinct Non-interactive Arguments of Knowledge) is used by some cryptocurrencies to protect the privacy of their users.

In this chapter we understand the basis fo ZKP, to go more in deep with this protocol, in the following chapters we are going to learn some mathematics and cryptography concepts. 