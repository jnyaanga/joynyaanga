---
title: 'Analyzing single cell data: scanpy'
author: Joy Nyaanga
date: '2021-10-05'
slug: scanpy
categories: 
  - Python
  - genomics
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2021-10-05T20:51:42-05:00'
featured: no
image:
  caption: '[Photo by National Cancer Institute on Unsplash](https://unsplash.com/photos/L7en7Lb-Ovc?utm_source=unsplash&utm_medium=referral&utm_content=creditShareLink)'
  focal_point: ''
  preview_only: no
projects: [trajectory-inference]
---
This past summer, I was immersed in the world of single-cell genomics - a completely new field to me. With this came learning not only how data were experimentally collected, but also how to computationally process these data. 
  
Although much of my work was performed in Python, I dabbled a bit in the R tools for exploring single-cell RNA-seq data. As such, this will be part 1 of a two part series on basics of handling single-cell data. Here I intend to discuss some basics of `Scanpy`: a Python-based toolkit for handling large single-cell expression data sets.   

[`Scanpy`](https://scanpy.readthedocs.io/en/stable/) contains various functions for the preprocessing, visualization, clustering, trajectory inference, and differential expression testing of single-cell gene expression data. It is built jointly with [`AnnData`](https://anndata.readthedocs.io/en/latest/) which allows for simple tracking of single-cell data and associated metadata. Typically, I interface with Python and `Scanpy` with `jupyterlab` but in this post I use Rmarkdown to run Python code (see previous [post](/post/r-python) if you're curious how this is done).  

## Set Up   

```r
library(reticulate)
use_python('/Users/joy/miniconda3/bin/python')
```

Loading necessary python packages




































