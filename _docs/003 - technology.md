---
title: "Technology Behind PACO"
permalink: /docs/technology/
excerpt: "Description regarding the technology used in PACO"
modified: 2016-09-30T15:54:02-04:00
redirect_from:
  - /theme-setup/
---

{% include base_path %}

### Design considerations
Our most important decision was the selection of the CPU we wanted to modify for the PACO core. The PACO group surveyed available CPU specifications and chose the [RISC V](https://riscv.org/) implementation [Rocket CPU](https://github.com/ucb-bar/rocket) because it offered

* a current open source CPU design
* a diverse and powerful set of open source tools (including spike, gdb, LLVM, binutils) 
* an active community developing it
* a novel, promising and apparently working language for hardware definition: [Chisel](https://chisel.eecs.berkeley.edu/)

### Description regarding the technology used in PACO

We tried to avoid reinventing the wheel, but wanted to build on open-source projects that are state of the art without adding unwanted complexity.

We built on:

* clang/LLVM for cross compilation
* GCC for linking and generation of executables from assembly
* QEMU for fast emulation of approximate applications
* mentioned above, the Rocket CPU for a current CPU design with an active community
    - Chisel for hardware specification
* Rocket SoC (System-on-Chip), providing us with a hardware environment for the CPU
* (non-open-source) Xilinx ISE for FPGA bitstream generation

Tools we added to Rocket to support the PACO system:

* QEMU, with it's inherent support for remote-gdb
* flashing tool to load applications to the FPGA
* a Lookup Table compiler capable of generating configuration of the Lookup table functional unit.
