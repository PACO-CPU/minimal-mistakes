---
title: "Developer Guide"
permalink: /docs/developer-guide/
excerpt: "Developer Guide"
sidebar:
  nav: "documentation"
---

{% include base_path %}

The Developer Guide is the second part of the implementation document that details all the implementation work done by us. 
Reading this document is crucial to understanding how PACO works in order to modify or contribute to it.

### So go ahead and click [here](/paco-cpu/docs/impl-doc.pdf) to download the Implementation Document!


If you are not yet convinced and wish to read the gist of the contents before downloading the document(for whatever reason!) then go ahead...

The developer guide is divided into three main sections:
Environment, Compiler System and Approximate Hardware.

## Environment

It starts out with the description of our development environment giving an 
overview of its directory structure and the repositories used.  

In the subsequent sections, we explain the set of tools modified by us that are
part of the environment. In particular:  

1. RISC-V Tests: Pieces of code to test the correctness of the RISC-V implementation. This was extended by us to also test the approximate functional unit behavior.
2. Rocket Chip C Emulator: One of three targets for the generation of the Rocket Chip implementation of RISC-V. It consists of a cycle-accurate simulator written in C.
3. QEMU: A RISC-V target was written for the QEMU virtual machine system and can be used to simulate a RISC-V machine behaviorally. Currently it only supports the approximate ALU and not yet the LUT functional unit. 
4. UART debug interface / flashing tool: A python script written by us that interfaces with an FPGA instantiation of the Rocket SoC. It serves as an interface for downloading test programs and handling user input / program output.
5. Rocket SoC Runtime Library: A set of common code for use in developing programs to be run on an FPGA instantiation of the Rocket SoC. Included in the library is a set of template applications for use as starting points when writing new ones.

## Compiler System
The Compiler System section details the modifications made to Clang, LLVM and the GNU Binutils to support compilation of our extended C language and to generate binaries utilizing our custom opcodes. It also elaborates on our LUT compiler tool , which translates a function description written in C along with some translation-specific metadata, into a configuration bitstream to be used by our LUT hardware core.

## Approximate Hardware
The final chapter of the Developer Guide explains the changes done to the Rocket Chip and Rocket SoC to support our approximate hardware units.   

Rocket Chip houses the entire CPU core written in Chisel and extended with our approximate ALU and a black-box interface to our LUT core. This Chisel description is translated to Verilog before being inputted into the Rocket SoC
along with the LUT core itself (written in VHDL).   

The sections detail the implementation of the LUT hardware core and the approximate ALU.

#### Convinced now? Then go ahead and click [here](/paco-cpu/docs/impl-doc.pdf) to download the Implementation Document!
