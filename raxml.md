### Using RAxML

One of the most popular tools for doing a Maximum Likelihood analysis is RAxML (Randomized Axelerated Maximum Likelihood).

We will be using [RAxML-NG](https://github.com/amkozlov/raxml-ng), which is a successor to RAxML. This version is faster and offers more user options than previous versions. Specifically, it can account for more models of evolution than just GTR

>Refelection

>Why do we need other models?
<br/>

1. You have to create the raxml-ng environment using Bioconda before being able to activate it and use the program. Make sure you load the miniconda module and have the Bioconda channel configured:

```
module use /GWSPH/groups/cbi/Apps/_modulefiles

module load miniconda3/4.7.10

conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge

conda create -n raxmlng raxml-ng

```

You can also add the `module use` command to your bashrc in your home directory to save time every time you connect to Pegasus.

2. Navigate to the correct directory where you have your aligned and trimmed fasta files. In the current example, we will be running raxml-ng on the concatenated COI and 16S dataset (`crayfish_concat.fasta`), which contains all GenBank samples, all KC unknown samples (that contain both COI and 16S) and three outgroups - 125_Astacoides_crosnieri, 126_Cherax_cairnsensis, 127_Samastacus_sp(SH crayfish-to be confirmed later). You also need to create a partitioned file that you can specify in your `--model` argument. It should look similar to this:

`crayfish.part`
```
TRNEF+I+G, COIp1=1-597/3
HKY+I+G, COIp2=2-597/3                                                                                         
GTR+G, COIp3=3-597/3                                                                                         
TVM+I+G, 16S=598-1031
```

3. Create a slurm script, which activates the raxml-ng environment and uses the program, titled `raxml.sh`. This slurm script will be submitted on Pegasus.

`raxml.sh`:

```bash
#!/bin/bash
#SBATCH -N 1
#SBATCH -t 2:00:00
#SBATCH -p tiny,short,defq
#SBATCH -o raxml.out
#SBATCH -e raxml.err

module load miniconda3/4.7.10
conda activate raxmlng

#--- Start the timer
t1=$(date +"%s")

raxml-ng --all --msa crayfish_concat_outgroups.fasta --model crayfish.part --tree pars{100},rand{100} --bs-trees 1000 --outgroup 125_Astacoides_crosnieri,126_Cherax_cairnsensis,127_Samastacus_sp --threads 2

#---Complete job
t2=$(date +"%s")
diff=$(($t2-$t1))
echo "[---$SN---] ($(date)) $(($diff / 60)) minutes and $(($diff % 60)) seconds elapsed."
echo "[---$SN---] ($(date)) $SN COMPLETE."

```

This is an example of the commands given to RAxML-ng, but what are some commands you may change?

At the end of you script you should see the following output files: <br>
![raxml_img1](/images/raxml_img1.png)

What do each of these output files mean? 

