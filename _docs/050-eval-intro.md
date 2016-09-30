---
title: "Evaluation"
permalink: /docs/evaluation/
excerpt: "Introduction to PACO evaluation"
sidebar:
   nav: "evaluation"
---
{% include base_path %}

Choosing suitable benchmarks to test the toolchain and the PACO core relied on several factors. 

- Several common benchmarks expect more RAM than the limited amount available on our synthesis of the Rocket SoC for the [ml605 FPGA](https://www.xilinx.com/products/boards-and-kits/ek-v6-ml605-g.html).
- The use cases of approximate computing require tolerance towards imprecision since humans will not be able to notice differences i.e, human assessibility.

Governed by these two guidelines, we decided to write our own image processing benchmarks:

* [Gaussian blur image filter application](/paco-cpu/docs/eval-gauss/) 
* [Gamma correction image filter application](/paco-cpu/docs/eval-gamma/).

