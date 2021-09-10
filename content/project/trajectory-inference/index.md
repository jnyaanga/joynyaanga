---
title: Trajectory Inference 
date: "2021-09-10T00:00:00Z"
external_link: ""
image:
  caption: '[Photo by David Brooke Martin on Unsplash](https://unsplash.com/photos/Ln23Be2OuyA?utm_source=unsplash&utm_medium=referral&utm_content=creditShareLink)'
  focal_point: Smart
summary: Implementing trajectory analysis methods in single-cell RNAseq data
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
---
I spent this past summer working as an intern at [Celsius Therapeutics](https://celsiustx.com) investigating the very open problem of lineage reconstruction and trajectory analysis. 
  
The processes of cell proliferation, differentiation, and specification are extremely important for the proper development of a tissue, organ, and organism. Therefore, understanding how these processes are misregulated in disease is of particular interest as this information can be harnessed for drug development and therapies. TI methods leverage data from thousands of single cells to reconstruct lineage paths and infer the order of cells along developmental trajectories.

Since their start, 70+ trajectory inference (TI) methods have been developed each, of course, with its own characteristics. These methods have been successful at recapitulating trajectories for cells in several developmental contexts. As part of the data science team, I was specifically interested in applying TI methods to identify branching fate decisions in the case of disease.

My objective was to survey existing TI methods, select a handful to benchmark, and subsequently apply those on both public and in-house data. The ultimate goal being to have a pipeline for implementing these algorithms to company data. 
