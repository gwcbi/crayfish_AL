## Step 3: Aligning data using MAFFT 

1. Read and review MAFFT [documentation](https://mafft.cbrc.jp/alignment/software/manual/manual.html). We will be using the command line to execute MAFFT and will need to use a handful of the command options from the documentation.

> Reflection:
> 
> Why are we deciding to use local alignment instead of global alignment?
<br/>


2. Create a slurm script, which contains the mafft command, titled `mafft.sh`. This slurm script will be submitted on pegasus.

You can either create this script on the terminal by doing:

A.  On pegasus, navigate to the direcory where you have uploaded the files. This should be `/lustre/groups/cbi/Projects/crayfish_ar`   
B.  `touch mafft_COI.sh` - this creates a file <br/>
C.  `nano mafft_COI.sh` - this opens the file to edit within the terminal <br/>
D.  Then you can paste the code below into the file. 
<br/>

Alternatively, you can open a next text file in your text editor and save the file. Then upload to pegasus.

This is the script you will use for your COI alignment. What would you need to change before you run it on 16S?

`mafft_COI.sh`:

```bash
#!/bin/bash
#SBATCH -N 1
#SBATCH -t 2:00:00
#SBATCH -p tiny,short,defq
#SBATCH -o mafft_COI.out
#SBATCH -e mafft_COI.err

module load mafft
#--- Start the timer
t1=$(date +"%s")

mafft --thread $(nproc) --localpair --maxiterate 1000 crayfishCOI.fasta > aligned_crayfishCOI.fasta

#---Complete job
t2=$(date +"%s")
diff=$(($t2-$t1))
echo "[---$SN---] ($(date)) $(($diff / 60)) minutes and $(($diff % 60)) seconds elapsed."
echo "[---$SN---] ($(date)) $SN COMPLETE."

```
<br/>


The script should look like this on the terminal: <br/>
![mafft_img1](/images/mafft_img1.png)

> Reflection:
> 
> What do all the lines in the above code block mean? Why are the options important to give to the slurm scheduler?
<br/>


3. Submitting the script to slurm. <br/>

After creating the above script, we now have to send it off to the scheduler on pegasus. The way you do that is: `sbatch mafft.sh`

The output will look like this on the terminal: <br/>
![mafft_img2](/images/mafft_img2.png)

To monitor your script: `squeue`, which will show you this on the terminal: <br/>
![mafft_img3](/images/mafft_img3.png)
<br/>

4. Record all your methods in the manuscript. 
<br/>


5. View the alignment in Geneious or online alignment viewers. How does it look? Do we need to adjust the commands or do we need to trim the alignment?
<br/>

### Aligning Concatenated Dataset

After COI and 16S alignments are concatenated, you will then re-align using MAFFT.
<br/>

`mafft_concat.sh`:

```bash
#!/bin/bash
#SBATCH -N 1
#SBATCH -t 2:00:00
#SBATCH -p tiny,short,defq
#SBATCH -o mafft_concat.out
#SBATCH -e mafft_concat.err

#--- Start the timer
t1=$(date +"%s")

mafft --op 3.00 --thread $(nproc) --localpair --maxiterate 1000 crayfish_concat.fasta > aligned_crayfish_concat.fasta

#---Complete job
t2=$(date +"%s")
diff=$(($t2-$t1))
echo "[---$SN---] ($(date)) $(($diff / 60)) minutes and $(($diff % 60)) seconds elapsed."
echo "[---$SN---] ($(date)) $SN COMPLETE."

```
<br/>
