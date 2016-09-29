---
title: "Developer Guide"
permalink: /docs/developer-guide/
excerpt: "Developer Guide"
sidebar:
  nav: "documentation"
---

{% include base_path %}


The Developer Guide is the second part of the
[implementation document]({{site.url}}/docs/impl-doc.pdf). It details all the
implementation work done by us. It is divided into three main areas:
Environment, Compiler System and Approximate Hardware.

## Environment

It starts out with the description of our development environment giving an 
overview of its directory structure and repositories used.  

In the subsequent sections we explain the set of tools used by us that are
part of the environment. In particular:   
1. RISC-V tests: Pieces of code to be run by a RISC-V implementation testing
the correctness of its implementation. This was extended by us to also test
for approximate functional unit behavior.
2. Rocket chip C emulator: One of three targets for the generation of the 
Rocket Chip implementation of RISC-V. It consists of a cycle-accurate 
simulator written in C.
3. QEMU: A RISC-V target was written for the QEMU virtual machine system and
can be used to simulate a RISC-V machine behaviorally. Currently it only 
supports the approximate ALU and not the LUT functional unit.
4. UART debug interface / flashing tool: A python script written by us that
interfaces with an FPGA instantiation of the Rocket SoC. It serves as an
interface for downloading test programs and handling user input / program 
output.
5. Rocket SoC Runtime Library: A set of common code for use in developing
programs to be run on an FPGA instantiation of the Rocket SoC. Included in
the library is a set of template applications for use as starting points when
writing new ones.

## Compiler System
The Compiler System section details modifications done to Clang, LLVM and the
GNU Binutils to support compilation of our extended C language and generating
binaries utilizing our custom opcodes.   
It also elaborates on the from-scratch implementation of the LUT compiler tool
which translates a target function description written in C and complemented
with translation-specific metadata into a configuration bitstream to be used by
our LUT hardware core.

## Approximate Hardware
The final chapter of the Developer Guide explains changes done to the
Rocket Chip and Rocket SoC to support our approximate hardware units.   
In this, the Rocket Chip houses the entire CPU core extended with our 
approximate ALU and a black-box interface to our LUT core. The Chisel 
description is translated to Verilog before being inputted into the Rocket SoC
along with the LUT core itself.   

After the changes to the Chisel code, subsequent sections detail the 
implementation of the LUT hardware core and the approximate ALU itself.

