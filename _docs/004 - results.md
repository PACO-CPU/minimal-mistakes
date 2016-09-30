---
title: "Results"
permalink: /docs/results/
excerpt: "The results obtained in PACO with LUT and Approx ALU"
modified: 2016-09-30T15:54:02-04:00
redirect_from:
  - /theme-setup/
---

{% include base_path %}

### Measuring Improvement
The stock Rocket core is compared to the approximate PACO core. The PACO core was not modified apart from integration of the approximate functional units and necessary changes to the decoder.
 
We chose two different image processing tasks as benchmarks, [Gaussian blur](https://en.wikipedia.org/wiki/Gaussian_blur), which is a neighbourhood operation (with several parameters), and [Gamma correction](https://en.wikipedia.org/wiki/Gamma_correction), which is a point operation (with one). Primary advantage of using image processing benchmarks is the possibility of visual appraisal of result quality by humans. (In precise benchmarks, exact conformance of results is expected, here other result quality metrics are needed. Since many use cases for approximate computing results expect human consumption, visual appraisal seems fitting.)

Both were used as test applications for both our approximate ALU and the Lookup Table, verifying their results stay within predicted error bounds and giving an impression of the effects of approximation for the human eye.

### Example: Accelerate Gaussian Blur with Lookup Table

An approximate implementation of the Gaussian algorithm is roughly 3 times as fast as a precise implementation. (Details) **TODO insert link to Gauss eval**

(insert graph)

The approximate result image is noticeably different from the precise version, but noise would certainly be filtered out.

(insert original image, precise image, approximate image)

(insert figure: LUT HW schematic)

Since the number of possible input combinations is 2^(3\*3)=512 and the hardware Lookup Table has less entries, entries that contain the same output results must be combined. The LUT compiler does this for arithmetical functions with one parameter, in this case it was done manually. The AND-plane can now recognize input patterns and the OR-plane generates addresses for the memory containing the results.

In effect, instead of

* a multiplication and an addition for each pixel in the Gauss filter neighborhood,
* and a division at the end,

for each pixel two lookup instructions are executed. A lookup instruction takes only one cycle in the execution stage of the pipeline.

### Example: Accelerate Gamma Correction with Lookup Table

Our other example application, Gamma correction, was accelerated by a more modest 38%. (Details) **TODO insert link to Gamma eval**
