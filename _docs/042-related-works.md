---
title: "Related Work"
permalink: /docs/related-work/
excerpt: "Related Works"
sidebar:
   nav: "links"
---

#### Introduce the section and its intention

#### remember that this is not a scientific paper. The language needs to more informal and exciting to read. Make it more personal please! 

### Related Work
Approximation techniques to make use of applications’ error resilience span the full stack
of software and hardware. Many efforts have been put into designing programming
languages and coding styles for approximate computing. EnerJ [15] uses type qualifiers
to declare data that may be subject to approximate computation. Loop perforation
provides a general technique to trade accuracy for performance by transforming loops to
execute a subset of their iterations [16]. A task-based programming model and runtime
system that exploit the observation that not all parts of a program are equally significant
for the accuracy of the end-result is introduced in [18].
 In  PACO we have not used any of the former , but rather added our own extensions to CLANG and LLVM. (a link to this may be)

Approximate adders and multipliers have also shown substantial advantages in improving delay, area and energy consumption. Different examples can be seen in [10], [9],
[7], [11], [23], [24], [25], [2] and [13]. Use of LUTs to approximate arithmetic functions has been around for a long time.
 Examples can be found in [22] and [17]. Stochastic search algorithms, in particular evolutionary algorithms, have shown to
 produce promising results in obtaining approximate circuits [14]. These concepts nevertheless were not used so far to design fully working approximate processors.  Approximate processors were built based on the concepts Clock gating, voltage scaling and neural networks, please check similar projects.

In addition to manual design techniques, design automation like automatic logic synthesis can be used to generate approximate circuits. [8] introduces transformations on
the Abstract Syntax Tree (AST) of the Hardware Description Language (HDL). [20]
proposes the substitution of signals with similar output such that the hardware generating one of the signals can be removed. [21] generates Approximate Don’t Cares into the
input such that traditional synthesis tools can exploit these Approximate Don’t Cares to
optimize the circuit using techniques of software synthesis originally not intended for approximate computing. 

#### Conclude 
