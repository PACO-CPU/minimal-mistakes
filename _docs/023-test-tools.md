---
title: "Testing using Tools"
permalink: /docs/test-tools/
excerpt: "Testing using tools such as the C Emulator"
modified: 2016-04-27T10:35:05-04:00
sidebar: 
    nav: "tutorial"
---

{% include base_path %}

This section guides you to test your applications using different tools. It is divided into two sections based on the tools you wish to use. 
Lets Get started

## 1) Decide on the tool you want to use
- C Emulator start [here](#2-C-Emulator)
- QEMU start [here](#3-QEMU)

## 2) C Emulator
The C Emulator allows you to run programs on a virtual version of the Rocket CPU. It is generated from the actual Chisel code describing the
Rocket CPU core and is cycle-accurate. This means it allows you to test your hardware
for logical correctness without synthesizing it and benchmark your applications much
more precisely in a virtual environment. For more information about C Emulator refer to [Developer Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:c-emulator).

To get the emulator working follow below steps:
- The emulator must be generated from the chisel code, for doing this go to rocket-chip/emulator directory and call

```

$  make CONFIG=PACOConfigCPP -jN

```

Once this works, then you can test the emulator by calling:

```

$ make CONFIG=PACOCOnfigCPP -jN run-asm-tests

```

More details about C Emulator are provided in [User Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:ug-c-emulator) and
[Developer Guide](/paco-cpu/docs/impl-doc.pdf#nameddest=sec:c-emulator)

## 3) QEMU

[QEMU](http://qemu.org/)allows you to test your approximate programs for logical correctness without
having to specify hardware but it cannot be generated from your hardware specification, giving no guarantee for the correctness of hardware specifications. To simulate your program using QEMU follow following steps:

- First build the qemu using following commands

```
$ mkdir qemu-build
$ cd qemu-build
$../qemu/configure --target-list=riscv-softmmu --enable-debug \
--python=/usr/bin/python2
$ make

```

- Once you have build qemu, set up your system and include Berkley boot loader, linux kernel and initrd(initial ram disk)
 along with your program. For more details how to build these components refer to [Developer Guide](/paco-cpu/docs/impl- doc.pdf#nameddest=sec:env-build-vm).
 
- Once all the components are prepared add your program in the initrd. Lwt us call the test-program as *test-program*. Insert test-program into the initrd by
 mounting it first and then copying the file over as follows:
 
```

$ mkdir -p rootfs
$ mount -o loop rootfs.ext2 rootfs
$ cp test-program rootfs/root/
$ umount rootfs

```
 
 - After adding your program in the initrd, it can be tested through the virtual machine. To execute it run following:
 
```

 $ qemu-system-riscv -kernel bbl -append vmlinux \
   -drive file=rootfs.ext2, format=raw -nographic
   
```
 
 - Now this will boot the virtual machine. Eventually the entry of a user name is required.
 Enter root (no password required). When logged in, the test program can simply be
 run by:
 
```

$ /root/test-program
 
```
