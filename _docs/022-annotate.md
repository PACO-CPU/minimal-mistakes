---
title: "Annotating Code"
permalink: /docs/annotate/
excerpt: "Annotating C Code with PACO constructs"
modified: 2016-08-31T11:00:35-04:00
sidebar:
  nav: "tutorial"
---

{% include base_path %}

This guide gives an overview over the way functions and variables can be annotated in C-code. Consider this guide as a cheat sheet. For annotating **functions** click [here](#1-function-approximation) and for **variables**, [here](#2-variable-approximation).

This guide however does not provide all the details regarding annotations, for which please read the the [Design Document](/paco-cpu/docs/design-doc.pdf#nameddest=sec:lang-lut-generator) 

## 1. Function Approximation

### Key/value pairs

key | value range | short description | notes
:---:|:---:|:---:|:---:
|**name** | Any string | this uniquely identifies this function | Will be set by clang, should not be set manually
|**numSegments** | 0 to 2^segmentsBits-1 |This defines the maximum number of segments (primary + secondary) in which the function ought to be divided | - |
|**numPrimarySegments** | (0 to 2^segmentsBits-1) | This defines the maximun number of primary segments in which the function ought to be divided  | - |
|**segments** | "uniform", "log-left", "log-right", or "min-error" | This defines how the segments should be distributed in the function to be approximated | See table below for an overview over the segmentation strategies. |
|segments2 | "uniform", "log-left", "log-right", or "min-error" | This defines how the subsegments (secondary segments) should be distributed in the function to be approximated  | Experimental |
|**explicitSegments** | [min,max],(min,max),... | If the programmer knows the segments beforehand, he can explicitly state them as comma seperated value ranges | - |
|**approximation** | "linear", or "step" | Describes which strategy should be used to approximate the function within each segment | 
|**bounds** | (min, max) | If you know your the range of the input values to the function beforehand you can specify it here | - |

### Segmentation Strategies:

value | short description | notes
:---: | :---: | :---:
**uniform** | all segments are uniformly distributed | -
**log-left** | the size of segments increases by the power of 2 starting from the right | -
**log-right** | the size of segments increases by the power of 2 starting from the left | -
**min-error** | the segments are chosen by the minizing the approximation error depending on the approximation strategy | You need to supply the key/value pair **approximation**

### Example Functions

![log-left](/paco-cpu/images/annotation-example-log-left.png)

![uniform](/paco-cpu/images/annotation-example-uniform.png)

## 2. Variable Approximation

### Key/Value Pairs

key | valid values | short description | notes
:---:|:---:|:---:|:---:
**neglect_amount** | 2,4,7,10,15,20,27 | Describes how many least significant bits should be neglected on operations with this variable | mutually exclusive with **mask**
**mask** | 0b1111110, 0b1111100, ..., 0b0000000| Similar to **neglect_amount**, but the neglected bits are specified as a mask | mutually exclusive with **neglect_amount** 
**inject** | 0, 1 | A variable, that has inject=1 is marked as approximate for operations that use this variable as an input. | -
**relax** | 0,1  | A variable, that has relax=1 can be approximated on operation even when it's inputs are seen as precise  | Default=1
