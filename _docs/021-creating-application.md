---
title: "Creating your Application"
permalink: /docs/create-application/
excerpt: "Creating your Application."
modified: 2016-09-226T17:19:29-04:00
redirect_from:
  - /theme-setup/
sidebar:
  nav: "tutorial"
---

{% include base_path %}

This guide will give you an introduction on how to write a simple 
applications which use the PACO components. This guide will be split up
in two parts depending on the component you want to use. Both parts will
share steps and can of course be combined to create a binary which uses
both components.

## 1. Decide on the Approximate Component to Use
- If you're interested to use the Lookup Table (LUT) start [here](#2-lut-guide)
- If you're interested to use the Approximate ALU start [here](#3-approximate-alu-guide)

## 2. Lut Guide <a id="#2-lut-guide"></a>
The Lookup Table (LUT) is a functional unit residing in the CPU pipeline and can be imagined as a software lookup table on crack. It's main purpose is to approximate any derivable function. To visualize it, lets take look and the graph of some function:

 <img src="/paco-cpu/images/lut-function.png" alt="lut-function" width="300">

In order to approximate this function, it needs to be split into several intervals, here called **segments**.
This example image shows a linear distribution of segements, but with the PACO tools other distributions can
be chosen, e.g. logarithmic (see **TODO: Insert link to impl. Doc**). To give you fine grained control these **primary segments** can be further divided into **secondary segment**.

For each segment we can now interpolate the function. The picture below shows a linear interpolation for each 
segment. The interpolated line of each segment can then be stored as integer values m, b in our LUT. With the formula
y = m * x + b we can describe the line again.

 <img src="/paco-cpu/images/lut-function-linear.png" alt="lut-function" width="300">
 
 For more information on the LUT please read the [Implementation Document](TODO)**TODO:Add link to Impl. Doc.**

For this example we will use a [Gamma correction](https://en.wikipedia.org/wiki/Gamma_correction) image filter. 

### 2.1 Pick your function to be approximated
First we have to implement our function in normal C code. You can see our implementation below:

```c
#include <math.h>

long image[IMG_WIDTH * IMG_HEIGHT];
long result_image[IMG_WIDTH * IMG_HEIGHT];

/* This is the implementation of our gamma correction */
long gamma(long a) 
{
  double v;
  int r;
  v=(double)a/(double)(1uL<<24);
  v= 1.0 * pow(v,0.25);
  if (v>1) v=1; else if (v<0) v=0;
  r=(int)(v*(double)(1uL<<24));
  return r;
}   

int main()
{
    int i;
    long inp;

    for(i = 0; i < IMG_WIDTH * IMG_HEIGHT; i++) {
        /* since we use greyscale images, we shift
           the data into the red channel */
        inp = image[i] << 16;
        result_image[i] = gamma(inp);
    }
}
```
Since we have implemented our function now, we need to tell the compiler to use the LUT for this 
function as well as decide how we want to divide it into segments and which range on the x-axis 
should be divided into segments. This is done by annotation which will be covert in the next 
section.

### 2.2 Annotate your function for approximation 
First we need to tell the compiler that our function **gamma** should be approximated by the LUT. We
do that by adding the **approx** decorator. Additionally we need to give the decorator the keyword 
**strategy="lut"** to indicate that we want to use the LUT for approximating this function.

```c
long approx(strategy="lut") gamma(long a)
{
/* ... */
}
```

Now that the compiler knows that this function should be approximated using the LUT, we can give hints how the 
approximation should be done. We do this by adding more key/value pairs to the approx decorator. The code snippet 
below the pairs we will be using:

```c
long approx(strategy="lut" numPrimarySegments="6" bound="(0,16777215)" segements="uniform" approximation="linear") gamma(long a)
{
/* ... */
}
```
An explenation for the key/value pairs we used can be seen here:

- **numPrimarySegments** describes how many **primary segments** should be used for approximation. Since we don't subdivide our segements into subsegments this is also the total number of segments.
- **bound** is used to describe the range of input values of our function we are interested in. It is given as a list of intervals (min, max), (min, max),.. . For an image we have 3 colors with 8 bit per pixel, which leads to a maximum value of (2⁸)³ = 16777216 and a minimum value of 0.
- **segments** describes how the segements are distributed in this case linear as in the pictures in section 2.
- **approximation** describes how the function is approximated within each segment. Linear in this case means that it is approximated using a line, as can be seen in the picture of section 2.

For more information on other possible key/values please read [Annotate Code](/paco-cpu/docs/annotate/).
    
### 2.3 Compile your program 
The basic steps to compile you program are (for more detail, refer to [User Guide](TODO) **TODO: Add link to User Guide**:

1. Compile you program using clang. This will yield an llvm-ir file of your code and an input file to the lut-compiler
2. Use llc to convert the llvm-ir file into an assembly file
3. Invoke the lut-compiler on it's input file to generate a configuration for the LUT
4. Use the lut-startup script with the configuration to create startup code that loads the configuration.
5. Link everythink together into a binary

Now you should have a binary ready to be run on an FPGA.
    
### 2.4 Run your program on the FPGA 
For instructions on how you can run your program on the FPGA please take a look [here](/paco-cpu/docs/use-fpga/). 

**TODO: Add fancy images**

## 3. Approximate ALU Guide <a id="#3-approximate-alu-guide"></a>
The PACO Approximate ALU is used to show the effect approximation has on certain applications. It is accomplished by not using some of least significant bits for an operation like add, sub, or mul.  Since no one can know which variables support these approximate operation you as the programmer need to annotate these variables as imprecise. The next section will show you how to do that.

For this example we will use a  [Gaussian blur](https://en.wikipedia.org/wiki/Gaussian_blur) image filter with the following kernel matrix:

 <img src="/paco-cpu/images/matrix.png" alt="alt text" width="206" height="153">


The complete code for this example, including a Makefile  can be found [here](TODO) **TODO: Add a link to the whole gauss application.**

### 3.1 Pick variables which can be imprecise
Lets say we have the following program snippet implementing this filter:

```c
long image[IMG_WIDTH * IMG_HEIGHT];
long result_image[IMG_WIDTH * IMG_HEIGHT];
long kernel[9] = {100, 300, 100,
                  300, 900, 300,
                  100, 300, 100};
void gauss()
{
    long image_data;
    long kernel_data;
    long intermediate_data;
    long result;

    for (x = 1; x < IMG_WIDTH - 1; x++) {
        for (y = 1; y < IMG_HEIGHT - 1; y++) {
            image_data = image[(y - 1) * IMG_WIDTH + (x - 1)];
            kernel_data = kernel[0];            
            intermediate_data = image_data * kernel_data;
            result = result + intermediate_data;
        
            image_data = image[(y - 1) * IMG_WIDTH + (x      )];
            kernel_data = kernel[1];            
            intermediate_data = image_data * kernel_data;
            result = result + intermediate_data;  

            /* .... */
            result /= 2500;
            result_image[y * IMG_WIDTH + x] = result; 
        }
    }
}
```

Suitable for approximation would be the variable **image_data**, **intermediate_data**, and the **result**. These are suitable because the input and output are images intended to be seen by humans, who cannot notice minor errors. The next section will explain how to mark these variables for approximation.

### 3.2 Annotate variables for approximation
We annotate a variable with approximate decorators as follows :

```c
/* ... */
void gauss()
{
    long approx(neglect_amount=2 inject=1)image_data;
    long kernel_data;
    long approx(neglect_amount=2 inject=1 relax=1)intermediate_data;
    long approx(neglect_amount=2, inject=1 relax=1)result;
}
```

An approx decorator can take key/value pairs which further describe how a variable can be approximated. For example: neglect_amount=2 tell the compiler
that the 2 least significant bits can be left out during an operation. If we take a look at the following code snippet from the gauss() function

```c
long approx(neglect_amount=2 inject=1 relax=1)intermediate_data;
long approx(neglect_amount=2, inject=1 relax=1)result;
/* since "intermediate_data" and "result" both can be approximated the compiler would emit a add.approx instruction here. */
result = result + intermediate_data;
```
we can see that if an operation uses two variables with approx decorators an approximate operation will be emitted. In this case this would be add.approx. 
The next section shows you how to compile your program and how this particular code snippet would be translated. If you want to read more
regarding annotation, take a look [here](/paco-cpu/docs/annotate/)

### 3.3 Compile your program
To compile your program there is not much more to do than invoking clang. The details on how to compile clang/llvm and which parameters to supply for example to use the correct ISA backended, please refer to the [User Guide](TODO) **TODO: Add link to user-guide document.**

However for now lets see how our compiler would translate the code snippet from above

```c
result = result + intermediate_data; 
/*
 * TODO: Add assembly here
 */
```

As you can see the compiler emitted the add.approx instruction. The last parameter of this instruction is the amount of bits to neglect. 

Congratulations, you successfully create your first approximate program using PACO.  Now let's see how it performs on the FPGA.

### 3.4 Run your program on the FPGA
For instructions on how you can run your program on the FPGA please take a look [here](/paco-cpu/docs/use-fpga/). 
For now, let us compare how the approximation affects the image. The default test image for graphical application is [Lenna](https://en.wikipedia.org/wiki/Lenna) as can be seen below in grey-scale.

![lenna-256x256](/paco-cpu/images/results/alu/lenna-256x256.png) 

Our approximated program with a neglect_amount of 4, which applies the gaussian filter, produces an image that looks like this:

![MUL62ADD62](/paco-cpu/images/results/alu/lenna-256x256-4bit-approx.png) 


Finally let's compare it against our program, which applies the gaussian filter without any approximate decorators: 

![native](/paco-cpu/images/results/alu/lenna-256x256-native.png) 

