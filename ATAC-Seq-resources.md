
# This file contains ATAc-Seq resorces 

## Introductory overviews

Overview of experimental and computational considerations for ATAC-seq analysis - good but a bit brief in places, doesn't go into alot of bioinformatic detail
[link](https://informatics.fas.harvard.edu/atac-seq-guidelines.html)



## Lab protocols 

An improved ATAC-seq protocol reduces background and enables interrogation of frozen tissues 
[nature methods paper](https://www.nature.com/articles/nmeth.4396): 

- dounce homogenise
- density gradient centrifugation 


**Omni-chip** - imporoved method - used for human brain slices, do nuclear extract 
https://www.nature.com/articles/nmeth.4396



## Bioconductor Packages 

**esATAC**

Wei Z, Zhang W, Fang H, Li Y, Wang X (2018). “esATAC: an easy-to-use systematic pipeline for ATAC-seq data analysis.” Bioinformatics. doi: 10.1093/bioinformatics/bty141. 
https://www.bioconductor.org/packages/release/bioc/html/esATAC.html

- esATAC easy to use ATAC-seq pipeline - wraps alot of other R packages in an easy to use workflow - from what I see it tend to merge all fastqc of a partivcular replicate at the beginning and then carries them downstream 
- does not include IDR 
- uses chipseeker for annotation
- uses enrichGO from clusterprofiler for GO enrichment
- also uses motif matcher
- does footprinitng and cutsite analysis 
- generates cutsites and filters nucleosome free fragments <100bp
- uses F-seq for peakcalling 


**Chipseeker**

- annotate peaks
- compare replicates 
- coverage plot over chromosomes 

**ATACSeqQC**

Ou J, Liu H, Yu J, Kelliher MA, Castilla LH, Lawson ND, Zhu LJ (2018). “ATACseqQC: a Bioconductor package for post-alignment quality assessment of ATAC-seq data.” BMC Genomics, 19(1), 169. ISSN 1471-2164, doi: 10.1186/s12864-018-4559-3, https://doi.org/10.1186/s12864-018-4559-3. 

Generates QC plots for ATAC-Seq samples 
- IGV snapshot function of specific regions
- library complexity - distinct fragments versus putative sequenced fragments 
- frag size distribution & nucleosome phasing plot
- shift reads for peakcalling and footprinting 
- coverage of promoter/coverage of transcript body
- NFR score - ratio between cut sifnal adjacent to TSS: 
- nucleosome-free, mononucleosome, di nucleosome, trinucleosome fractions 
    - uses random forest to classify fragments 
      - top 10% reads <100bp = nucleosome free
      - top 10% of reads 180-247bp = mononucleosomes
      - this is the training set to classify the rest using randon forest - number of the three is 2*sqrt(len(training_set))
      - conservation score can also be inclused 
 - heatmap and coverage curve for nucleosome possitions
   - average signal across all active TSSs 
        - nuc free fragements enriched at TSS
        - nucleosome bound fragments at upstream and downstream of TSS 
 -factor footprints does not take conservation into account (centipede = an alternative)
 - V plot - distance to binding sites 

### Footprinting


 - **centerpede**:
    takes PhyloP into account 


Basic experimental and computational atac-seq overview
https://informatics.fas.harvard.edu/atac-seq-guidelines.html






