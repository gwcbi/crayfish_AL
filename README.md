# crayfish_AR
<br/>

![crayfish](/images/crayfish.jpg)

## Arkansas Crayfish Project
Here is an overview of the tasks that need to be completed for the phylogenetic analysis of the crayfish samples from Arkansas.
This workflow starts with a fasta file of sequences and ends up with appropriate trees.

1) Rename the samples. Copy the current names to the descriptions (using batch rename), and then make the name `genus_species_#` where # is a unique number we have given them that corresponds to the shared voucher number that the 16S and COI gene share.
2) For each of the genes, export all of the files as a fasta file, and then [align the data using MAFFT](mafft.md). Export the COI gene as 'crayfishCOI.fasta' and the 16S gene as `crayfish16S.fasta`.
* note: you should do a separate alignment for each of the the genes before trimming and concatenating the alignments
2) Trim the alignment in MEGA or geneious-- You should trim off the primers that were used to generate the sequences, as well as the ends of sequences that are much longer than any other sequences--anything that is not phylogenetically useful.
3) Concatenate alignments of the two genes using Geneious. Since the two alignments have the same names, you should be able to concatenate all of them at the same time. Export the alignments in Phylip, nexus, fasta, clustal or MSF format (check the method you are using next to see what the preferred format is.
4) Partition the concatenated data and estimate the model of evolution using [PartitionFinder2](partitiondfinder.md)
6) Estimate a tree using maximum likelihood, usually [RaxML](raxml.md) or [IQ-tree](http://iqtree.cibiv.univie.ac.at/)
7) Estimate a tree using Bayesian analysis using [BEAST](BEAST.md)
8) Evaluate your tree

GREAT JOB!
