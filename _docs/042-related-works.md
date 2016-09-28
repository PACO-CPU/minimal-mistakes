---
title: "Related Work"
permalink: /docs/related-work/
excerpt: "Related Works"
sidebar:
   nav: "links"
---

PACO inroduced modifications to the hardware architecture to build an approximate processor, as well as extentions to the compiler to support approximate instructions. This section shows offers done in both fields related to our project. First, approximate arithemtic units and automatic logic synthesis tools to produce approximate circuits. Then, programming languages and compilers to support approximate hardware.

### Approximate hardware

Several modifications were done to adder and multiplier units on the circuit level, showing substantial advantages in improving delay, area and energy consumption. Different examples can be seen in [10], [9], [7], [11], [23], [24], [25], [2] and [13]. The mentioned examples lack , however, the possibility of scaling the error to different levels. The error introduced by the modified designs depends mainly on the value of the their inputs.  
Use of LUTs to approximate arithmetic functions, a concept directly related to our work, has been around for a long time. Examples can be found in [22] and [17]. Stochastic search algorithms, in particular evolutionary algorithms, have also shown to
produce promising results in obtaining approximate circuits [14].  
These concepts nevertheless were not used so far to design fully working approximate processors. Approximate processors built based on the concepts of Clock gating, voltage scaling and neural networks caqn be found here (link).

### Automatic logic generation

In addition to manual design techniques, design automation like automatic logic synthesis can be used to generate approximate circuits. [8] introduces transformations on the Abstract Syntax Tree (AST) of the Hardware Description Language (HDL). [20]
proposes the substitution of signals with similar output such that the hardware generating one of the signals can be removed. [21] generates Approximate Don’t Cares into the input such that traditional synthesis tools can exploit these Approximate Don’t Cares to
optimize the circuit using techniques of software synthesis originally not intended for approximate computing. 

### Programming languages and compiler support

 Many efforts have been put into designing programming languages and coding styles for approximate computing. EnerJ [15] uses type qualifiers to declare data that may be subject to approximate computation. Loop perforation
provides a general technique to trade accuracy for performance by transforming loops to
execute a subset of their iterations [16]. A task-based programming model and runtime
system that exploit the observation that not all parts of a program are equally significant
for the accuracy of the end-result is introduced in [18]. In  PACO we have not used any of the former , but rather added our own extensions to CLANG and LLVM (link). 

### References

[2] Robert H Dennard, Fritz H Gaensslen, Hwa-Nien Yu, V Leo Rideout, Ernest Bassous, and Andre R LeBlanc. Design of ion-implanted MOSFET’s with very small
physical dimensions. Proceedings of the IEEE, 87(4):668–678, 1999.  

[4] Hadi Esmaeilzadeh, Emily Blem, Ren´ee St Amant, Karthikeyan Sankaralingam,
and Doug Burger. Power challenges may end the multicore era. Communications
of the ACM, 56(2):93–102, 2013.  

[5] Hadi Esmaeilzadeh, Adrian Sampson, Luis Ceze, and Doug Burger. Architecture
support for disciplined approximate programming. In ACM SIGPLAN Notices,
volume 47, pages 301–312. ACM, 2012.  

[7] Vaibhav Gupta, Debabrata Mohapatra, Anand Raghunathan, and Kaushik Roy.
Low-power digital signal processing using approximate adders. Computer-Aided
Design of Integrated Circuits and Systems, IEEE Transactions on, 32(1):124–137,
2013.  

[8] Jie Han and Michael Orshansky. Approximate computing: An emerging paradigm
for energy-efficient design. In Test Symposium (ETS), 2013 18th IEEE European,
pages 1–6. IEEE, 2013.  

[9] Kumud Nepal Yueting Li R Iris and Bahar Sherief Reda. Automated high-level
synthesis of low power/area approximate computing circuits.  

[10] Andrew B Kahng and Seokhyeong Kang. Accuracy-configurable adder for approximate arithmetic designs. In Proceedings of the 49th Annual Design Automation
Conference, pages 820–825. ACM, 2012.  

[11] Parag Kulkarni, Puneet Gupta, and Milos Ercegovac. Trading accuracy for power
with an underdesigned multiplier architecture. In VLSI Design (VLSI Design),
2011 24th International Conference on, pages 346–351. IEEE, 2011.  

[13] Dong-U Lee, Altaf Abdul Gaffar, Oskar Mencer, and Wayne Luk. Optimizing
hardware function evaluation. Computers, IEEE Transactions on, 54(12):1520–
1531, 2005.  

[14] Jin Miao, Ku He, Andreas Gerstlauer, and Michael Orshansky. Modeling and synthesis of quality-energy optimal approximate adders. In Proceedings of the International Conference on Computer-Aided Design, pages 728–735. ACM, 2012.  

[15] Vojtech Mrazek, Zdenek Vasicek, and Lukas Sekanina. Evolutionary approximation
of software for embedded systems: Median function. In Proceedings of the Companion Publication of the 2015 on Genetic and Evolutionary Computation Conference,
pages 795–801. ACM, 2015.  

[16] Adrian Sampson, Andr´e Baixo, Benjamin Ransford, Thierry Moreau, Joshua Yip,
Luis Ceze, and Mark Oskin. Accept: A programmer-guided compiler framework
for practical approximate computing. University of Washington Technical Report
UW-CSE-15-01, 1, 2015.  

[17] Adrian Sampson, Werner Dietl, Emily Fortuna, Danushen Gnanapragasam, Luis
Ceze, and Dan Grossman. EnerJ: Approximate data types for safe and general lowpower computation. In ACM SIGPLAN Notices, volume 46, pages 164–174. ACM,
2011.  

[18] Stelios Sidiroglou-Douskos, Sasa Misailovic, Henry Hoffmann, and Martin Rinard.
Managing performance vs. accuracy trade-offs with loop perforation. In Proceedings of the 19th ACM SIGSOFT symposium and the 13th European conference on
Foundations of software engineering, pages 124–134. ACM, 2011.  

[19] Kanwaldeep Sobti, Lanping Deng, Chaitali Chakrabarti, Nikos Pitsianis, Xiaobai
Sun, Jungsub Kim, Prasanth Mangalagiri, K Irick, M Kandemir, and Vijaykrishnan
Narayanan. Efficient function evaluations with lookup tables for structured matrix
operations. In Signal Processing Systems, 2007 IEEE Workshop on, pages 463–468.
IEEE, 2007.  

[20] Vassilis Vassiliadis, Konstantinos Parasyris, Charalambos Chalios, Christos D
Antonopoulos, Spyros Lalis, Nikolaos Bellas, Hans Vandierendonck, and Dimitrios S
Nikolopoulos. A programming model and runtime system for significance-aware
energy-efficient computing. In Proceedings of the 20th ACM SIGPLAN Symposium
on Principles and Practice of Parallel Programming, pages 275–276. ACM, 2015.  

[21] Swagath Venkataramani, Vinay K Chippa, Srimat T Chakradhar, Kaushik Roy,
and Anand Raghunathan. Quality programmable vector processors for approximate
computing. In Proceedings of the 46th Annual IEEE/ACM International Symposium
on Microarchitecture, pages 1–12. ACM, 2013.  

[22] Swagath Venkataramani, Kaushik Roy, and Anand Raghunathan. Substitute-andsimplify: a unified design paradigm for approximate and quality configurable circuits. In Proceedings of the Conference on Design, Automation and Test in Europe,
pages 1367–1372. EDA Consortium, 2013.  

[23] Swagath Venkataramani, Amit Sabne, Vivek Kozhikkottu, Kaushik Roy, and Anand
Raghunathan. Salsa: systematic logic synthesis of approximate circuits. In Proceedings of the 49th Annual Design Automation Conference, pages 796–801. ACM,
2012.  

[24] O Vinyals, G Friedland, and N Mirghafori. Revisiting a basic function on current
cpus: a fast logarithm implementation with adjustable accuracy. International
Computer Science Institute, 2007.  

[25] Zhixi Yang, Abhishek Jain, Jinghang Liang, Jie Han, and Floriana Lombardi. Approximate xor/xnor-based adders for inexact computing. In Nanotechnology (IEEENANO), 2013 13th IEEE Conference on, pages 690–693. IEEE, 2013.  
