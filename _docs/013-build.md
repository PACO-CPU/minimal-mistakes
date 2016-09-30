---
title: "Building the Toolchain"
permalink: /docs/build/
excerpt: "How to build the PACO toolchain before running"
sidebar:
    nav: "getting-started"
---

{% include base_path %}
Now that you have the prerequisites mentioned in [getting -started](https://paco-cpu.github.io/paco-cpu/docs/getting-started/) installed and the project [downloaded](https://paco-cpu.github.io/paco-cpu/docs/download/), let's build the toolchain so that
you can use it.

#### Quick Build

You can build the entire project by using the install script.

```bash
$ cd paco-env
$ ./install.sh
```

#### Building the Toolchain Step-by-Step

If you have already built the entire project, you can go ahead and [run](https://paco-cpu.github.io/paco-cpu/docs/run/) the project. Unless of course if you want to learn about the parts of the toolchain that you just built, you can stick around. 

These are the parts of the toolchain that needs to be build if you consider to do it manually:

1. RISCV-Toolchain
2. Clang and LLVM
3. LUT-Compiler
4. Python Libaries
5. Rocket Libaries

#### 1 RISCV-Toolchain

The RISCV-Toolchain consists of the gcc compiler, binutils and the riscv-tests and these
need to be installed into the `paco-env/riscv-tools` tools directory.

To do so, go to the `riscv-tools-src` directory and run the build script.  

```bash
$ cd paco-env/riscv-tools-src
$ ./build.sh
```  

The gcc compiler can be used to compile non approximate code. As well some libaries of it are needed to run GNU-Binutils. Binutils consists of an assembler and a linker. The assembler converts assembly language to machine or object code. The linker finally links the binary output. Riscv-test consists test programs to make sure the rocket core has been implemented correct. 

#### 2 Clang and LLVM

Clang is is a compiler front end for the programming languages C, C++ and many others. LLVM is a collection of modular and reusable compiler and toolchain technologies used to develop compiler front ends and back ends. 

In order to set them up, run the following code.   

```bash
$ cd paco-env/riscv-tools-src/riscv-llvm
$ CC=gcc CXX=g++ ../configure --enable-targets=riscv --prefix=$RISCV
$ make -jN && make install
```  
Attention: remember to replace N with the number of threads you want to spawn.

This will install the clang compiler and the llvm tools into the `riscv-tools` directory.
The flags of the configure command sets the make configuration that the code is only build for target RISCV. This prevents building for other targets which are not needed and results in taking less disk space and speeding up the building process a bit.

#### 3 LUT Compiler
If you decide to use our PACO's LUT to approximate functions, you will need our LUT compiler. The following code gets it installed into the `riscv-tools` directory:  

```bash
$ cd paco-env/riscv-tools-src/riscv-lut-compiler
$ make -jN && make install
```  
Attention: remember to replace N with the number of threads you want to spawn.

#### 4 Python Libaries

Python is used to communicate with the core via the UART interface for flashing and runtime diagnose of results. To install the python libaries use the following command:

```bash
$ cd paco-env/riscv-tools-src/py
$ make install
```
This installs the python libraries into the `riscv-tools` directory.

#### 5 Rocket Libaries

#### Again what are the rocket libraries? Why do we need them?

The RocketLib is used to communicate from your program running on the FPGA to the machine attached. This will install the RocketLib into the directory riscv-tools when you run it:

```bash
$ cd paco-env/rocket-soc/rocket_soc/lib
$ make -jN && make install
```  
Attention: remember to replace N with the number of threads you want to spawn.  

Congrats. From this point onwards your system should be prepared to run all the software tools of this
environment. Hopefully you didn't even break a sweat!

### Hardware setup

If you are interested in running code on either the approximate ALU or the approximate LUT, you will need to download the PACO core to an FPGA. The following setup would allow you to synthesize and download the PACO Core on a Xilinx Virtex-6 board. You need to have Xilinx ISE 14.7 installed on your system as well as the Xilinx cable driver. A guide on installing both of them can be found [here](http://www.george-smart.co.uk/wiki/Xilinx_JTAG_Linux). You start ISE by first sourcing the file settings64.sh and invoking:

```bash
$ source /opt/Xilinx/14.7/ISE_DS/settings64.sh
$ ise&
```  

Attention: The previous step assumes that ISE is installed in the path /opt/Xilinx/14.7/ISE DS, If not please change the path in the first command.

This will start ISE in a GUI window. From here you have to select ”File - Open
Project” and open the Rocket-SoC project file called rocket soc.xise. If you finished the previous steps successfully, you should find the file under `paco-env/rocket-soc/rocket_soc/prj/ml605`. If a window pops
up stating the file ”Memo.vhd” cannot be found, you can click the checkbox ”Remove
unspecified files from project” and proceed. Once you open the project click generate
programming file, which starts the synthesis process. Once the process is finished, a
bitstream file is created called rocket soc.bit.
To flash this bitstream onto you FPGA you have to start impact by either clicking on
”Configure Target Device” in ISE or run:

```bash
$ source /opt/Xilinx/14.7/ISE_DS/settings64.sh
$ impact&
```

In impact first click on ”No” or ”Cancel” on every popup window. Make sure your FPGA board is plugged in, then doubleclick on
”Boundary Scan”, press ”Ctrl-I” to initalize your cable to the FPGA and click ”No” and
”Cancel” on the two popups. Rightclick on the chip symbol labeled ”xc6vlx240t”, select
”Assign new configuration File...”, and select the file rocket soc.bit. Finally rightclick
the chip symbol again and select ”Program”, then ”Ok” and after a loading bar a blue
box should appear saying ”Program succeeded”.

If you have reached so far, then you have everything ready to use our PACO core. Proceed to the next page to know how to [run](https://paco-cpu.github.io/paco-cpu/docs/run/) code on it.

