---
title: "Using an FPGA"
permalink: /docs/use-fpga/
excerpt: "Instructions on using an FPGA to test your application."
sidebar:
   nav: "tutorial"
---

{% include base_path %}

This guide gives you step by step instructions on how to run your application on an FPGA.

- If you are using the FPGA for the very first time, start from [here](#1 Installing Xilinx and starting ISE)
- If you already have Xilinx tools, start from [here](#2 Prerequisites)

** links don't work **

### 1) Installing Xilinx and starting ISE

** If it was my first time, i wouldn't know what xilinx and ise is and does .. introduce the process of testing before you write points**
** Why use xilinx and not any other tool. why this version? Which fpga have we tested in **

- Xilinx ISE 14.7 as well as the Xilinx cable driver must be installed on your system. A guide on installing both of them can be found [here](http://www.george-smart.co.uk/wiki/Xilinx_JTAG_Linux). 

- The ISE after installation can be found in the path /opt/Xilinx/14.7/ISE DS.
** depends on the OS **

- Before starting the ISE, source the settings64.sh file. For example:

```
$ source /opt/Xilinx/14.7/ISE_DS/settings64.sh

$ ise&
```
- This will start ISE in a GUI window

### 2) Prerequisites
For running programs on an FPGA, the following prerequisites are required:

- Synthesize PACO core on an FPGA. Details on how to synthesize the core is provided in the [User Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:synth-FPGA)

- Compile your program and generate a binary.

** where do i get the riscv-uart-flash tool from **

Once the above prerequisites are met, you are ready to run your program on the FPGA.

### 3) Run Programs on FPGA
Your program can be loaded and run on the FPGA over the UART via the flashing tool this way:

```
$ riscv-uart-flash -i prog.elf -w

```
** hopefully in the overview to this page, u introduce the UART as well **

*prog.elf* is your program and the argument *-w* asks the flashing tool to continue executing until it receives a terminating signal from the program running on the FPGA.

To write data or status information back from the program running on FPGA, use appropriate function from rocket-lib
 for more details regarding this refer to [User Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:communicate-with-prog)
 
** what is data or status information? please introduce before you state it. Don't include rocket-lib until you want to describe it ** 
