---
title: "Results"
permalink: /docs/results/
excerpt: "The results obtained in PACO with LUT and Approx ALU"
---

{% include base_path %}

### Measuring Improvement
The stock Rocket core is compared to the approximate PACO core. The PACO core was not modified apart from integration of the approximate functional units and necessary changes to the decoder.
 
We chose two different image processing tasks as benchmarks, [Gaussian blur](https://en.wikipedia.org/wiki/Gaussian_blur), which is a neighbourhood operation (with several parameters), and [Gamma correction](https://en.wikipedia.org/wiki/Gamma_correction), which is a point operation (with one). Primary advantage of using image processing benchmarks is the possibility of visual appraisal of result quality by humans. (In precise benchmarks, exact conformance of results is expected, here other result quality metrics are needed. Since many use cases for approximate computing results expect human consumption, visual appraisal seems fitting.)

Both were used as test applications for both our approximate ALU and the Lookup Table, verifying their results stay within predicted error bounds and giving an impression of the effects of approximation for the human eye.

### Example: Accelerate Gaussian Blur with Lookup Table

An approximate implementation of the Gaussian algorithm is roughly 3 times as fast as a precise implementation. For more details, check the [Gaussian evaluation](/paco-cpu/docs/eval-gauss/) section.

 <img src="/paco-cpu/images/results/lut/gaussian_lut_speedup.png" alt="LUT speedup" width="500" height= "300" style = "margin:30px">

The approximate result image is noticeably different from the precise version, but noise would certainly be filtered out.

The following images from left to right: original image, image from the precise version and the image approximated. 

<div style = "display:flex; flex-direction:row; justify-content: space-around;" >
 <img src="/paco-cpu/images/results/lut/star/star_64x64.png" alt="LUT example" style = "margin:30px">
 <img src="/paco-cpu/images/results/lut/star/star_64x64_native.png" alt="LUT example native" style = "margin:30px">
 <img src="/paco-cpu/images/results/lut/star/star_64x64_lut.png" alt="LUT example lut" style = "margin:30px">
</div>
<img src="/paco-cpu/images/results/lut/LUT-design.png" alt="LUT core" width="700" style = "margin:30px">

Since the number of possible input combinations is 2^(3\*3)=512 and the hardware Lookup Table has less entries, entries that contain the same output results must be combined. The LUT compiler does this for arithmetical functions with one parameter, in this case it was done manually. The AND-plane can now recognize input patterns and the OR-plane generates addresses for the memory containing the results.

In effect, instead of

* a multiplication and an addition for each pixel in the Gauss filter neighborhood,
* and a division at the end,

for each pixel two lookup instructions are executed. A lookup instruction takes only one cycle in the execution stage of the pipeline.

### Example: Accelerate Gamma Correction with Lookup Table

Our other example application, Gamma correction, was accelerated by a more modest 38%. For more details, check the [Gamma Evaluation](/paco-cpu/docs/eval-gamma/) page.*
