# Bioinformatics resources

This repository collects various helpful links, training materials, courses, code snippets and information for all things computational biology...

I have used many of these sites myself to learn or have across them when looking for good teaching materials and have collated them here not only as a useful reminder to  myself but also as helpful resource to those starting out on their journey into bioinformatics, genomics, programming and computational biology.

There is a lot of overlap between sections but links are split into broad sections

# Genomics/Bioinformatics Focused resources

## General Genomics resources/tools

### Tutorials/Course Materials
- Bioconductor resources
  - [Bioc2020 conference resources](http://bioc2020.bioconductor.org/)
        - overview of bioconductor
        - recorded workshops and vignettes (beginner to advanced) on key bioconductor packages (e.g. annotations) as well as more specific single cell, HiC packages
        - Keynote lectures and short talks on recent developments in field
- [Biostars Handbook](https://www.biostarhandbook.com/) - Introductory guide to bioinformatics, giving overview of theory and step by step instructions for getting started with many bioinformatic tasks and analysis
- Curated list of bioinformatic resources from [Edinburgh XDF fellowship programme](https://www.ed.ac.uk/cross-disciplinary-fellowships/training-resources)
- [Harvard Chan Bioinformatic Core training repository](https://github.com/hbctraining) and [website](https://hbctraining.github.io/main/)- introductory tutorials to several bioinformatic topics (ATAC-seq, RNA-seq, scRNA-seq)
- [CSAMA](https://www.huber.embl.de/csama2020/#home) - Intermediate course focusing on statistical analysis of genomic datasets
- [Hemberg lab scRNA-seq course](https://scrnaseq-course.cog.sanger.ac.uk/website/index.html)
- [EMBL-EBI online training resources](https://www.ebi.ac.uk/training/online/) - introductory courses covering the use of many online databases and resourses
- [Stats Quest Videos](https://www.youtube.com/channel/UCtYLUTtgS3k1Fg4y5tAhLbw) Small but thorough video tutorials on many statistical concepts related to genomics and broader statistical concepts - has nice deseq2 and edgeR explainers e.g. [deseq2 library normalisation](https://www.youtube.com/watch?v=UFB993xufUU)
- [Modern Statistics for Modern Biology](https://www.huber.embl.de/msmb/) By Susan Holmes and Wolfgang Huber - Excellent beginner to intermediate statistical concepts that are geared towards biological problems - These are  two top experts in the field of statistics and biological data science, this book really is a must read.
- [MIT Deep Leanring in the Life Sciences Course Materials](https://mit6874.github.io/)
- [Harvard Introdution to Bioinformatics and Computational Biology by Shirley Liu](https://liulab-dfci.github.io/bioinfo-combio/) - An amazing collection of lectures by Shirley Liu, one of the world leaders in bioinformatics, covering fundamental and key algorithmns in the field in excellent detail. 

### Lecture series
- Broad Institute [Models Inference and Algorithms meeting](https://www.broadinstitute.org/scientific-community/science/mia/models-inference-algorithms)
- Broad Institute [Other uploads](https://www.youtube.com/user/broadinstitute/videos?view=0&sort=dd&shelf_id=10)

## More specific genomic applications/fields

### Genome Browsers for visualising genomic data
- [Washu genome browser](http://epigenomegateway.wustl.edu)
- [IGV](http://software.broadinstitute.org/software/igv/)
- [UCSC](https://genome.ucsc.edu/)
- [awesome-expression-browser repository](https://github.com/federicomarini/awesome-expression-browser)

### Genomes and Annotations
- [GTFs and Fasta files](./genomics/What_the_GTF_Fastas_and_Annotations.md)


### Single cell
- Repository collecting single cell tools - [awesome-single-cell](https://github.com/seandavi/awesome-single-cell)

### ATAC-Seq
- [My list of useful ATAC-Seq resources](./genomics/ATAC-Seq-resources.md)

### ChIP-Seq

# General Datascience

- [General data science topics](https://towardsdatascience.com/) - general data science website with interesting articles relating to all things data science, lots of machine learning topics
- [datacamp](https://www.datacamp.com/) - various online courses covering a broad range of data science topics - many introductory

# General Programming
### Linux and command line
- [Linux Foundation Course](https://www.edx.org/course/introduction-to-linux) - Through intro to linux and command line
### R resources
- [**R for data science**](http://r4ds.had.co.nz/) - Introductory book that covers R, Rstudio, Tidyverse for data wrangling, plotting in ggplot, general data science approaches and methods.
- [Software carpentry R for genomics](https://datacarpentry.org/genomics-r-intro/) - basic r introductory course
- [rstudio webinars](https://rstudio.com/resources/webinars/) - webinars on various topics related to R and rstudio
- [R graph gallery](https://www.r-graph-gallery.com/) - gallery of various R-based graphs and how to make them
- [ggplot extensions gallery](https://exts.ggplot2.tidyverse.org/gallery/) - nice overview of ggplot extensions you can use - good for plotting inspiration

### Python
- [Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/) very detailed textbook on using python for datascience, includes: ipython, numpy, pandas, matplotlib and scikit learn for machine learning
- [Python graph gallery](https://python-graph-gallery.com/) - gallery of various python-based graphs and how to make them
- [equivalent of setting PYTHONPATH so conda installs of python can access your own repos](./conda/Add_directories_to_conda_python_path.md)

# Statistics
- [The Art of Statistics: Learning from Data](https://www.amazon.co.uk/Learning-Data-Statistics-Pelican-Books/dp/0241258766/ref=sr_1_1?adgrpid=66294937627&dchild=1&gclid=CjwKCAjw_JuGBhBkEiwA1xmbRX7ccFq7iH3r3Vk5YQtechuGGdJoNUzpZWjstl00Td1BL7q1Vhy6rhoCVDMQAvD_BwE&hvadid=318278936635&hvdev=c&hvlocphy=1006457&hvnetw=g&hvqmt=e&hvrand=1773382778919080832&hvtargid=kwd-656409493610&hydadcr=11438_1841583&keywords=art+of+statistics&qid=1623678011&sr=8-1)By David Spiegelhalter - A short general book on the importance of visulising data and many key statistical concepts that crop up time and time again in biological data science - a really good and interesting read to those a bit rusty in statistics 
- [Modern Statistics for Modern Biology](https://www.huber.embl.de/msmb/) By Susan Holmes and Wolfgang Huber - Excellent beginner to intermediate statistical concepts that are geared towards biological problems - These are  two top experts in the field of statistics and biological data science, this book really is a must read.
- [Think Stats](http://greenteapress.com/thinkstats/)
- [Think Bayes](http://www.greenteapress.com/thinkbayes/html/index.html)
- [Stats Quest Videos](https://www.youtube.com/channel/UCtYLUTtgS3k1Fg4y5tAhLbw) Small but thorough video tutorials on many statistical concepts related to genomics and broader statistical concepts - has nice deseq2 and edgeR explainers e.g. [deseq2 library normalisation](https://www.youtube.com/watch?v=UFB993xufUU)

# Graphs/Visulisation
  - [Chartmaker](https://chartmaker.visualisingdata.com/) - summary of different types of plot and how to make them using different software
  - [Python graph gallery](https://python-graph-gallery.com/) - gallery of various python-based graphs and how to make them
  - [R graph gallery](https://www.r-graph-gallery.com/) - gallery of various R-based graphs and how to make them
  - [ggplot extensions gallery](https://exts.ggplot2.tidyverse.org/gallery/) - nice overview of ggplot extensions you can use - good for plotting inspiration

# Machine learning
- [Python Machine Learning](https://www.packtpub.com/product/python-machine-learning-third-edition/9781789955750) by Sebastian Raschka and Vahid Mirjalili -> Nice introductory textbook going over the fundamentals of machine learning concepts, algorithmns and using the Python scikit learn library
- [Encoding of categorical variables](./machine_learning/encoding.md)
- [MIT Deep Leanring in the Life Sciences Course Materials](https://mit6874.github.io/)

# Other useful software
- Git
- Conda
- tmux
    - [intro to tmux](https://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/) - brief 2 minute guide to getting started with tmux a program you can run in a server that keeps your terminal (and the processes in it open) even if your ssh connection to the server drops 
- Atom - a text editor you can use to write scripts for R, python or any text document.
    [atom guide](https://flight-manual.atom.io/) - guide to getting started with atom text editor

# Resources for teaching bioinformatics
- [Ten quick tips for teaching with participatory live coding](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1008090)

# My notes for my own computer setup 
These notes are pretty rough and mainly for my own use so bare with them... 
- [Useful Software to setup on new computer](./computer_setup/computer_setup.md)
- [How to add own directories to equivalent of PYTHONPATH so conda installs of python can access your own repos](./computer_setup/Add_directories_to_conda_python_path.md)
- [Setting up cgatpipelines on new cluster](./computer_setup/cgatpipelines_on_new_cluster.md)
    - [Transfer data between computers/clusters using rsync](./computer_setup/rsync.md)
