---
title: "Using an FPGA"
permalink: /docs/use-fpga/
excerpt: "Instructions on using an FPGA to test your application."
sidebar:
   nav: "tutorial"
---

{% include base_path %}

This guide gives you step by step instructions on how to run your application on an FPGA. We have used *virtix 6 ml605 FPGA Board* for testing our applications. To load and run the applications on FPGA a flash tool named as riscv-uart-flash is written in python script which communicates with FPGA using an UART port, this tool takes the binary loads it on FPGA and get the result back from FPGA . 

- If you are using the FPGA for the very first time, start from [here](#1 Installing Xilinx and starting ISE)
- If you already have Xilinx tools, start from [here](#2 Prerequisites)

** links don't work **

### 1) Installing Xilinx and starting ISE

- Xilinx ISE 14.7 as well as the Xilinx cable driver must be installed on your system. For more information regarding Xilinx ISE refer [here](https://en.wikipedia.org/wiki/Xilinx_ISE). A guide on installing both of them can be found [here](http://www.george-smart.co.uk/wiki/Xilinx_JTAG_Linux). This guide specifies the installation steps for linux user. Windows user can find all the information for installing and running ISE from [here](http://www.xilinx.com/support/documentation/sw_manuals/xilinx14_1/iil.pdf)

- Before starting the ISE, source the settings64.sh file and run the ise by running following commands:

```
$ source INSTALLATION_DIRECTORY/Xilinx/14.7/ISE_DS/settings64.sh

$ ise&
```
- This will start ISE in a GUI window

### 2) Prerequisites
For running programs on an FPGA, the following prerequisites are required:

- Install the PACO enviornment in your system, for further details refer to [User Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:setup-env)

- Synthesize PACO core on an FPGA. Details on how to synthesize the core is provided in the [User Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:synth-FPGA)

- Compile your program and generate a binary, for comilation steps please refer [Create your application](/paco-cpu/docs/create-application/).


Once the above prerequisites are met, you are ready to run your program on the FPGA.

### 3) Run Programs on FPGA
Your program can be loaded and run on the FPGA over the UART via the flashing tool by running your program :

```
$ riscv-uart-flash -i prog.elf -w

```

*riscv-uart-flash* is the flash tool obtained from the PACO enviornment ,prog.elf* is your program and the argument *-w* asks the flashing tool to continue executing until it receives a terminating signal from the program running on the FPGA.

To get data back from FPGA and writing data to FPGA, your application should use appropriate functions which does this, detailed description can be seen from [User Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:communicate-with-prog).
