
# This file contains ATAc-Seq resorces 

## Introductory overviews

Overview of experimental and computational considerations for ATAC-seq analysis - good but a bit brief in places, doesn't go into alot of bioinformatic detail
[link](https://informatics.fas.harvard.edu/atac-seq-guidelines.html)



## Lab protocols 

An improved ATAC-seq protocol reduces background and enables interrogation of frozen tissues 
[nature methods paper](https://www.nature.com/articles/nmeth.4396): 

- dounce homogenise
- density gradient centrifugation 

Human brain ATAC

https://www.nature.com/articles/nmeth.4396


## Bioconductor Packages 

**esATAC**

Wei Z, Zhang W, Fang H, Li Y, Wang X (2018). “esATAC: an easy-to-use systematic pipeline for ATAC-seq data analysis.” Bioinformatics. doi: 10.1093/bioinformatics/bty141. 
https://www.bioconductor.org/packages/release/bioc/html/esATAC.html

- esATAC easy to use ATAC-seq pipeline - wraps alot of other R packages in an easy to use workflow - from what I see it tend to merge all fastqc of a partivcular replicate at the beginning and then carries them downstream 
- does not include IDR 
- uses chipseeker for annotation
- uses enrichGO from clusterprofiler 
- also uses motif matcher
- does footprinitng and cutsite analysis 
- uses F-seq for peakcalling 

**Chipseeker**

- annotate peaks
- compare replicates 
- coverage plot over chromosomes 

**ATACSeqQC**

- atacseq qc plots
- proportion of fragment lengths in library
- nucleosome phasing 
- heatmap of fragment locations 

Normalisation between replicates 



