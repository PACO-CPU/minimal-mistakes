---
title: "Using an FPGA"
permalink: /docs/use-fpga/
excerpt: "Instructions on using an FPGA to test your application."
modified: 2016-04-13T15:54:02-04:00
sidebar:
   nav: "tutorial"
---

{% include base_path %}

This guide gives you step by step instructions on how to run your application on FPGA.

- If you are using the FPGA for the very first time, start [here](#1 Installing Xilinx and starting ise)
- If you already have Xilinx tools, start [here](#2 Prerequisites)

### 1) Installing Xilinx and starting ise
- First of all you need to have Xilinx ISE 14.7 installed on your system as well as the
  Xilinx cable driver. A guide on installing both of them can be found [here](http://www.george-           smart.co.uk/wiki/Xilinx_JTAG_Linux). The ISE is installed in the path /opt/Xilinx/14.7/ISE DS.

- You start ISE by first sourcing the file settings64.sh and invoking
```c
$ source /opt/Xilinx/14.7/ISE_DS/settings64.sh
$ ise&
```
- This will start ISE in a GUI window

### 2) Prerequisites
For running programs on FPGA following prerequisites are needed:

- Synthesize PACO core on FPGA, details how to synthesize the core is provided in [User Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:synth-FPGA)
- Have a binary generated after compilation.

Once the above prerequistes are met you can get going with running your program with FPGA from [here](#3 Run Programs on FPGA)

### 3) Run Programs on FPGA
- Loading and running of a program on FPGA is done via flash tool over UART communiation. The program is loaded by running the following command
```c
$ riscv-uart-flash -i prog.elf -w
```
prog.elf is your program and the argument -w tells the flash tool to continue executing until it recieves a terminal signal from the program running on FPGA

- To write data or status information back from the program running on FPGA, use appropriate function from rocket-lib
 for more details regarding this refer to [User Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:communicate-with-prog)
 
 
