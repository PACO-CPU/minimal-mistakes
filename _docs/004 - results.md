---
title: "Results"
permalink: /docs/results/
excerpt: "The results obtained in PACO with LUT and Approx ALU"
modified: 2016-04-13T15:54:02-04:00
redirect_from:
  - /theme-setup/
---

{% include base_path %}

### Demo Application to showcase PACO
The stock Rocket core is compared to the approximate PACO core. The PACO core was not modified apart from integration of the approximate functional units and necessary changes to the decoder.
 
We chose two different image processing tasks as benchmarks, [Gaussian blur](https://en.wikipedia.org/wiki/Gaussian_blur), which is a neighbourhood operation (with several parameters), and [Gamma correction](https://en.wikipedia.org/wiki/Gamma_correction), which is a point operation (with one). Primary advantage of using image processing benchmarks is the possibility of visual appraisal of result quality by humans. (In precise benchmarks, exact conformance of results is expected, here other result quality metrics are needed. Since many use cases for approximate computing results expect human consumption, visual appraisal seems fitting.)

Both were used as test applications for both our approximate ALU and the Lookup Table, verifying their results stay within predicted error bounds and giving an impression of the effects of approximation for the human eye.

(insert Lenna images)

(insert speedup graph for Gaussian LUT)

(insert a checkerboard image with different parameters for Gaussian ALU, maybe small with a link to the full image)
