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
PACO relies on [libuuid](https://sourceforge.net/projects/libuuid/) and [lua](https://www.lua.org/), if they aren't already on your maschine, please install them. 
- libuuid is a The libuuid library is used to generate unique identifiers. It is needed so that Clang and LLVM would work properly. *which version is needed?*. If you do not have it already, You can install it using:  
```bash
$ # sudo apt-get install uuid-dev
```  
- Lua is a powerful, efficient, lightweight, embeddable scripting language. It is needed to compile your code to run on PACO's approximate LUT. You can check if lua is already installed on your machine using:  
```bash
$ # lua -v
```  
If you don't have it already you can download it from [here](https://www.lua.org/download.html).
- python is ... `python --version` checks the version running 

### explain what the prerequisites are, how to check if they are already installed 
### I think there are more prerequisites like Python and which version. please ask others

You also need some disc space free on your machine. ### Give a quantity or leave this sentence out

Now that you have all the prerequisites setup precisely [:wink], lets move on to [downloading](https://paco-cpu.github.io/paco-cpu/docs/download/) PACO on your machine.
