---
title: "Related Work"
permalink: /docs/related-work/
excerpt: "Related Works"
sidebar:
   nav: "links"
---

PACO introduced modifications to the hardware architecture to build an approximate processor, as well as extentions to the compiler to support approximate instructions. This section shows other work done in both fields related to our project. 

### Approximate Hardware

Several modifications were done to the adder and the multiplier units on the circuit level showing substantial advantages in improving delay, area and energy consumption. A comparison between different examples can be found [here](http://approximate.uni-paderborn.de/media/invitedTalks/JieHan-ACPaderborn2015.pdf). The mentioned examples however, lack the possibility of scaling the error to different levels. The error introduced by the modified designs depends mainly on the value of the their inputs.  

The use of Lookup Tables (LUT) to approximate arithmetic functions, a concept directly related to our work, has been around for a long time. An example of using a lookup table (LUT) approach for function evaluation can be found [here](http://www.public.asu.edu/~chaitali/jourpapers/tanor-tc.pdf).  

Stochastic search algorithms, in particular evolutionary algorithms, have also shown to
produce promising results in obtaining approximate circuits. [This paper](http://dl.acm.org/citation.cfm?id=2768416), for example, uses genetic programming-based improvement of non-functional properties of programs intended for low-cost microcontrollers.   

These concepts nevertheless, are not used so far to design fully working approximate processors. In [similar projects](https://paco-cpu.github.io/paco-cpu/docs/similar-projects/), we provide a short description about Approximate processors built based on the concepts of clock gating, voltage scaling and neural networks.

### Automatic Logic Generation

In addition to manual design techniques, design automation like automatic logic synthesis can be used to generate approximate circuits. [ABACUS](http://dl.acm.org/citation.cfm?id=2617115) introduces transformations on the Abstract Syntax Tree (AST) of the Hardware Description Language (HDL). [Substitute-and-Simplify](http://dl.acm.org/citation.cfm?id=2485615) proposes the substitution of signals with similar output such that the hardware generating one of the signals can be removed. [SALSA](http://dl.acm.org/citation.cfm?id=2228504) generates Approximate Don’t Cares into the input such that traditional synthesis tools can exploit these Approximate Don’t Cares to optimize the circuit using techniques of software synthesis originally not intended for approximate computing. 

### Programming Languages and Compiler Support

Several efforts have been put into designing programming languages and coding styles for approximate computing. [EnerJ] (http://sampa.cs.washington.edu/research/approximation/enerj.html) uses type qualifiers to declare data that may be subject to approximate computation. Loop perforation provides a general technique to trade accuracy for performance by transforming loops to execute a subset of their iterations, an example of using this technique for better energy performance is found [here] (http://dl.acm.org/citation.cfm?id=2025133). A task-based programming model and runtime system that exploit the observation that not all parts of a program are equally significant for the accuracy of the end-result is introduced [here](http://delivery.acm.org/10.1145/2690000/2688546/p275-vassiliadis.pdf?ip=131.234.42.90&id=2688546&acc=ACTIVE%20SERVICE&key=2BA2C432AB83DA15%2EFF86995C7D80A64D%2E4D4702B0C3E38B35%2E4D4702B0C3E38B35&CFID=673132489&CFTOKEN=69262487&__acm__=1475069518_463584b9e4294fad9427e857dec931dc). 

In  PACO we have not used any of the formerly discussed concepts rather added our own extensions to CLANG and LLVM. Check our [developer guide](https://paco-cpu.github.io/paco-cpu/docs/developer-guide/) for more details. 

** Add modifications discussed on Slack
