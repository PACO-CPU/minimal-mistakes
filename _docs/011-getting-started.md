---
title: "Quick-Start Guide"
permalink: /docs/getting-started/
excerpt: "How to quickly install and setup Minimal Mistakes for use with GitHub Pages."
modified: 2016-04-13T15:54:02-04:00
redirect_from:
  - /theme-setup/
sidebar:
  nav: "getting-started"
---

{% include base_path %}

### Write introduction to getting started page

## Prerequisites

Fork the [Minimal Mistakes theme](https://github.com/mmistakes/minimal-mistakes/fork), then rename the repo to **USERNAME.github.io** --- replacing **USERNAME** with your GitHub username.

<figure>
  <img src="{{ base_path }}/images/mm-theme-fork-repo.png" alt="fork Minimal Mistakes">
</figure>

---

Congratulations! You've successfully blah blah!

---

### Real page starts here:

---


# Getting started with PACO – Paderborn CPU Core for Approximate Computing

Welcome on the webpage of the project PACO. PACO is an implementation of a CPU core which contains approximate computing units. In the current state, it consits two approximation units. The first is an approximate ALU which can add, substract and multiply approximately, the second one is lookup table, which selects a precomputed output for a specific function. 
The approximate ALU can be used to analyse approximation, the LUT also saves computation time up to be 3 times faster than a normal CPU would compute results. 

Before you start to download and use PACO, please make sure you have all the needed prerequisites.

## Prerequisites

For installation you need some packages installed on your machine: 
- libuuid for Clang and LLVM
- lua for the LUT Compiler

You also need some disc space free on your machine. 

## Next steps

Now you can download the content from the git repository. Click on Download to do it.

When the downloaded was successful, you can start to build the project. To do so, see Build. 

To run it, read content of Run. 

For using PACO with your own code, please look into the Tutorial section how to annotate your code and how to use PACO. 

If you want to extend PACO with your own ideas, look into the Documentation to understand how the core works. 

If you are interested in the benefit of PACO, please see the Evaluation section. 

For scientific interests and similar work, look into the Links section
