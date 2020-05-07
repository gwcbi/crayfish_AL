### Step 6: Bayesian Tree Estimation with BEAST

> Reflection: How is this different from the maximum-likelihood tree? Why are we estimating both?

Note: BEAST has fantastic online documentation. For more details on the software and additional tutorials, reference their docs [here](https://beast.community/index.html). Here, we will be running BEAST using the [CIPRES Science Gateway](http://www.phylo.org), but we need to download the BEAST package to complate data preparation steps.

#### Step 1: Make the BEAST XML file using BEAUTI.

1. Install BEAST. Instructions are here for [Mac](https://beast.community/install_on_mac) and [Windows](https://beast.community/install_on_windows).
2. Open BEAUti and select `Import Data` from the `File` menu. Select your alignment FASTA file.

<br>![img1](/images/beast1.png) <br>

You can view your alignment by selecting `View Partition`.

<br>![img2](/images/beast2.png)<br>

3. Go to the `Sites` tab and select your substitution model.

<br>![img3](/images/beast3.png)<br>

Based on our PartitionFinder2 results, we may have to substitute our models with base models available. Check out this [blog post](BEAST_DNA_sub_models.pdf) by Justin C. Bagley to choose the appropriate models.

4. On the `Trees` tab, select `Speciation: Yule Process` as the Tree Prior.

<br>![img4](/images/beast4.png)<br>

5. Next, click `Generate BEAST File...` and save your file with a `.xml` extension.

<br>![img5](/images/beast5.png)<br>


#### Step 2: Run BEAST in CIPRES.

1. Upload your `.xml` file to CIPRES under your `Data` folder.
2. Create a new task with your `.xml` file as Input, `BEAST on XSEDE` as Tool, and with default parameters. Click `Save and Run`.

<br>![img6](/images/beast6.png)<br>

3. When your BEAST run finishes, go to Output and download the file ending in `.trees`.

#### Step 3: Build the tree in TreeAnnotator.
BEAST generates many trees during analysis. We will now combine these trees into one "consensus" tree, called a Maximum Clade Credibility (MCC) tree.

1. From your BEAST download, open TreeAnnotator. Import your tree file from BEAST as `Input Tree File`. Then, click `Specify the burnin as the number of states` and enter 1,000,000 (10% of the length of the MCMC chain, which was 10,000,000). Then, enter a filename ending in `.mcc.tre` in the `Output File` box. Click run.

<br>![img7](/images/beast7.png)<br>

You should see a progress screen now:

<br>![img8](/images/beast8.png)<br>

2. The output file will be written to the directory from which you uploaded the input tree file. Opening, you'll see a NEXUS formatted tree file.

<br>![img9](/images/beast9.png)<br>

This file can now be taken into iTOL or FigTree and annotated!

<br>![img10](/images/beast10.png)<br>


> Reflection: Upload your tree into iTOL or FigTree. Does it look similar to the ML tree? If not, what is different?




