---
title: "Design Document"
permalink: /docs/design-document/
excerpt: "Design Document"
sidebar:
  nav: "documentation"
---

{% include base_path %}

The Design Document delivers an understanding of the idea behind the implementation work done in this project
group.   

If you are curious as to how many apples fell on our heads before we came to the PACO realization, find out *[here](/paco-cpu/docs/design-doc.pdf)*.

The contents of the document are as follows:

- Introduction to the components designed
- Approximation Techniques
  - The Approximate ALU unit as a swag modification of the already implemented precise ALU in the Rocket Chip (an implementation of the RISCV processor architecture). We make use of bypass registers to omit changes in the least
significant bits of the ALU inputs, thereby reducing dynamic power consumption at the cost of accuracy.
  - The Lookup-Table unit as a *realization* of a configurable piece-wise affine linear function computed within the processor pipeline. This core implements functional approximation of a high-level function in one or more inputs and
a single output.
- Compiler/Language Modifications - the application programmer's interface to our approximation units. 
  - An approximate decorator following the syntax of a parameterized C/C++ preprocessor macro. It can annotate C declarations with an arbitrary set of key-values that are understood by the compiler and 
translated to utilize approximation units on the constructs being decorated.   
  - Changes to Clang/LLVM and the GNU Binutils to effect the realization of our language extensions.   
  - LUT Configuration Generator or LUT Compiler - a piece of software to generate configuration 
bitstreams for our LUT units that is loaded at startup time of applications using respective LUT units. It inputs a function written in C, a set of key-value pairs (e.g. extracted from approximate decorators) as well as
an optional architecture file specifying the parameters of the LUT core in question.
  
I know, things got serious quickly. The plot thickens however, this was not the original design. We modified the design document to confuse you further. Actually not, there were problems that arose when we implemented the design and we had to modify it [:embarrassed].

So click *[here](/paco-cpu/docs/design-doc-pre.pdf)* for the original version of the document.

### The list of not-so-embarrassing changes:

### Usage of DMA-based LUT configuration
Originally we had envisioned the option of configuring LUT units by 
memory-mapping its configuration registers to the Rocket SoC memory bus.   
As most of the configuration bitstream consisted of registers as opposed to
random-addressable memory it showed to be more realistic to use a single 
instruction to load configuration data word-by-word.

### LUT-related instruction set changes
The original instruction set extension for the LUT unit consisted of merely
a load and an execute instruction.   
This was changed for a number of reasons:

1. Against our initial design, we decided to allow more than a single word
of input data to be used by the LUT unit. This resulted in the addition of a
LUTE3 instruction that would transmit three registers at a time. We later
figured out that this behavior would encompass significant changes to the 
processor pipeline and we degraded this to a pseudo-instruction. To allow
three (or more) input registers to be used by the LUT core we added internal
registers to the LUT core, one or two of which can be modified at a time using
the LUTE or the newly added LUTE2 instruction. To prevent running computations
on incomplete sets of input data, the LUTW and LUTW2 instructions were added
at the same time to allow writing to internal registers without running 
computations.

2. During the fine-grained design of the LUT core it became apparent that we
would like to have information about the internal state of a LUT core for
debugging and testing purposes. For this purpose the LUT core was given error
states to be reached by incorrect configuration or premature execution. To
read this error state and receive feedback on the configuration status of a
LUT core, the LUTS instruction was created.

3. To recover from an error state or to load a new configuration bitstream (
possibly without completing a previous configuration operation), the LUTL
instruction was complemented with another bit effecting a reset of the LUT
control state, setting back the LUT core to its initial, unconfigured, state.

### Key-value renaming
During the implementation of the high-level compiler components we learned that
the processing of pragma directives in Clang uses the same Lexer as is used
for the actual C/C++ code. Thus using hyphens in identifiers resulted in
needless complexity for the compiler modification. We thus replaced hyphens
with underscores. This also affects key-value names used by the LUT compiler
as they occur as identifiers in approximate decorators.

### Use of LLVM intrinsics
The discovery of intrinsics used in LLVM offered a very simple and elegant way
to add instructions to the LLVM backend. As we discovered this functionality
we decided to re-design the LLVM IR extension to make use of these intrinsics.
This affected both ALU and LUT related parts of the LLVM IR.

### LUT Compiler input format adjustments
To improve flexibility in the LUT compiler input format with respect to by-hand
editing and readability, section separators were changed to lines containing
two percent signs. This is also a tribute to the the Flex scanner generator
tool used in the implementation of the LUT compiler tool.   
To further improve flexibility, another section was added that explicitly
designates the signature of the target function. This serves to allow forward
declarations to be used in the C code for the target function and to make use
of type coercion.

### LUT Compiler intermediate format adjustments
During the fine-grained design of the LUT Compiler program an ambiguity was
introduced in the intermediate format that resulted from segments being 
specified in input space. To solve this, segments are now specified in domain
space and the domain itself is defined by a dedicated statement in the
LUT compiler intermediate format.

### LUT Compiler strategy changes
Implementation-specific details of the LUT segmentation strategies resulted in
weights to be used by default, negating the need for strategies explicitly
exploiting weights.   
Concurring with the renaming of key-values, the min-error strategy was renamed
to linear and the step approximation strategy was added.

I hope you had a laugh. Now go on and read the [Glossary](). 
