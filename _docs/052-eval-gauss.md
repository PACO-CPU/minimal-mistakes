---
title: "Gauss Filter"
permalink: /docs/eval-gauss/
excerpt: "Gauss Filter"
sidebar:
   nav: "evaluation"
---
{% include base_path %}

### Approximate Gaussian Filter Evaluation
The Gaussian blur filter algorithm is used in image processing to smooth over noisy images. They generally generate a new color value for each pixel by incorporating the color values of neighboring pixels, weighted depending on the distance between pixel and neighbor.

Precise implementations of the Gaussian blur algorithms calculate this by moving a sliding window over the image, adding up neighboring pixels (multiplied by weights).

We compare a precise implementation of the Gaussian blur algorithm with a 3x3 window (greyscale) to implementations using

* the [approximate ALU]() **insert address**
* the [Lookup Table]() **insert address**

### Evaluation: Lookup Table
**insert anchor**
The Gaussian LUT implementation passes over the image twice: once with a 3x1 window in the horizonal direction to generate an intermediate image, then with a 1x3 window in the vertical to generate the final pixel value. The lookup table is fed with the 3 most significant bits from each pixel value in the window.

<img src="/paco-cpu/images/gauss_filter_grid.png" alt="Gaussian window" width="500">

Only the 3 most significant bits of each pixel in the window are fed into the lookup table to first look-up an intermediate result for the horizontal traveling window. Another lookup from the intermediate image returns the final value of each pixel.

For a 256 by 256 pixel image the original:

<img src="/paco-cpu/images/results/lut/lenna_256/lenna_256x256.png" alt="Lenna original" width="512">

a precisely Gaussian-blurred version:

<img src="/paco-cpu/images/results/lut/lenna_256/lenna_256x256_native.png" alt="Lenna native" width="508">

and an an approximated Gaussian blur version, created with a Lookup Table with 9 inputs and 128 possible entries:

<img src="/paco-cpu/images/results/lut/lenna_256/lenna_256x256_lut.png" alt="Lenna lut" width="508">

The performance gains:
(insert speedup graph for Gaussian LUT)

### 3.1 Implementation

This implementation approximates the multiplication of one pixel with the filter kernel using **mul.approx** and the additions of the resulting values from each multiplication using **add.approx**. Other then that, it corresponds to the [native implementation](anchor).**TODO:** Add anchor 

The complete code including a makefile can be found [here](https://github.com/PACO-CPU/rocket-soc/tree/master/rocket_soc/lib/templates/alu-gaussian-application). 

### 3.2 Approach

The application was run on a [ml605 FPGA](https://www.xilinx.com/products/boards-and-kits/ek-v6-ml605-g.html) using the script
[run_eval.py](https://github.com/PACO-CPU/rocket-soc/blob/master/rocket_soc/lib/templates/alu-gaussian-application/run_eval.py).
This script iterates over a [Lenna](https://en.wikipedia.org/wiki/Lenna) image in three different sizes: 128x128, 192x192, and 256x256. For each iteration it applies the gaussian filter once using the native implementation and afterwards it applies the filter for each possible neglect amount combination the two instructions can have. An image is saved once for the native run and for each possible combination run using the following naming convention:

- Native -> native.png
- mul.approx with 2 bits neglected, add.approx not used -> MUL63.png
- add.approx with 4 bits neglected, mul.approx not used -> ADD62.png
- add.approx with 7 bits neglected, mul.approx with 4 bits neglected -> ADD60MUL62.png

**Note:** The values after MUL and ADD in the image name correspond to the decimal value of the binary neglect masks defined in the [Design Document]()**TODO**: Add link to table in Design Document

### 3.3 Results

The Table below shows the results for an image of the size 256x256 pixel. The first column of the table describes how many bits were neglected on a **mul.approx** instruction, the second column is likewise for **add.approx** instructions. A " - " means that a precise instruction was used. The third column is 
a calculation of the [approximation error](https://en.wikipedia.org/wiki/Approximation_error) between the natively calculated image and the respective approximately computed image. The last column show the resulting image of the approximate calculation.

| MUL neclect amount | ADD neglect amount | Approximation error | Image |
|:---:|:---:|:--------------:|:-----:|
| - 	| - 	| -              | ![ADD62](/paco-cpu/images/results/alu/lenna-256x256-native.png)|
| - 	| 2 	| 0              | ![ADD62](/paco-cpu/images/results/alu/lenna-256x256-native.png)|
| - 	| 4 	| 0.0004360977   | ![ADD62](/paco-cpu/images/results/alu/ADD62.png) |
| - 	| 7 	| 0.0025993256   | ![ADD60](/paco-cpu/images/results/alu/ADD60.png) |
| - 	| 10	| 0.0199205464   | ![ADD56](/paco-cpu/images/results/alu/ADD56.png) |
| - 	| 15	| 0.4975493702   | ![ADD48](/paco-cpu/images/results/alu/ADD48.png) |
| -	  | >15	| 1              | ![ADD32](/paco-cpu/images/results/alu/black.png) |
| 2 	| - 	| 0.0161600577   | ![ADD48](/paco-cpu/images/results/alu/MUL63.png) |
| 2 	| 2 	| 0.0161600577   | ![ADD48](/paco-cpu/images/results/alu/MUL63ADD63.png) |
| 2 	| 4 	| 0.0161600577   | ![ADD48](/paco-cpu/images/results/alu/MUL63ADD62.png) |
| 2 	| 7 	| 0.0185167734   | ![ADD48](/paco-cpu/images/results/alu/MUL63ADD60.png) |
| 2 	| 10 	| 0.0367156413   | ![ADD48](/paco-cpu/images/results/alu/MUL63ADD56.png) |
| 2 	| 15	| 0.5161841232   | ![ADD48](/paco-cpu/images/results/alu/MUL63ADD48.png) |
| 2 	| >15	| 1              | ![ADD32](/paco-cpu/images/results/alu/black.png) |
| 4 	| - 	| 0.1064377457   | ![ADD48](/paco-cpu/images/results/alu/MUL62.png) |
| 4 	| 2 	| 0.1064377457   | ![ADD48](/paco-cpu/images/results/alu/MUL62ADD63.png) |
| 4 	| 4 	| 0.1064377457   | ![ADD48](/paco-cpu/images/results/alu/MUL62ADD62.png) |
| 4 	| 7 	| 0.1064377457   | ![ADD48](/paco-cpu/images/results/alu/MUL62ADD60.png) |
| 4 	| 10	| 0.1143191514   | ![ADD48](/paco-cpu/images/results/alu/MUL62ADD56.png) |
| 4 	| 15	| 0.6022564094   | ![ADD48](/paco-cpu/images/results/alu/MUL62ADD48.png) |
| 4 	| >15	| 1              | ![ADD32](/paco-cpu/images/results/alu/black.png) |
| 7 	| - 	| 0.7206358056   | ![ADD48](/paco-cpu/images/results/alu/MUL60.png) |
| 7 	| 2 	| 0.7206358056   | ![ADD48](/paco-cpu/images/results/alu/MUL60ADD63.png) |
| 7 	| 4 	| 0.7206358056   | ![ADD48](/paco-cpu/images/results/alu/MUL60ADD62.png) |
| 7 	| 7 	| 0.7206358056   | ![ADD48](/paco-cpu/images/results/alu/MUL60ADD60.png) |
| 7 	| 10 	| 0.7206358056   | ![ADD48](/paco-cpu/images/results/alu/MUL60ADD56.png) |
| 7 	| 15	| 0.7403286548   | ![ADD48](/paco-cpu/images/results/alu/MUL60ADD48.png) |
| >7  | * 	| 1              | ![ADD32](/paco-cpu/images/results/alu/black.png) |
                   
