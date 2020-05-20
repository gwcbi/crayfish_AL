### Step 6: Bayesian Tree Estimation with BEAST

> Reflection: How is this different from the maximum-likelihood tree? Why are we estimating both?

Note: BEAST has fantastic online documentation. For more details on the software and additional tutorials, reference their docs [here](https://beast.community/index.html). Here, we will be running BEAST using the [CIPRES Science Gateway](http://www.phylo.org), but we need to download the BEAST package to complate data preparation steps. [Taming the beast](https://github.com/Taming-the-BEAST/Introduction-to-BEAST2) is also a great resource for understanding what is going on here.

#### Step 1: Make the BEAST XML file using BEAUTI.

1. Install BEAST. Instructions are here for [Mac](https://beast.community/install_on_mac) and [Windows](https://beast.community/install_on_windows).

2. Convert your fasta alignment to a nexus output using Geneious (export -> nexus format)

3. Edit your nexus file to reflect your partitions

<br>![img12](/images/beast12.png) <br>

4. Open BEAUti and select `Import Data` from the `File` menu. Select your alignment nexus file.

<br>![img15](/images/beast15.png) <br>

You can view your alignment by selecting `View Partition`.

<br>![img16](/images/beast16.png)<br>

5. Link your tree and clock model for all 4 partitions by selecting the checkbox on the right, and then clicking "Link Clock Models" and "Link trees". Rename each of row in the clock model column "Clock", and each row in the tree colum "tree".

<br>![img17](/images/beast17.png)<br>

6. Go to the `Sites` tab and select your substitution models.

<br>![img3](/images/beast3.png)<br>

Based on our PartitionFinder2 results, we may have to substitute our models with base models available. Check out this [blog post](BEAST_DNA_sub_models.pdf) by Justin C. Bagley to choose the appropriate models.

7. As an example: If one model is TVM, you can use GTR and just uncheck the AG rate operator:

<br>![img13](/images/beast13.png)<br>

8. We'll use a linked, uncorrelated relaxed clock model.

<br>![img14](/images/beast14.png)<br>

9. On the `Trees` tab, select `Speciation: Yule Process` as the Tree Prior.

<br>![img4](/images/beast4.png)<br>

10. Next, click `Generate BEAST File...` and save your file with a `.xml` extension.

<br>![img5](/images/beast5.png)<br>


#### Step 2: Run BEAST in CIPRES.

1. Upload your `.xml` file to CIPRES under your `Data` folder.
2. Create a new task with your `.xml` file as Input, `BEAST on XSEDE` as Tool, and with default parameters. Click `Save and Run`.

<br>![img6](/images/beast6.png)<br>

3. When your BEAST run finishes, go to Output and download the file ending in `.trees`, as well as the file ending in `.log`.

#### Step 2.5 Analyze the results using tracer
1. Download tracer from [this website](https://github.com/beast-dev/tracer/releases/tag/v1.7.1) and open the program
2. Drag and drop the `.log` file into the tracer window. There are a lot of useful things to see here, but two main important things--your ESS and the raw trace.
3. ESS (effective sample size) values are generally considered to be "good" if they are over 200. If most of your ESS values are good, you can continue. If you have many ESS values lower than 200, we have not sufficiently explored the posterior space. Go back and edit your BEaUTi file so that MCMC chain length parameter is 100'000'000 and change the tracelog frequency to 10'000, and run BEAST again

<br>![tracer_bad](/images/tracer_bad.png)<br>

Here is an example of a run that needs to go for a longer time. Notice all the low ESS values, and the trace that is very sporadic. 
4. Look at the trace for the different parameters. If it looks like a hairy caterpillar, you have sufficiently explored the posterior space and can continue. This step can also help you to know if you need to do more than a 10% burn in.

<br>![tracer_good](/images/tracer_good.png)<br>

Here is an example of a "hairy caterpillar" trace with some higher ESS values.

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




