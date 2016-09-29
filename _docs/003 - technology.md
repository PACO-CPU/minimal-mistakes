---
title: "Technology Behind PACO"
permalink: /docs/technology/
excerpt: "Description regarding the technology used in PACO"
modified: 2016-04-13T15:54:02-04:00
redirect_from:
  - /theme-setup/
---

{% include base_path %}

### Description regarding the technology used in PACO

We tried to avoid reinventing the wheel, but wanted to build on open-source projects that are state of the art without adding unwanted complexity.

We built on:
* clang/LLVM for cross compilation
* GCC for linking and generation of executables from assembly
* QEMU for fast emulation of approximate applications
* the Rocket CPU for a current CPU design with an active community
    - Chisel for hardware specification
* (non-open-source) Xilinx ISE for FPGA bitstream generation
* **(more)**

Additional tools supported by the PACO system:
* remote-gdb for QEMU
* flashing tool to load applications to the FPGA
* **(more)**
