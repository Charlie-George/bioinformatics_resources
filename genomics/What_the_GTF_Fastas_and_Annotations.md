
## What The GTF! Fasta Files and Annotations - all you need to know....

In order to analyse your genomics data whether its RNA-seq, Chip-seq atac-seq, whole genome sequencing,
exome, sequencing whatever you to take the files that contain the information about your raw reads (the Fastq files)
and find where in the genome or transcripts your reads are comming from. 

In order to do this you need to have a reference genome or transcripts to 'map' these reads to. However getting the genome and annotations that most suit your purposes is not always easy, infact for beginners its often terribly confusing, becuase there are different places that you can get your genomes or annotations from and these come in different formats. Quite often on shared systems the bioinformatics gropus will have nicely processes and cleaned up the annotations and genomes for users, which is great, but there is often limited documentation on how this was done and often, key chromsomes or regions might have been filtered out. For examples the mitochoindrial genome or chrY or random contigs (genes or regions that they can't find which chromosome they came from).  

https://genestack.com/blog/2016/07/12/choosing-a-reference-genome/#:~:text=Masked%20reference%20genomes%20are%20also%20known%20as%20hard%2Dmasked%20DNA%20sequences.&text=In%20soft%2Dmasked%20reference%20genomes,the%20base%20(e.g.%20acgt).

### Whats the difference beween a Fasta File and a GTF or GFF File - which one contains the genome? 

- A Fasta file is a file which contains the actual sequence information of a region e.g. ATACGACTACGA e.g. the human reference genome hg38 or hg19 - this is often refered to as your 'Genome file' 

- A GTF or GFF is a tabular file, with several collumns that contains the locations of features of interest - e.g. your annotations of transcripts, genes, exons, introns. We often refer to this as your 'Annotations File'. It does not contain any information about the actual bases or sequence of those Annoations, only the location (chromosome, start, stop, strand) and metadata about which consortium annoated that annotation and what that annotation region represents (e.g. exon, UTR, gene etc) 

### How can I check if my genome or GTF file is the origional download or has been filtered 

### Where can I get the origionals from 

### What is the difference between Ensembl and UCSC fasta files and GTF files - is one better? 

### What do I do if i want to use the UCSC fasta file but Ensembl GTF Annotations 
