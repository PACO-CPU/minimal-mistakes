---
title: "Build"
permalink: /docs/build/
excerpt: "How to build the PACO toolchain before running"
sidebar:
    nav: "getting-started"
---

{% include base_path %}

## Building the toolchain

### Elements that need to be build

The toolchain consints of five parts they need to be build. These parts are:

1. RISCV-Toolchain
2. Clang and LLVM
3. LUT-Compiler
4. Python Libaries
5. Rocket Libaries

### Building process

#### Prerequisites

To install the toolchain make sure you have installed the following packages:
- libuuid for Clang and LLVM
- lua for the LUT Compiler


#### 1 RISCV-Toolchain

To build the RISCV-Toolchain just go to the source directory and run the build script. 
This will install the gcc compiler, binutils, and the riscv-tests into the directory riscv-
tools.

```bash
$ cd paco-env/riscv-tools-src
$ ./build.sh
```

#### 2 Clang and LLVM

Just run the following code. This will install the clang compiler and the llvm tools into the directory riscv-tools.

```bash
$ cd paco-env/riscv-tools-src/riscv-llvm
$ CC=gcc CXX=g++ ../configure --enable-targets=riscv --prefix=$RISCV
$ make -jN && make install
```
Attention: remember to replace N with the number of threads you want to spawn.

#### 3 LUT Compiler

To install the LUT compiler run this code, which will install the LUT compiler into the directory riscv-tools:

```bash
$ cd paco-env/riscv-tools-src/riscv-lut-compiler
$ make -jN && make install
```
Attention: remember to replace N with the number of threads you want to spawn.

#### 4 Python Libaries

This will install the python libs into the directory riscv-tools, if you run it:
```bash
$ cd paco-env/riscv-tools-src/py
$ make install
```

#### Rocket Libaries

This will install the RocketLib into the directory riscv-tools when you run it:
```bash
$ cd paco-env/rocket-soc/rocket_soc/lib
$ make -jN && make install
```
Attention: remember to replace N with the number of threads you want to spawn.


From this point on your system should be prepared to run all the software tools of this
environment.
