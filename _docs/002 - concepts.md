---
title: "Concepts"
permalink: /docs/concepts/
excerpt: "Description of the Idea/Concepts."
---

{% include base_path %}

## The PACO Idea
[Approximate computing](https://en.wikipedia.org/wiki/Approximate_computing) is a [steadily growing research topic](/paco-cpu/images/year_on_year_growth_approx.png) because other performance gains become [harder to reach](https://en.wikipedia.org/wiki/Dennard_scaling#Breakdown_of_Dennard_scaling_around_2006) while [applications](https://en.wikipedia.org/wiki/Computer_vision) [requiring](https://en.wikipedia.org/wiki/Image_processing) [less](https://en.wikipedia.org/wiki/Big_data) [than](https://en.wikipedia.org/wiki/Speech_recognition) [absolute](https://en.wikipedia.org/wiki/Machine_learning) [precision](https://en.wikipedia.org/wiki/Data_compression#Video) proliferate. The common goal is trading off accuracy or reliability for energy-savings, speed-up or computational latency reduction.

Approximate computing concepts range from 

* completely custom CPU core fabrics with error rate self-monitoring <small>over</small>
* under-volting or overclocking of circuits  <small>to</small>
* selectively ignoring cache coherency requirements.

A large majority of these approaches live an isolated existence because they target a very specific trade-off effect and are not based on a current general purpose CPU design. This isolated existence translates to often outdated and limited toolsets around the approximate computing platform.  

In contrast, the PACO group decided to **extend** a current **open general purpose CPU/ISA** by some promising **approximate functional units**.

## PACO Goal
To provide a platform that allows us and others to:

* learn about hardware approximation techniques by implementing them quickly
* measure effects on the quality of results and the speed-up acquired
* quickly compile approximate applications with a C/C++ compiler, allowing developers to evaluate results for their general purpose applications
* foster cooperation through open source hardware and software
* experiment with static approximation - the programmer/compiler has to try to predict precision requirements of individual operations and encode them within instructions. (In contrast to other approximate computing systems that try to regulate precision trade-offs at runtime and require quality metrics for every approximate calculation.)

## PACO Approximate Functional Units
These functional units

* reside in the execution stage of the pipeline 
* compute arithmetic functions in the most general sense
* behave deterministically, i.e. given the same inputs they always compute the same results 
* addressed using special approximate instructions.

<img src="/paco-cpu/images/PACO_core.png" alt="PACO core" width="400" style = "margin:30px">

To prove that it is possible to integrate different approximate functional units in the PACO core, we have implemented:

### An Approximate ALU  
The PACO Approximate ALU allows one to experiment with different degrees of approximation for approximate applications rather than providing energy savings or speedup as compared to the standard ALU. The ALU ignores a certain number of least significant bits of its inputs depending on the degree of approximation specified in the instruction.
An extension to C/C++ languages has also been created that allows both expected precision of inputs and minimum precision boundaries of outputs to be specified. The PACO compiler determines the most approximation possible without violating the output precision boundaries.
 
 <img src="/paco-cpu/images/results/alu/approx-alu-pipeline.svg" alt="Approx ALU" width="500" height= "300" style = "margin:30px">
 
The [Design Document](/paco-cpu/docs/design-doc.pdf#nameddest=sec:alu) elaborates on the concept behind approximation using the ALU in detail.
 
### A Lookup Table (LUT) 
The Lookup Table unit allows an application to replace complex arithmetical functions with a segment-wise linear approximation of it (see Fig.2). It is created within the CPU pipeline and takes **only one cycle** in the execution stage of the CPU. 

The LUT accepts inputs from upto three registers. It can be configured at runtime to evaluate upto 9 bits from these registers to determine the segment that has be interpolated. Then, some input bits can be multiplied with the segment's slope and finally an offset is added to calculate the result of the lookup instruction. The design of the Lookup Table is shown in Fig.3.
 
<img src="/paco-cpu/images/lut-function-linear.png" alt="lut-function" width="400" style = "margin:30px">

Fig.2: The Lookup Table unit approximates arithmetic functions within segments. In this case values within the segment are linearly interpolated.

<img src="/paco-cpu/images/results/lut/LUT-design.png" alt="LUT core" width="700" style = "margin:30px">

Fig.3. Design of LUT as a part of the pipeline.

To understand how LUT performs its magic refer to the [Design Document](/paco-cpu/docs/design-doc.pdf#nameddest=sec:lut).

## PACO Compiler Extensions

In order to create approximate applications, programmers must be able to control the level of approximation in their applications. The compiler must then be capable of translating this code to instructions that controls the approximate functional units. This not only requires special annotations but also new instructions.  

The PACO Toolchain consists of CLANG capable of handling special annotations, translating this C code into an Intermediate Representation(IR). This IR is consumed by LLVM to create assembly code. Binutils then converts assembly to maschine level representation that can be loaded and run on the FPGA or an emulator. Besides this, the special annotations are used to create a configuration for the LUT Core by the **LUT Compiler**. 

It is useful if the compiler can at least try to predict consequences of previous arithmetical operations on later ones. This prediction is of course limited because [small changes can have hard-to-predict effects in some functions](https://en.wikipedia.org/wiki/Numerical_stability).

An extensive description of the compiler can be found in the [Design Document](/paco-cpu/docs/design-doc.pdf#nameddest=sec:lang-instruction-approx).
