
Deseq2 PCA 
- https://support.bioconductor.org/p/100069/
- https://support.bioconductor.org/p/71899/

- does not scale the data -> rlog and vst should have already taken care of the variance, setting variance to =1 will cause bad noise/signal 

- normalisatin to size factos occurs 
