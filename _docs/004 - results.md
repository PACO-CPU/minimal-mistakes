---
title: "Results"
permalink: /docs/results/
excerpt: "The results obtained in PACO with LUT and Approx ALU"
---

{% include base_path %}

### Measuring Improvements
Improvements on the execution are measured by comparing the native Rocket core to the approximate PACO core. Modification of the Rocket core was limited to integration of the approximate functional units and the necessary changes to the decoder.
 
We chose two different image processing tasks as benchmarks: [Gaussian Blur](https://en.wikipedia.org/wiki/Gaussian_blur), a neighbourhood operation with several parameters, and [Gamma Correction](https://en.wikipedia.org/wiki/Gamma_correction), a point operation with a single parameter. The primary advantage of using image processing benchmarks is the possibility of visual appraisal of the quality of results by humans. (In precise benchmarks, exact conformance of results is expected, whereas here other quality metrics are required. Since the results of many approximate computing use cases expect human consumption, visual appraisal seems apt.)

Gaussian Blur and Gamma Correction were both used as test applications for the Approximate ALU and the Lookup Table. Let's look at some of the results obtained:

### Accelerating Gaussian Blur with the Lookup Table

An approximate implementation of the Gaussian algorithm is roughly **3 times** faster than the precise implementation. The graph of the performance can be seen below,

 <img src="/paco-cpu/images/results/lut/gaussian_lut_speedup.png" alt="LUT speedup" width="500" height= "300" style = "margin:30px">

A look at one of the example evaluated images:

<div style = "display:flex; flex-direction:row; justify-content: space-around;" >
 <img src="/paco-cpu/images/results/lut/star/star_64x64.png" alt="LUT example" style = "margin:30px">
 <img src="/paco-cpu/images/results/lut/star/star_64x64_native.png" alt="LUT example native" style = "margin:30px">
 <img src="/paco-cpu/images/results/lut/star/star_64x64_lut.png" alt="LUT example lut" style = "margin:30px">
</div>

The leftmost image is the original image, the middle one has been generated precisely and the rightmost, approximately. The resulting approximate image is noticeably different from the precise version. However, it can be quite clearly recognized by the human eye without suffering from substantial quality loss, considering the speedup obtained. 

For more details, check the [Gaussian evaluation](/paco-cpu/docs/eval-gauss/) section.

### Accelerating Gamma Correction with the Lookup Table

The Gamma correction application was accelerated by a modest 38%. [Details ...](/paco-cpu/docs/eval-gamma/)
