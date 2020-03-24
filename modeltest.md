## Step 3: Model Selection with jModelTest

1. Create an account and log in to the [CIPRES Science Gateway](https://www.phylo.org/portal2/login!input.action).

2. Click `Create New Folder` and enter a title and description for your analysis.

![img1](/images/img1.png)

3. Go to your `Data` Subfolder and choose `Upload/Enter Data`. Upload the FASTA alignment file. (Note: if you have any `.` characters in your sequence names, you will need to first find and remove them from your input file.)

![img9](/images/img9.png)

4. Go to your `Tasks` subfolder and create a new task with your alignment as input and `jModelTest2 on XSEDE` as the tool. Under `Advanced Parameters` go to `Select Information Criterion` and choose the first three. Click `Save and Run Task`. When your job has finished, you will get an email. 

![img6](/images/img6.png)

5. When the task has completed, go to the output and download `STDOUT`. This file contains all the jModelTest output, including the best fit models.

![img7](/images/img7.png)

6. The best models (based on each critera) are printed at the bottom of the file. Metrics for additional models are also available in the file. 

![img8](/images/img8.png)

