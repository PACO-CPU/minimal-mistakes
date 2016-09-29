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

### PACO Goals
Provide a platform that allows us and others to

* learn about approximations
* measure effects
* provide a working system that allows application developers to see results
* foster cooperation through open source hardware and software
* experiment with static approximation - the programmer/compiler has to try to predict precision requirements of individual operations and encode them in instructions. (In contrast with other approximate computing systems that try to regulate precision trade-offs at runtime, and need quality metrics for every approximate calculation.)

### Design considerations:
* 
* picked Rocket CPU as a basis, because it is under development, by an active community, open
* Chisel, why?

### Our hardware:
* approximate ALU:  
 The PACO approximate ALU does not provide energy savings or calculation speedup compared to the standard ALU, it just allows you to experiment with different degrees of approximation for approximate applications. We have created an extension of the C/C++ languages that allows you to specify both expected precision of inputs (maybe you already know that the real world gauge feeding that input has limited measurement precision) and minimum precision boundaries of outputs. The PACO compiler will then try to specify the most approximation possible without violating the output precision boundaries.
* Lookup Table (LUT) with interpolation within segments  
 The Lookup Table unit we created within the CPU pipeline allows an application to replace complex arithmetical functions with a segment-wise linear approximation of it **insert image of graph, with original function and segmentwise approximation**. It accepts input from up to three registers. The LUT can be configured at runtime to evaluate up to 9 bits from these registers to determine the segment it has to interpolate. When the segment is determined, some bits from the input can be multiplied with the slope for that segment, and finally an offset is added to calculate the result of the lookup instruction. A lookup instruction still only takes one cycle in the execution stage of the CPU.
