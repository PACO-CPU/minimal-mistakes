---
title: "Using an FPGA"
permalink: /docs/use-fpga/
excerpt: "Instructions on using an FPGA to test your application."
sidebar:
   nav: "tutorial"
---

{% include base_path %}

This guide gives you step by step instructions on how to run your application on an FPGA. 

In order to load and run your applications on an FPGA, a flashing tool named as **riscv-uart-flash** is written in **where can I find it?**. This tool communicates with the FPGA via an UART port, loads the binary and obtains the result back from the FPGA. 

** introduce the process of synthesis using Xilinx ISE also in a line, the way flashing tool was introduced before**

- If you are using the FPGA for the very first time, start from [here](#1 Installing Xilinx and starting ISE)
- If you already have Xilinx tools, start from [here](#2 Prerequisites)

** links don't work **

### 1) Installing Xilinx and starting ISE

- [Xilinx ISE 14.7](https://en.wikipedia.org/wiki/Xilinx_ISE) as well as the Xilinx cable driver must be installed on your system. A guide on installing both of them can be found [here](http://www.george-smart.co.uk/wiki/Xilinx_JTAG_Linux). 

- Before starting the ISE, source the settings64.sh file and run the ise by running following commands:

```
$ source INSTALLATION_DIRECTORY/Xilinx/14.7/ISE_DS/settings64.sh

$ ise&
```
- This will start the ISE in a GUI window

### 2) Prerequisites
For running programs on an FPGA, the following prerequisites are required:

- Install the PACO environment in your system; follow the Getting Started Guide. 

- Synthesize PACO core on an FPGA. Details on this is provided in the [User Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:synth-FPGA)

- Compile your program and generate a binary; refer to [Create your application](/paco-cpu/docs/create-application/) guide.


Once the above prerequisites are met, you are ready to run your program on the FPGA.

### 3) Run Programs on FPGA
Your program can be loaded and run on the FPGA over the UART via the flashing tool this way :

```
$ riscv-uart-flash -i prog.elf -w

```

wherein **riscv-uart-flash** is the flashing tool obtained from the PACO environment, **prog.elf** is your program and the argument **-w** asks the flashing tool to continue executing until it receives a terminating signal from the program running on the FPGA.

In order to obtain the data back from the FPGA and writing data into FPGA, your application should use appropriate functions **name the functions atleast **. For a detailed description follow the [User Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:communicate-with-prog).
