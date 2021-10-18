---
title: 'R + Python: The best of both worlds'
author: Joy Nyaanga
date: '2021-07-28'
slug: r-python
categories: 
  - R
  - Python
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2021-07-28T20:51:42-05:00'
featured: no
image:
  caption: '[Photo by James Harrison on Unsplash](https://unsplash.com/photos/vpOeXr5wmR4)'
  focal_point: ''
  preview_only: no
projects: []
---
'R' you ready for some Python??  
  
Over the last few weeks I've been immersed in an internship where I've learned a **TON** about single cell genomics, trajectory inference methods, and Python. I'll leave the fun details for another post but here I wanted to share something I've recently learned that's been quite the game changer...
  
The first programming language I learned that opened me up to the wide world of computational biology was Python. Over the last few years, however, I transitioned into an avid R user. I've always held the misconception that the two languages were entirely independent, not easily integrated into a single analysis notebook. But thanks to RStudio, this is not true!!
  
The *reticulate* R package provides a comprehensive set of tools for interoperability between R and Python.  
  

```r
library(reticulate)
```

Now, as usual, I can run some R code --  

```r
#```{r}
some_R <- 'Hello World!'
print(some_R); class(some_R)
```

```
## [1] "Hello World!"
```

```
## [1] "character"
```
  
But with *reticulate*, I can also run some Python code --  

```python
#```{python}
some_Python = 'Good Morning!'
print(some_Python); type(some_Python)
```

```
## Good Morning!
## <class 'str'>
```
  
    
## Accessing objects between languages  
Objects in either language can be accessed in the other language thanks to the *reticulate* package.

Use R to call a variable made in Python:  

```r
# ```{r}
py$some_Python
```

```
## [1] "Good Morning!"
```
  
Use Python to call a variable made in R:  

```python
# ```{python}
r.some_R
```

```
## 'Hello World!'
```
  
    
## Converting objects between languages
**NOTE**: When calling variables between environments using 'r.' and 'py$', the *reticulate* package translates the data type from one environment to another data type of the other environment. For example, a named list in R will be translated into a Python dictionary. 
  
<img src='images/conversions.png' alt='Data type conversions'>  
  
Besides simply accessing objects, you can also convert an R object into a Python object while still running R with ***r_to_py***.


```r
# ```{r}
# creating an R vector
rvector <- c(1,2,3,4,5)

# converting vector to Python list
rvector_converted <- r_to_py(rvector)
class(rvector); class(rvector_converted)
```

```
## [1] "numeric"
```

```
## [1] "python.builtin.list"   "python.builtin.object"
```
  
    
## Running a Python code chunk in R  
There may be times when you want to run a code chunk written in Python within R. In this case, the ***py_run_string*** function from *reticulate* comes in handy. This function runs the Python code and saves the results into the Python environment. These results can then be accessed using 'py$' as before.  


```r
#```{r}
py_run_string("import numpy as np")
py_run_string("pyrun = np.array(range(5))")

py$pyrun
```

```
## [1] 0 1 2 3 4
```

Likewise, ***py_run_file*** allows you to run entire Python scripts in R.  
  
And that's it! Keeping it short and sweet for this one. In a later post I'll showcase a bit more of the integration of R and Python in the genomics analysis I've recently learned.












