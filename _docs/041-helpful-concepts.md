---
title: "similar projects"
permalink: /docs/similar-projects/
excerpt: "Links to helpful and related concepts"
bibliography: literature.bib
sidebar:
  nav: "links"  
---

{% include base_path %}

 At the level of micro-architecture, different techniques of approximation were adopted to build approximate processors. Three different approaches that achieved considerable speed-up or energy saving are introduced in this section.
 
 [Truffle](http://dl.acm.org/citation.cfm?id=2151008) was designed by a team from the University of Washington to exploit the concept of voltage scaling. It uses two pipelines supplied with two different levels of voltage for precise and approximate processing. Exexution of approximate arithemtic operation using a lower voltage supply resulted in more than 50% energy reduction for certain test benches.
  
 [Quora](http://www.microarch.org/micro46/files/paper1a1_slides.pdf) a project from Purdue University, used precision scaling with error monitoring and compensation to facilitate quality programmable execution in a vector architecture. LSBs of operands of arithmetic operations were neglected according to Quality prorammable instructions, where programmers define average or maximum of error allowed. Clock gating of logic slices responsible for operating on the neglected bits, and despite overhead introduced by the control and monitoring logic, achieved more than 2.5X savings for 7.5 % quality loss.

 [A third approach](http://dl.acm.org/citation.cfm?id=2457519) uses machine learning-based transformations to accelerate approximation-tolerant programs. Certain code regions are transformed from a von Neumann model to a neural model. A neural processing unit (NPU) is tightly coupled to the processor pipeline to permit profitable acceleration even when small regions of code are transformed. For a set of diverse applications, NPU acceleration provides whole-application speedup of 2.3X and energy savings of 3.0X on average with average quality loss of at most 9.6%.
