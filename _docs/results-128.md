---
title: "Lenna 128x128 image comparison"
permalink: /docs/results-128/
excerpt: "Visual comparison of 128x128 images."
---

For a 128 by 128 pixel image the original:

<img src="/paco-cpu/images/results/lut/lenna/lenna_128x128.png" alt="Lenna original" width="256">

a precisely Gaussian-blurred version:

<img src="/paco-cpu/images/results/lut/lenna/lenna_128x128_native.png" alt="Lenna native" width="252">

and an approximated Gaussian blur version, created with a Lookup Table with 9 inputs and 128 possible entries:

<img src="/paco-cpu/images/results/lut/lenna/lenna_128x128_lut.png" alt="Lenna lut" width="252">
