---
title: "Download"
permalink: /docs/download/
excerpt: "How and where from can the PACO toolchain be downloaded."
modified: 2016-08-08T16:25:30-04:00
sidebar:
    nav: "getting-started"
---

## Download
To prevent you from cloning all subdirectories of the project by yourself, you can download the content from the master directory: (TODO: add link)
Be aware that all data will need about 18GB. 

## Repository structure

Here you can take a look into the structure to have a clue how the repositories are located correct. 

#### The navigation below is not removed as a hint for documentation of the project structure

```bash
paco-env                                 # Main folder of the whole project
├── env.sh                               # Shell script that should be sourced before working with any tool of PACO. 
├── install.sh                           # Shell script that automates the installation process of the software tools. 
├── _qemu                                # Repository containing the QEMU emulator with PACO extension. Note: QEMU is not usable for PACO anymore.
├── _riscv-tools                         # This is the installation directory for all software tools used. Also the RISCV shell variable points here.
├── _riscv-tools-src                     # Repository containing all the software tools needed to create and run executables.
|  ├── _py                               # Directory containing the python libraries used by the flash-tool to communicate with the FPGA.
|  ├── _riscv-fesrv                      # Repository containing the frontend-server used for communication. Note: This is not used by PACO
|  ├── _riscv-gnu-toolchain              # Repository containing the PACO extended binutils and the GCC compiler.
|  ├── _riscv-isa-sim                    # Repository containing the golden RISCV simulator. Note: PACO did not extend this simulator.
|  ├── _riscv-llvm                       # Repository containing the PACO extended LLVM backend used for optimizing and emitting assembly code.
|  |  ├── _riscv-clang                   # Repository containing the PACO extended C/C++ compiler of the LLVM compiler framework.
|  ├── _riscv-lut-compiler               # Repository for the LUT-compiler that creates a LUT configuration ready to be linked to an executable.
|  ├── _riscv-opcodes                    # This repository contains a textutal representation of all CPU instructions, which is used to generate a decoder for binutils and the Rocket chip.
|  ├── _riscv-pk                         # This repository contains the RISC-V Proxy Kernel used on tethered systems to run binaries. It also contains the Berkeley Bootloader to boot Linux.
|  ├── _riscv-tests                      # Repository containing hand written assembly tests for testing the Rocket chip's functionallity.
|  |  ├── _env                           # Repository containing the framework for writing tests, that test the functionallity of the Rocket chip.
|  ├── _rocket-chip                      # Repository containing all the components of the CPU. Also contains the configurations to generate variants.
|  |  ├── _chisel                        # Chisel is a new open-source hardware construction language developed at UC Berkley used for Rocket chip.
|  |  ├── _context-dependent-environment # A Scala library which is used for parameterization of the Rocket chip
|  |  ├── _dramsim2                      # DRAMSim is a cycle accurate model of a DRAM memory controller.
|  |  ├── _emulator                      # Directory for generating a cycle accurate C emulator which can be used for simulation.
|  |  ├── _fsim                          # Directory for generating a verilog description of the Rocket chip, which can be used for FPGAs.
|  |  ├── _groundtest                    # A memory tester circuit for Rocket Chip's memory system.
|  |  ├── _hardfloat                     # A repository containing hardware floating-point units written in Chisel.
|  |  ├── _junctions                     # A repository for peripheral components and IO devices associated with the RocketChip project.
|  |  ├── _rocket                        # Contains the Rocket CPU and caches.
|  |  ├── _torture                       # This is the RISCV random test generator framework used to verify the Rocket chip.
|  |  ├── _uncore                        # This is the repository for uncore components associated with the Rocket chip project.
|  |  ├── _vsim                          # Directory for generating a verilog description of the rocket-chip which can be used for ASIC.
|  |  ├── _zscale                        # Contains the Zscale cpu implementing the RV32IMA ISA and is not used by this project.
|  ├── _rocket-soc                       # Contains only a license file and a readme, which have to be retained.
|  |  ├── _rocket_soc                    # Contains the ecosystem around the CPU, e.g. axi-bus, sram, etc, the bootloader and the ISE project.
|  |  |  ├── _lib                        # Contains the RocketLib to communicate from your program running on the FPGA to the machine attached
|  |  |  ├── _rocket-lut                 # This direcory contains the VHDL description of the LUT functional unit as well as software to test this.
