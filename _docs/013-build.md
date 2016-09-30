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

The gcc compiler is needed to . Binutils consists of an assembler and a linker. The assembler converts assembly language to machine or object code. The linker  Riscv-test ..

#### 2 Clang and LLVM

Clang is . LLVM is a .

In order to set them up, run the following code.   

```bash
$ cd paco-env/riscv-tools-src/riscv-llvm
$ CC=gcc CXX=g++ ../configure --enable-targets=riscv --prefix=$RISCV
$ make -jN && make install
```  
Attention: remember to replace N with the number of threads you want to spawn.

This will install the clang compiler and the llvm tools into the `riscv-tools` directory.

#### explain what the second and the third command does. for example the flag --enable-targets does something ...

#### 3 LUT Compiler
If you decide to use our PACO's LUT to approximate functions, you will need our LUT compiler. The following code gets it installed into the `riscv-tools` directory:  

```bash
$ cd paco-env/riscv-tools-src/riscv-lut-compiler
$ make -jN && make install
```  
Attention: remember to replace N with the number of threads you want to spawn.

#### 4 Python Libaries

#### What python libraries? Why do we need the python libraries?

```bash
$ cd paco-env/riscv-tools-src/py
$ make install
```
This installs the python libraries into the `riscv-tools` directory.

#### 5 Rocket Libaries

#### Again what are the rocket libraries? Why do we need them?

This will install the RocketLib into the directory riscv-tools when you run it:
```bash
$ cd paco-env/rocket-soc/rocket_soc/lib
$ make -jN && make install
```  
Attention: remember to replace N with the number of threads you want to spawn.  

Congrats. From this point onwards your system should be prepared to run all the software tools of this
environment. Hopefully you didn't even break a sweat!

### Hardware setup

In case you possess an FPGA, the following setup would allow you to test the PACO Core on the device.
#### Should there be a particular series of FPGA, should the FPGA be plugged in
#### introduce what this process does?

#### Generating the CPU core

#### please dont use words without giving an introduction. 
#### What is the rocket-chip directory?
#### why should I generate the CPU? Im using the LUT :P
#### what is fsim?

To translate the Rocket-Chip, written in Chisel HDL, to a verilog description, run:
```bash
$ cd paco-env/rocket-chip/fsim
$ make -jN && make install
```

#### Synthesizing the system for FPGA installation
#### please introduce? why should I synthesize.. what is the use of it? 
#### You can't directly ask for the user to check the guide. Please go through the guide for a detailed description of something.

Please look into the User guide for more information. 

#### WHere is the conclusion of this page? and the link to the next page?
