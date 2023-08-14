## Heatmaps 

Heatmaps are a common visulisation tool for genomic data but somethimes hard to interpret. 

Typically for expression data you might visulise 
  1. Z-Score
    - centre and scale the row data by standard deviation (i.e a row = a single gene, columns = its value across all samples)
    - rather  then plotting the actual abundance values you are plotting the z-score (thier std deviation from the mean)
    - colors represent how much the data divergens from the mean
2. the Log values of data
   - will show you how much a gene in a sample diverges from that sample - can interpret the log2 fold change (https://support.bioconductor.org/p/109594/)
   


Packages 
  - R
      - pheatmap
      - complexheatmap
  - Python
      - seaborn clustermap
   
