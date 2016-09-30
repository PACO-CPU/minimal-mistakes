---
title: "Testing using Tools"
permalink: /docs/test-tools/
excerpt: "Testing using tools such as the C Emulator"
sidebar: 
    nav: "tutorial"
---

{% include base_path %}

This section guides you on testing your applications using several tools. 

## C Emulator
The C Emulator enables you to test your hardware for logical correctness without synthesizing it in a virtual environment. It uses Chisel code that describes the Rocket core and is cycle-accurate. 

To get the emulator working follow these steps:

- In the rocket-chip/emulator directory, run

```
$  make CONFIG=PACOConfigCPP -jN
```

- You can run tests on the emulator by calling:

```
$ make CONFIG=PACOCOnfigCPP -jN run-asm-tests
```

To write your own test to the testsuite, look into the [riscv-tests](https://github.com/PACO-CPU/riscv-tests). A good example to start with is [add_approx.S](https://github.com/PACO-CPU/riscv-tests/blob/master/isa/rv64ui/add_approx.S). Once you added your own file, you need to rebuild the tests and add your addition to the [Makefrag](https://github.com/PACO-CPU/riscv-tests/blob/4019a9c000d7471cc5dca149fed206aae88fe35f/isa/rv64ui/Makefrag) of the same folder.

**Note:** The C Emulator should only be used for the approximate ALU.

More details about the C Emulator are provided in the [User Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:ug-c-emulator) and
[Developer Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:c-emulator). 

## QEMU

[QEMU](http://qemu.org/) allows you to test your approximate programs for logical correctness without
having to specify hardware, just functional behaviour. Thus it cannot be generated from your hardware specification, giving no guarantee for the correctness of the hardware specification. The repository of QEMU for PACO can be found [here](https://github.com/PACO-CPU/qemu.git). 
To simulate your program using QEMU follow the steps:

- First build the qemu using the following commands

```sh
$ mkdir qemu-build
$ cd qemu-build
$../qemu/configure --target-list=riscv-softmmu --enable-debug --python=/usr/bin/python2
$ make
```

- Once you have build qemu, you can create an application using the approximate ALU (e.g. [Gaussian Blur](paco-cpu/docs/create-application/#3-approximate-alu-guide)) to be run in QEMU. Make sure you compile it with a linux compiler version of GCC. The program can be any [annotated](/paco-cpu/docs/annotate/) program using the approximate ALU. **Note:** You can use the glibc method common in any linux system, e.g. "printf" for I/O.

- Set up your system and include Berkley boot loader (bbl), linux kernel and initrd(initial ram disk)
 along with your program. For more details how to build these components refer to [Developer Guide](/paco-cpu/docs/impl- doc.pdf#nameddest=sec:env-build-vm). A prebuild version of bbl, linux kernel, and initrd can be found here:[bbl](https://github.com/PACO-CPU/qemu/raw/master/images/bbl), [linux](https://github.com/PACO-CPU/qemu/raw/master/images/vmlinux), and [initrd](https://github.com/PACO-CPU/qemu/raw/master/images/rootfs.ext2).
 
- Once all the components are prepared add your program in the initrd. Let us call the test-program as *test-program*. Insert test-program into the initrd by mounting it first and then copying the file over as follows:

```sh
$ mkdir -p rootfs
$ mount -o loop rootfs.ext2 rootfs
$ cp test-program rootfs/root/
$ umount rootfs
```
 
- After adding your program in the initrd, it can be tested through the virtual machine. To execute it, run the following:
 
```
 $ qemu-system-riscv -kernel bbl -append vmlinux -drive file=rootfs.ext2, format=raw -nographic
   
```
 
- Now this will boot the virtual machine. Eventually a user name is requested to be logged in. The test program can then be run by:
 
```
$ /root/test-program
 
```

**Note:** The prebuilt images for QEMU contain a systemtest for the approximate ALU. You can start it by running

```sh
$ /root/alu_verify.elf
```

** Conclude **
