---
title: "Evaluation"
permalink: /docs/evaluation/
excerpt: "Introduction to PACO evaluation"
sidebar:
   nav: "evaluation"
---
{% include base_path %}

## Evaluation

Many common benchmarks expect more than the very limited amount of RAM available on our synthesis of the Rocket SoC for the [ml605 FPGA](https://www.xilinx.com/products/boards-and-kits/ek-v6-ml605-g.html). We deliberated about choice of existing benchmarks or writing our own, and convinced ourselves that a priority for approximate computing benchmarks should be human assessibility: Many use cases of approximate computing have in common that imprecision is tolerable because humans will not notice differences.

Governed by these two guidelines, we decided to write our own (small) image processing benchmarks:

* a [Gaussian blur image filter application](/paco-cpu/docs/eval-gauss/) and
* a [Gamma correction image filter application](/paco-cpu/docs/eval-gamma/).

They have different demands on a CPU: One needs only one input per calculation, the other needs several (neighborhood operation). One only needs basic ALU functions, the other is arithmetically more complex. 
