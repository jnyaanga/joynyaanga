---
title: Model selection and its many trials
author: Joy Nyaanga
date: '2021-05-17'
slug: model-selection
categories:
  - research
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2021-05-17T07:18:14-05:00'
featured: no
image:
  caption: '[Photo by Issac Smith on Unsplash](https://unsplash.com/photos/6EnTPvPPL6I?utm_source=unsplash&utm_medium=referral&utm_content=creditShareLink)'
  focal_point: ''
  preview_only: no
projects: [growth-and-dev]
---
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />

Model selection is the process of selecting one statistical model from a set of many candidate models. It seems relatively straightforward in principal but in practice (especially with noisy experimental data) it can be challenging.  

My research is focused on understanding how organisms coordinate developmental progression and growth rate to reach an appropriate adult size. To understand how this is achieved in *C. elegans*, I must first examine how *C. elegans* grow. Two general models were proposed for *C. elegans* growth in volume: linear and exponential.   
  
> It is important to note that these volume growth models require different dynamics in length and width. 
>  - For **linear volume growth**, length and width must increase at precise sublinear rates that together result in a linear increase in volume. 
>  - If animal length and width increased at a constant linear rate, then volume would increase at a **cubic rate**. 
>  - If both length and width grew exponentially, then volume would fit an **exponential model**.  

I sought to identify which model best described *C. elegans* growth behavior. To start I fit linear, exponential, and cubic functions to the data using least-squares regression. I do this for all 4 larval stages: L1, L2, L3, and L4. You will notice that L1 was further divided into two sections, this is due to the small volume drop we observe mid stage. 


```
linear <- lm(volume~hour)
exponential <- nls(volume~ I(exp(1)^(m*hour + b)), start = list(m = 0.08, b = 5))
cubic <- lm(volume~poly(hour, degree = 3))
```
<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

Given these fits, its time for model selection! I used Akaike’s information criterion (AIC) and Bayesian information criterion (BIC) as goodness of fit criteria to evaluate the candidate models. In short, I want to find the model with the smallest AIC/BIC and compare it to the other candidate models 
 > If the delta value was greater than 6, the model with the smallest AIC/BIC value was denoted as the best model. If the delta value was less than 6 but greater than 2, the model with the smallest AIC/BIC value was determined to likely be the best model. If the delta value was less than 2, we are unable to distinguish the model of best fit.

<table class=" lightable-classic" style='font-family: "Arial Narrow", "Source Sans Pro", sans-serif; width: auto !important; margin-left: auto; margin-right: auto;'>
<thead>
<tr>
<th style="empty-cells: hide;" colspan="1"></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="3"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">AIC</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="3"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">BIC</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="3"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Delta_AIC</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="3"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Delta_BIC</div></th>
<th style="empty-cells: hide;" colspan="2"></th>
</tr>
<tr>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Stage</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Linear</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Exponential</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Cubic</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Linear</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Exponential</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Cubic</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Linear</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Exponential</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Cubic</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Linear</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Exponential</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Cubic</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Best model by AIC</div></th>
<th style="padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #111111; margin-bottom: -1px; ">Best model by BIC</div></th>
</tr>
</thead>
<tbody>
  <tr>
   <td style="text-align:center;"> L1.1 </td>
   <td style="text-align:center;"> 138159 </td>
   <td style="text-align:center;"> 138163 </td>
   <td style="text-align:center;"> 138142 </td>
   <td style="text-align:center;"> 138179 </td>
   <td style="text-align:center;"> 138184 </td>
   <td style="text-align:center;"> 138175 </td>
   <td style="text-align:center;"> 17 </td>
   <td style="text-align:center;"> 21 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 9 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> Cubic </td>
   <td style="text-align:center;"> Likely Cubic </td>
  </tr>
  <tr>
   <td style="text-align:center;"> L1.2 </td>
   <td style="text-align:center;"> 193414 </td>
   <td style="text-align:center;"> 193416 </td>
   <td style="text-align:center;"> 193412 </td>
   <td style="text-align:center;"> 193435 </td>
   <td style="text-align:center;"> 193437 </td>
   <td style="text-align:center;"> 193447 </td>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 2 </td>
   <td style="text-align:center;"> 12 </td>
   <td style="text-align:center;"> Can't distinguish </td>
   <td style="text-align:center;"> Can't distinguish </td>
  </tr>
  <tr>
   <td style="text-align:center;"> L2 </td>
   <td style="text-align:center;"> 189190 </td>
   <td style="text-align:center;"> 189091 </td>
   <td style="text-align:center;"> 189048 </td>
   <td style="text-align:center;"> 189211 </td>
   <td style="text-align:center;"> 189111 </td>
   <td style="text-align:center;"> 189083 </td>
   <td style="text-align:center;"> 142 </td>
   <td style="text-align:center;"> 43 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 128 </td>
   <td style="text-align:center;"> 28 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> Cubic </td>
   <td style="text-align:center;"> Cubic </td>
  </tr>
  <tr>
   <td style="text-align:center;"> L3 </td>
   <td style="text-align:center;"> 211208 </td>
   <td style="text-align:center;"> 210979 </td>
   <td style="text-align:center;"> 210834 </td>
   <td style="text-align:center;"> 211229 </td>
   <td style="text-align:center;"> 211000 </td>
   <td style="text-align:center;"> 210869 </td>
   <td style="text-align:center;"> 374 </td>
   <td style="text-align:center;"> 145 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 360 </td>
   <td style="text-align:center;"> 131 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> Cubic </td>
   <td style="text-align:center;"> Cubic </td>
  </tr>
  <tr>
   <td style="text-align:center;"> L4 </td>
   <td style="text-align:center;"> 183027 </td>
   <td style="text-align:center;"> 183067 </td>
   <td style="text-align:center;"> 183023 </td>
   <td style="text-align:center;"> 183047 </td>
   <td style="text-align:center;"> 183087 </td>
   <td style="text-align:center;"> 183057 </td>
   <td style="text-align:center;"> 4 </td>
   <td style="text-align:center;"> 44 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 0 </td>
   <td style="text-align:center;"> 40 </td>
   <td style="text-align:center;"> 10 </td>
   <td style="text-align:center;"> Likely Cubic </td>
   <td style="text-align:center;"> Linear </td>
  </tr>
</tbody>
</table>

As you can see, it is difficult to consistently distinguish between linear, exponential, and cubic models using statistical information criterion because of the similarity in the shapes of the growth curves. This is not entirely surprising as it is well understood that distinguishing between linear and exponential growth requires [highly accurate measurements](https://doi.org/10.1038/nmeth.1452). From these results, however, one could conclude that volume growth likely proceeds at a rate faster than linear. This is particularly interesting as [recent work](https://doi.org/10.1101/2021.03.24.436858) has suggested that *C. elegans* do in fact grow at a rate faster than linearly within larval stages. 
