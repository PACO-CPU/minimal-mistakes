---
title: "Concepts"
permalink: /docs/concepts/
excerpt: "Description of the Idea/Concepts."
---

{% include base_path %}

### Description of the Idea and the Concepts behind PACO

* PACO is a CPU designed to calculate approximations
* hardware that has approximate instructions
* provide a research platform

### Goals:
* learn about approximations
* measure effects
* provide a working system that allows application developers to see results
* open source hardware and software
* functional approximation (...)
* static approximation - the programmer/compiler try to predict precision requirements of individual operations and encode them in instructions. (Some systems, like ... need a specification of result precision, and will try to evaluate the output quality and adjust approximation accordingly at runtime.)

### Design considerations:
* picked Rocket CPU as a basis, because it is under development, by an active community
* Chisel, why?

### Our hardware:
* approximate ALU:  
 The PACO approximate ALU does not provide energy savings or calculation speedup compared to the standard ALU, it just allows you to experiment with different degrees of approximation for approximate applications. We have created an extension of the C/C++ languages that allows you to specify both expected precision of inputs (maybe you already know that the real world gauge feeding that input has limited measurement precision) and minimum precision boundaries of outputs. The PACO compiler will then try to specify the most approximation possible without violating the output precision boundaries.
* Lookup Table (LUT) with interpolation within segments  
 The Lookup Table unit we created within the CPU pipeline allows an application to replace complex arithmetical functions with a segment-wise linear approximation of it **insert image of graph, with original function and segmentwise approximation**. It accepts input from up to three registers. The LUT can be configured at runtime to evaluate up to 9 bits from these registers to determine the segment it has to interpolate. When the segment is determined, some bits from the input can be multiplied with the slope for that segment, and finally an offset is added to calculate the result of the lookup instruction. A lookup instruction still only takes one cycle in the execution stage of the CPU.
