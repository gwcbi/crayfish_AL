## Step 3: Model Selection 

1. Create an account and log in to the [CIPRES Science Gateway](https://www.phylo.org/portal2/login!input.action).

2. Click `Create New Folder` and enter a title and description for your analysis.

3. Go to your `Data` Subfolder and choose `Upload/Enter Data`. Upload a FASTA alignment file.

![img1](/images/img1.png)

4. Go to your `Tasks` Subfolder and choose `Create New Task`. Under `Select Data` select your alignment file. Under `Select Tool` 
choose `jModelTest2 on XSEDE`. Under `Set Parameters` select `Convert input to Phylip format (only)` and choose `Save Parameters` and click `Ok`. On the Task page, choose `Save and Run Task`.

![img2](/images/img2.png)

5. When your job has finished, you will get an email. Then, on the task page, you will have an option to `View Output`. Go to the output 
and download `infile.phy.phy`. (Note: if you have any `.` characters in your sequence names, you will need to first find and remove them from your input file.)

![img3](/images/img3.png)

6. Go back to the `Data` folder and upload `infile.phy.phy`. 

![img4](/images/img4.png)

7. Create a new task with `infile.phy.phy` as input and `jModelTest2 on XSEDE` as the tool. Under `Advanced Parameters` go to `Select Information Criterion` and choose the first three. Click `Save and Run Task`. 
![img6](/images/img6.png)

8. When the task has completed, go to the output and download `STDOUT`. This file contains all the jModelTest output, including the best fit models.
![img7](/images/img7.png)

9. The best models (based on each critera) are printed at the bottom of the file. Metrics for additional models are also available in the file. 
![img8](/images/img8.png)

