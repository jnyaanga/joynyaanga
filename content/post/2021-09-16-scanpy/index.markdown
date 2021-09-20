---
title: 'Analyzing single cell data using scanpy'
author: Joy Nyaanga
date: '2021-09-16'
slug: scanpy
categories: 
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2021-09-16T20:51:42-05:00'
featured: no
image:
  caption: '[Photo by National Cancer Institute on Unsplash](https://unsplash.com/photos/bwMhq_itmMU?utm_source=unsplash&utm_medium=referral&utm_content=creditShareLink)'
  focal_point: ''
  preview_only: no
projects: [trajectory-inference]
---




```python
import numpy as np
import pandas as pd
import scanpy as sc
```


```python
pbmc = sc.read_10x_mtx('filtered_gene_bc_matrices/hg19/',
                       var_names = 'gene_symbols',
                       cache = True)
```


```python
pbmc.var_names_make_unique()
```


```python
pbmc
```

```
## AnnData object with n_obs × n_vars = 2700 × 32738
##     var: 'gene_ids'
```

### Pre-processing: QC

Identify mitochondiral specific genes


```python
pbmc.var['mt'] = pbmc.var_names.str.startswith('MT-') 
sc.pp.calculate_qc_metrics(pbmc, qc_vars=['mt'], percent_top=None, log1p=False, inplace=True)
```

Visualize the QC metrics


```python
sc.pl.violin(pbmc, ['n_genes_by_counts', 'total_counts', 'pct_counts_mt'],
             jitter=0.4, multi_panel=True, size = 1.5)
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="1440" />


```python
sc.pl.scatter(pbmc, x='total_counts', y='pct_counts_mt')
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-8-3.png" width="772" />

```python
sc.pl.scatter(pbmc, x='total_counts', y='n_genes_by_counts')
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-8-4.png" width="772" />

Filter out cells that have <200 or > 2500 genes.


```python
sc.pp.filter_cells(pbmc, min_genes = 200)
sc.pp.filter_cells(pbmc, max_genes = 2500)
pbmc = pbmc[pbmc.obs.pct_counts_mt < 5, :]
```


```python
pbmc
```

```
## View of AnnData object with n_obs × n_vars = 2638 × 32738
##     obs: 'n_genes_by_counts', 'total_counts', 'total_counts_mt', 'pct_counts_mt', 'n_genes'
##     var: 'gene_ids', 'mt', 'n_cells_by_counts', 'mean_counts', 'pct_dropout_by_counts', 'total_counts'
```

### Normalize & log-transform


```python
sc.pp.normalize_total(pbmc, target_sum=1e4)
```

```
## /Users/joy/miniconda3/lib/python3.9/site-packages/scanpy/preprocessing/_normalization.py:155: UserWarning: Revieved a view of an AnnData. Making a copy.
##   view_to_actual(adata)
```


```python
sc.pp.log1p(pbmc)
```

### Feature Selection


```python
sc.pp.highly_variable_genes(pbmc, min_mean=0.0125, max_mean=3, min_disp=0.5)
sc.pl.highly_variable_genes(pbmc)
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-13-7.png" width="1344" />


```python
# filter to keep only HVGs
pbmc = pbmc[:, pbmc.var.highly_variable]
```


```python
pbmc
```

```
## View of AnnData object with n_obs × n_vars = 2638 × 2013
##     obs: 'n_genes_by_counts', 'total_counts', 'total_counts_mt', 'pct_counts_mt', 'n_genes'
##     var: 'gene_ids', 'mt', 'n_cells_by_counts', 'mean_counts', 'pct_dropout_by_counts', 'total_counts', 'highly_variable', 'means', 'dispersions', 'dispersions_norm'
##     uns: 'log1p', 'hvg'
```

### Scale expression


```python
sc.pp.scale(pbmc, max_value = 10)
```

```
## /Users/joy/miniconda3/lib/python3.9/site-packages/scanpy/preprocessing/_simple.py:843: UserWarning: Revieved a view of an AnnData. Making a copy.
##   view_to_actual(adata)
```

### PCA


```python
sc.tl.pca(pbmc, svd_solver='arpack')
sc.pl.pca(pbmc, color='NKG7')
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-17-9.png" width="672" />


```python
# Determining dimensionality
sc.pl.pca_variance_ratio(pbmc, log=True)
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-18-11.png" width="672" />

### tSNE


```python
sc.tl.tsne(pbmc, n_pcs = 10)
sc.pp.neighbors(pbmc, n_neighbors=10, n_pcs=10)
```


```python
sc.pl.tsne(pbmc)
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-20-13.png" width="672" />

### Clustering


```python
sc.tl.leiden(pbmc, resolution = 0.4)
```


```python
sc.pl.tsne(pbmc, color = 'leiden')
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-22-15.png" width="672" />

### Assign cell type identities


```python
new_cluster_names = [
    'Memory CD4 T', 'Naive CD4 T',
    'CD14 Monocytes',
    'B', 'CD8 T',
    'NK', 'FCGR3A Monocytes',
    'DC', 'Platelet']
pbmc.rename_categories('leiden', new_cluster_names)
```

```
## /Users/joy/miniconda3/lib/python3.9/site-packages/pandas/core/arrays/categorical.py:2630: FutureWarning: The `inplace` parameter in pandas.Categorical.rename_categories is deprecated and will be removed in a future version. Removing unused categories will always return a new Categorical object.
##   res = method(*args, **kwargs)
```

```python
pbmc.obs['clusters'] = pbmc.obs.leiden
```


```python
sc.pl.tsne(pbmc, color='clusters', legend_loc='on data')
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-24-17.png" width="672" />











