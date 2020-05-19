## Step 3: Partition the Concatenated Dataset

1. Read and review PartitionFinder2 [documentation](http://www.robertlanfear.com/partitionfinder/assets/Manual_v2.1.x.pdf). 
PartitionFinder2 is a program for selecting best-fit partitioning schemes and models of evolution for nucleotide, amino acid, and morphology alignments. 

> Reflection:
> 
> Why are we partitioning the dataset?
<br/>

1. Create an account and log in to the [CIPRES Science Gateway](https://www.phylo.org/portal2/login!input.action).

2. Click `Create New Folder` and enter a title and description for your analysis.

![partition01](/images/partition01.png)

3. Go to your `Data` Subfolder and choose `Upload/Enter Data`. Upload the alignment file in Phylip format. When you export the alignment in Geneious, make sure to export it in FASTA and Phylip format. 

![partition02](/images/partition02.png)

You also need to upload your configuration file, which specifies the path of your input file, branch length linkage, model selections, and data blocks. It should appear as so:

```
## ALIGNMENT FILE ##
alignment=infile.phy;

## BRANCHLENGTHS: linked | unlinked ##
branchlengths = linked;

## MODELS OF EVOLUTION: all | allx | mrbayes | beast | gamma | gammai |
models = all;

# MODEL SELECCTION: AIC | AICc | BIC #
model_selection = aicc;

## DATA BLOCKS: see manual for how to define ##
[data_blocks]
COI_1stpos = 1-597\3;
COI_2ndpos = 2-597\3;
COI_3rdpos = 3-597\3;
16S         = 598-1031;

## SCHEMES, search: all | user | greedy | rcluster | rclusterf | kmeans ##
[schemes]
search = all;

```
>Reflection:

>What are some settings your may want to change? Why is COI partitioned differently than 16S?

4. Go to your `Tasks` subfolder and create a new task with your alignment as input and `PartitionFinder2 on XSEDE` as the tool. 

![partition03](/images/partition03.png)

5. Under `Input Parameters` go to `Select cfg file ` and choose your .cfg file. Click `Save and Run Task`. When your job has finished, you will get an email. 

![partition04](/images/partition04.png)

6. Download the `analysis.zip` file and observe the `best_scheme.txt` text file and you can see the best models for each partition.

![partition05](/images/partition05.png)

>Reflection: How did the GTR model (often used as a default on RAxML) perform relative to the best model? Did all three criteria choose the same model?

>Reflection: What do the G and I terms in some of the model names mean? Why is this important?

We are now ready to estimate trees using [RAxML-NG](raxml.md)
