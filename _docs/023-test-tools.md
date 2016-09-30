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

** What about writing custom tests? Where are the test files present and how to read the results from the emulator?**

More details about the C Emulator are provided in the [User Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:ug-c-emulator) and
[Developer Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:c-emulator). 

## QEMU

[QEMU](http://qemu.org/) allows you to test your approximate programs for logical correctness without
having to specify hardware but it cannot be generated from your hardware specification, giving no guarantee for the correctness of hardware specifications. To simulate your program using QEMU follow the steps:
** The above description is unclear **
** So where do I find qemu. Is it a part of our repository? **

- First build the qemu using the following commands

```
$ mkdir qemu-build
$ cd qemu-build
$../qemu/configure --target-list=riscv-softmmu --enable-debug \
--python=/usr/bin/python2
$ make

```

- Once you have build qemu, set up your system and include Berkley boot loader, linux kernel and initrd(initial ram disk)
 along with your program. For more details how to build these components refer to [Developer Guide](/paco-cpu/docs/impl- doc.pdf#nameddest=sec:env-build-vm).
 
- Once all the components are prepared add your program in the initrd. Let us call the test-program as *test-program*. Insert test-program into the initrd by mounting it first and then copying the file over as follows:
 
```
$ mkdir -p rootfs
$ mount -o loop rootfs.ext2 rootfs
$ cp test-program rootfs/root/
$ umount rootfs

```
 ** So the test program is the annotated C program? **
 
- After adding your program in the initrd, it can be tested through the virtual machine. To execute it, run the following:
 
```
 $ qemu-system-riscv -kernel bbl -append vmlinux \
   -drive file=rootfs.ext2, format=raw -nographic
   
```
 
- Now this will boot the virtual machine. Eventually a user name is requested to be logged in. The test program can then be run by:
 
```
$ /root/test-program
 
```
** How to read the results in qemu? **

** Conclude **
