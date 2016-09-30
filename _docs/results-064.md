---
title: "Star image comparison"
permalink: /docs/results-064/
excerpt: "Visual comparison of 64x64 images."
---

For a 64 by 64 pixel image the original:

<img src="/paco-cpu/images/results/lut/star/star_64x64.png" alt="Star original" width="128">

a precisely Gaussian-blurred version:

<img src="/paco-cpu/images/results/lut/star/star_64x64_native.png" alt="Star native" width="124">

and an approximated Gaussian blur version, created with a Lookup Table with 9 inputs and 128 possible entries:

<img src="/paco-cpu/images/results/lut/star/star_64x64_lut.png" alt="Star lut" width="124">
