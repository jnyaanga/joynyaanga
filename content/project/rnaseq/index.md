---
title: RNA-seq - Impact of diet on _C. elegans_ expression patterns 
date: "2021-10-05T00:00:00Z"
external_link: ""
summary: Implementing a bulk RNA-seq pipeline to _C. elegans_ expression data
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""
---
During the fall of 2021, I took a special topics course as part of my graduate program titled "R for Biologists". In it I had the opportunity to dig into the world of bulk RNA-seq analysis. Below I describe my personal project.

# Introduction

As bacterivores, *C. elegans* feed on bacteria that grow on rotting vegetation. Historically, a 
strain of *Escherichia coli*, OP50, was chosen as the standard laboratory diet. While most 
experimental studies use OP50 as the primary food source, the number of bacterial diets used 
to propagate *C. elegans* has expanded in recent years. Another laboratory *E. coli* strain that 
is routinely used is HB101. Although both of these bacterial diets support growth and 
development, the nutritional composition of each is unique, and when fed to *C. elegans*, 
differentially impacts several traits. Research has indicated that animals fed HB101 develop 
faster and are larger than those fed OP50 [1,2,3]. Unsurprisingly, these diet-induced growth 
effects are also accompanied by global changes in gene expression [4]. Characterizing the 
expression changes of *C. elegans* fed differing strains of bacteria expands the understanding 
of diet effects at the molecular level. 

# The data 

Changes in diet can have profound effects on gene expression. Previously, researchers have 
analyzed the transcriptional response of animals fed differing diets [4]. *C. elegans* populations 
were cultured for five days with either *E. coli* OP50 or *E. coli* HB101. Two replicates for each 
diet were included, resulting in four total experimental populations. Total RNA was then 
extracted from these populations, and samples were sequenced using an Illumina NextSeq 
500 sequencing platform. Raw FASTQ sequence files were processed with a bioinformatics 
pipeline. Another recent study also collected expression data of *C. elegans* fed multiple 
bacterial diets [5]. In this study, animals were grown on plates seeded with 
E.coli (OP50, HT115, and HB101) for 48 hours. RNA was extracted, samples were sequenced, 
and read counts were reported in triplicate.

# Objective

I plan to study the publicly available raw FASTQ files during this course. My goal is to 
successfully analyze these data through all steps of an RNAseq bioinformatics pipeline (the 
AndersenLab has such a pipeline). I have considerable experience using R for data 
manipulation and statistical analysis but I have no experience handling sequencing data. 
Through this project I hope to gain a better understanding of how sequencing data can be 
processed and studied using command line and R. From this analysis, I expect to identify 
differentially expressed genes when comparing E. coli OP50 and HB101 diets. I expect many 
of these genes to play a role in metabolic pathways. 
  
**Ultimately, my goal is to gain experience handling and analyzing sequencing data.**

## See final project page [here.](https://rpubs.com/jnyaanga/ibis455final)

### References  
1. So S, Miyahara K, Ohshima Y. Control of body size in C. elegans dependent on food and 
insulin/IGF-1 signal: Body size control in C. elegans. Genes Cells. 2011;16: 639–651.   
2. Soukas AA, Kane EA, Carr CE, Melo JA, Ruvkun G. Rictor/TORC2 regulates fat 
metabolism, feeding, growth, and life span in Caenorhabditis elegans. Genes Dev. 2009;23: 
496–511.  
3. Avery L, Shtonda BB. Food transport in the C. elegans pharynx. J Exp Biol. 2003;206: 
2441–2457.   
4. Schumacker ST, Chidester CAM, Enke RA, Marcello MR. RNA sequencing dataset 
characterizing transcriptomic responses to dietary changes in Caenorhabditis elegans. Data 
Brief. 2019;25: 104006.   
5. Stuhr NL, Curran SP. Bacterial diets differentially alter lifespan and health span trajectories 
in C. elegans, Commun Biol. 2020;653
