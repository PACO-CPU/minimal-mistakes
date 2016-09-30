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

(insert images: traveling windows for standard gaussian, LUT gaussian)

Only the 3 most significant bits of each pixel in the window are fed into the lookup table to first look-up an intermediate result for the horizontal traveling window. Another lookup from the intermediate image returns the final value of each pixel.

(insert figure: LUT HW schematic)

Since the number of possible input combinations is 2^(3\*3)=512 and the hardware Lookup Table has less entries, entries that contain the same output results must be combined. The LUT compiler does this for arithmetical functions with one parameter, in this case it was done manually. The AND-plane can now recognize input patterns and the OR-plane generates addresses for the memory containing the results.

Original image:

(insert Lenna images)

This is the output of a precise Gaussian blur algorithm:

This is the output of an approximate Gaussian blur algorithm using the lookup table:

The performance gains:
(insert speedup graph for Gaussian LUT)


ALU?

(insert a checkerboard image with different parameters for Gaussian ALU, maybe small with a link to the full image)
