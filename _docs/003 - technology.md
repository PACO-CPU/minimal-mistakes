---
title: "Technology Behind PACO"
permalink: /docs/technology/
excerpt: "Description regarding the technology used in PACO"
---

{% include base_path %}

## The CPU of Choice
Our most important decision was the selection of the CPU that we wanted to modify for the PACO core. The PACO group surveyed several available CPU specifications and chose a [RISC V](https://riscv.org/) implementation - the [Rocket CPU](https://github.com/ucb-bar/rocket). We decided to use the Rocket is because it offered

* a current open source CPU design
* a diverse and powerful set of open source tools (including Spike, gdb, LLVM, binutils) 
* an active community developing it
* a novel, promising and apparently working(!) language for hardware definition: [Chisel](https://chisel.eecs.berkeley.edu/)

## On the Technology used in PACO

We tried to avoid reinventing the wheel but wanted to build on open-source projects that are state of the art without adding unnecessary complexity.

We developed on:

* Clang/LLVM for cross compilation
* GCC for linking and generation of executables from assembly
* QEMU for fast emulation of approximate applications with its inherent support for remote-gdb
* Rocket CPU, as mentioned above, a current CPU design with an active community
    - Chisel for hardware specification
* Rocket SoC (System-on-Chip), providing us with a hardware environment for the CPU
* (non-open-source) Xilinx ISE for FPGA bitstream generation

Tools we added to Rocket to support the PACO system:

* Flashing tool to load applications to the FPGA
* Lookup Table Compiler capable of generating configuration of the Lookup table functional unit.
