# crayfish_AR
<br/>

![crayfish](/images/crayfish.jpg)

## Arkansas Crayfish Project
Here is an overview of the tasks that need to be completed for the phylogenetic analysis of the crayfish samples from Arkansas.
This workflow starts with a fasta file of sequences and ends up with appropriate trees.

1) For each of the genes, export all of the files as a fasta file, and then [align the data using MAFFT](mafft.md).
* note: you should do a separate alignment for each of the the genes before trimming and concatenating the alignments
2) Trim the alignment-- You should trim off the primers that were used to generate the sequences, as well as the ends of sequences that are much longer than any other sequences--anything that is not phylogenetically useful.
3) Concatenate alignments of the two genes using Geneious. Export the alignments in Phylip, nexus, fasta, clustal or MSF format (check 
4) Select the model you should use with [jModeltest](modeltest.md)
5) Estimate a tree using maximum likelihood, usually [RaxML](raxml.md) or [IQ-tree](http://iqtree.cibiv.univie.ac.at/)
6) Estimate a tree using Bayesian analysis using [BEAST](BEAST.md)
7) Evaluate your tree

GREAT JOB!
