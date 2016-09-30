---
title: "Quick-Start Guide"
permalink: /docs/getting-started/
excerpt: "How to quickly install and setup Minimal Mistakes for use with GitHub Pages."
sidebar:
  nav: "getting-started"
---

{% include base_path %}

# Getting started with PACO

Welcome to our Getting-started page where you can find the prerequists to use PACO and how to download, build and use the core and toolchain. Now lets make sure you have all the required prerequisites.

## Prerequisite
PACO relies on [libuuid](https://sourceforge.net/projects/libuuid/) and [lua](https://www.lua.org/), if they aren't already on your machine, please install them.  

#### If you already worked with the rocket core, you just have to check the following packages:

- libuuid is used to generate unique identifiers. It is needed so that Clang and LLVM would work properly. If you do not have it already, You can install it using:  

```bash
$ sudo apt-get install uuid-dev
```  
    
- Lua is a powerful, efficient, lightweight, embeddable scripting language. It is needed to compile your code to run on PACO's approximate LUT. You can check if lua is already installed on your machine using: 

```bash
$ lua -v
```  
  
If you don't have it already you can download it from [here](https://www.lua.org/download.html).  

For both and libuuid lua you can use the newest version. If problems occur, use the tested versions for libuuid(2.20.1-5.lubuntu20.7) and lua(5.2.3-1).

- Python is used to communicate with the core via the UART interface. Version 2.7.6 is known to work with our environment. You can check your version by using the command:

```bash
$ python --version
```  

#### Assumed you use a new installation of Ubuntu 16.04 LTS the following command will install the missing liberaries for PACO:

```bash
$ sudo apt-get install autoconf automake autotools-dev curl libmpc-dev \
libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf \
libtool patchutils bc uuid-dev liblua5.2-dev
``` 

#### Installation on other systems

We suppose you use Ubuntu 16.04 LTS where all components are known to run successfully. You are free to use other linux distributions as well. For example parts of PACO has been tested to run successful on Arch Linux. 

#### Next step

Now that you have all the prerequisites setup precisely [:wink], lets move on to [downloading](https://paco-cpu.github.io/paco-cpu/docs/download/) PACO on your machine.
