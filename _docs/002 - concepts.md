---
title: "Concepts"
permalink: /docs/concepts/
excerpt: "Description of the Idea/Concepts."
---

{% include base_path %}

### The PACO idea
[Approximate computing](https://en.wikipedia.org/wiki/Approximate_computing) is a [steadily growing research topic](/paco-cpu/docs/related-work/) because other performance gains become [harder to reach](https://en.wikipedia.org/wiki/Dennard_scaling#Breakdown_of_Dennard_scaling_around_2006) while [applications](https://en.wikipedia.org/wiki/Computer_vision) [requiring](https://en.wikipedia.org/wiki/Image_processing) [less](https://en.wikipedia.org/wiki/Big_data) [than](https://en.wikipedia.org/wiki/Speech_recognition) [absolute](https://en.wikipedia.org/wiki/Machine_learning) [precision](https://en.wikipedia.org/wiki/Data_compression#Video) proliferate. Common goal is trading off accuracy or reliability for energy-savings, speed-up or computation latency reduction.

Approximate computing concepts range from 

* completely custom CPU core fabrics with error rate self-monitoring over
* under-volting or overclocking of circuits to 
* selectively ignoring cache coherency requirements.

A large majority of these approaches live an isolated existence, because they target a very specific trade-off effect and are not based on a current general purpose CPU design. This isolated existence translates to often outdated and limited toolsets around the approximate computing platform.  
In contrast, the PACO group decided to **extend** a current **open general purpose CPU/ISA** by some promising approximate functional units.

These **functional units**

* reside in the execution stage of the pipeline, 
* compute arithmetic functions in the most general sense,
* behave deterministically (i.e. given the same inputs they always compute the same results) and
* are addressed with special approximate instructions.

### PACO Goal
Provide a platform that allows us and others to

* learn about hardware approximation techniques by implementing them quickly
* measure effects on result quality and speed-up
* quickly compile approximate applications with a C/C++ compiler, allowing developers to evaluate results for their general purpose applications
* foster cooperation through open source hardware and software
* experiment with static approximation - the programmer/compiler has to try to predict precision requirements of individual operations and encode them in instructions. (In contrast with other approximate computing systems that try to regulate precision trade-offs at runtime, and need quality metrics for every approximate calculation.)

### PACO approximate functional units
To provide proof that it possible to integrate very different approximate functional units in the PACO core, we have implemented:

* an approximate ALU:  
 The PACO approximate ALU does not provide energy savings or calculation speedup compared to the standard ALU, it just allows you to experiment with different degrees of approximation for approximate applications: Depending on the degree of approximation specified in the instruction, the ALU ignores a certain number of least significant bits of its inputs.  
 We have also created an extension of the C/C++ languages that allows you to specify both expected precision of inputs (maybe you already know that the real world gauge feeding that input has limited measurement precision) and minimum precision boundaries of outputs. The PACO compiler will then try to specify the most approximation possible without violating the output precision boundaries.
* a Lookup Table (LUT) interpolating functions within segments of the domain  
 The Lookup Table unit we created within the CPU pipeline allows an application to replace complex arithmetical functions with a segment-wise linear approximation of it (see Fig.2). It accepts input from up to three registers. The LUT can be configured at runtime to evaluate up to 9 bits from these registers to determine the segment it has to interpolate. When the segment is determined, some bits from the input can be multiplied with the slope for that segment, and finally an offset is added to calculate the result of the lookup instruction. A lookup instruction still only takes one cycle in the execution stage of the CPU.


<img src="/paco-cpu/images/lut-function-linear.png" alt="lut-function" width="400">

Fig.2: The Lookup Table unit approximates arithmetic functions within segments. In this case values within the segment are linearly interpolated.
