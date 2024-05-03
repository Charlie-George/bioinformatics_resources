# RNA-seq on the Linux Command Line

## Setup

### TIP Record your commands in a text file

Open a text file - preferably on your computer, alternatively on the cluster -
to record the commands that you will type and execute during this workflow.
We recommend naming the file `obds_rnaseq_README.txt` or 'README.txt'.

In either case, save that file regularly to make sure that you do not lose
your progress throughout the day.

In addition, we recommend adding comments next to your commands
(preferably on the line above the command being commented on, alternatively below).
Each line of comment must start with the `#` (hashtag) symbol,
so that it is ignored if and when the file is executed as a Bash script.


### Using FastQC on the interactive command line 

1.  **Change into your rnaseq project directory​ in your working directory
that we created in the data management lesson** 

```bash
cd /project/obds/$USER/1_linux/rnaseq/
```

NOTE:
The environment variable `$USER` makes the command above universal,
adapting dynamically to each user on the system.
The environment variable `$USER` is replaced by the username of the
user who executes the command, which results in a different command
for each user.

List the contents of the directory to remind yourself of the files
that you prepared for the anaysis:

```bash
tree
```

2. **Load mamba and activate your conda environment for the course (obds-rnaseq)**

The Conda environment for the course contains all the software packages
and bioinformatics programs that you will need during this lesson.

Activating the Conda environment puts the executable files of those programs
on your `PATH`, allowing you to execute those programs and display their
reference manual pages.

Run the command below to activate your Conda installation
using the alias that you added in your `~/.bashrc` file
during the Conda lesson.

```bash
load_mamba
mamba activate obds-rnaseq
```
3. **Create a file called fastqc_commandline for our output files**
   
 ```bash
mkdir fastqc_commandline
```

4. **Run FastQC on a pair of FASTQ file​**

- **Look at the fastqc options using the help command and try to formulate a statement to run** ​

```bash
fastqc --help          # what options might be helpful?
```
- **Formulate a statement to run that will put the output files into the directory you created in 3​**
  
```bash
fastqc --nogroup -o fastqc_commandline   fastq/ERR1755082_*.fastq.gz
```

  - `--nogroup` stops fastqc grouping on the x-axis of some of the qc plots
  - `-o` sets the directory you where you want the outputs from fastqc to go
  - the files you want to run fastqc on go at the end of the command  

- **Examine the FastQC output files on the command line​**

```bash
cd fastqc_commandline
ls
```
You should see a `.html` file and `.zip` file for each fastqc 

- **Download the HTML report on your own computer and open in your web browser​**

You can either do this using scp or for a graphical interface, filezilla or cyberduck

For scp you can use a commands like this 
```bash
# On your own machine terminal run the below
# make sure to change <SSO> for your username and the fastq file name to your match your fastq files
scp <SSO>@obds:/project/<SSO>/1_linux/rnaseq/fastqc_commandline/ERR1755082_1_fastqc.html .
scp <SSO>@obds:/project/<SSO>/1_linux/rnaseq/fastqc_commandline/ERR1755082_2_fastqc.html .
```

- **Run MultiQC to collate reports​**
```bash
multiqc .
```
- Examine the MultiQC output files​ (you can use `cat` or `less` to look at the files in ls multiqc_data

```bash
ls multiqc_data
```

- Download the multiqc HTML report on your own computer and open in your web browser - you could do this using cyberduck, filezilla or on the command line of your laptop using: 
```bash
# On your own machine terminal run the below
# make sure to change <SSO> for your username and the fastq file name to your match your fastq files
scp <SSO>@obds:/project/<SSO>/1_linux/rnaseq/multiqc_report.html .
```

### Copy the Slurm template script

Now we are learning how to use slurm and rather then run our commands interactively on the command line submit them to a node on a HPC cluster

Run the command below to make a copy of the template Slurm script
that is named `slurm_fastqc.sh` in your analysis directory.

```bash
cd /project/obds/$USER/1_linux/rnaseq/
cp /project/obds/shared/resources/1_linux/4_slurm/slurm_template.sh slurm_fastqc_script.sh
```
### Make your output directory 

```bash
mkdir fastqc_slurm_exercise
```

### Edit your copy of the Slurm script

First run the command below to display the reference manual page for the command `fastqc`.

```bash
fastqc --help
```

Read the manual page to determine the exact command(s) that you wish to run on the input files,
or more precisely the symbolic links that you have made to those input files.

Run the command below to edit your newly made copy of the Slurm script using the text editor `nano`.

```bash
nano slurm_fastqc.sh
```

Check the contents of the template file and edit as needed.

In particular, at the bottom of the file, edit the lines that
define the command and at the top check the cores, memory and queue name. 
Because we are running the script in oour rnaseq directory we are using 
relative paths to the input and output directory. You could specify
the full path (e.g. /project/$USER/1_linux/rnaseq/fastq/*.fastq.gz 
if you wanted to. 

For instance:

```bash
#!/bin/bash
##########################################################################
## A script template for submitting batch jobs. To submit a batch job, 
## please type
##
##    sbatch myprog.sh
##
## Please note that anything after the characters "#SBATCH" on a line
## will be treated as a Slurm option.
##########################################################################

## Specify a partition. Check available partitions using sinfo Slurm command.
#SBATCH --partition=long

## The following line will send an email notification to your registered email
## address when the job ends or fails.
#SBATCH --mail-type=END,FAIL

## Specify the amount of memory that your job needs. This is for the whole job.
## Asking for much more memory than needed will mean that it takes longer to
## start when the cluster is busy.
#SBATCH --mem=2G

## Specify the number of CPU cores that your job can use. This is only relevant for
## jobs which are able to take advantage of additional CPU cores. Asking for more
## cores than your job can use will mean that it takes longer to start when the
## cluster is busy.
#SBATCH --ntasks=2

## Specify the maximum amount of time that your job will need to run. Asking for
## the correct amount of time can help to get your job to start quicker. Time is
## specified as DAYS-HOURS:MINUTES:SECONDS. This example is one day.
#SBATCH --time=0-01:00:00

## Provide file name (files will be saved in directory where job was ran) or path
## to capture the terminal output and save any error messages. This is very useful
## if you have problems and need to ask for help.
#SBATCH --output=fastqc_slurm_exercise/%j_%x.out
#SBATCH --error=fastqc_slurm_exercise/%j_%x.err

## ################### CODE TO RUN ##########################
# Load modules (if required - e.g. when not using conda) 
# module load R-base/4.3.0

# Execute these commands 
fastqc  --nogroup --threads 2 -o fastqc_slurm_exercise  fastq/ERR1755082_*.fastq.gz
```

Save and close the file when ready.

NOTE:
Make sure that the job log files -- standard output and standard error --
are created where you expect them (relative to the working directory of the job), e.g.

```bash
#SBATCH --output=fastqc_slurm_exercise/%j_%x.out
#SBATCH --error=fastqc_slurm_exercise/%j_%x.err
```

### Submit the Slurm script

Run the command below to submit the script to the queue manager.

```bash
sbatch slurm_fastqc_script.sh

# you can check its submitted using
squeue
```

NOTE:
The queue manager may not execute the job right away.
Depending on the number of jobs running at any given time,
the amount of resources (CPU, memory) that they request,
and the amount of resources that are available,
the queue manager may place the job in a queue while waiting that
sufficient resources become available, and other jobs
with higher priority in the queue have started running too.

Once the job starts execution, it should only take a few minutes
to complete.

### Inspect the FastQC output files

While the submitted job starts running, you should see the output directory appear,
and output files appear within it.

Once the command has completed, run the command below to list the contents
of the directory.

```bash
ls slurm_fastqc_script/fastqc
```

Amongst the contents of the directory, you should see HTML files.
Their names will depend on the names of the input FASTQ files that
were processed by the `fastqc` command.

Transfer the generated files to your own computer using scp like you did in the earlier exercise. 
To do this open a second Terminal application on your computer - do _not_ log into the CCB cluster -,
then edit and run the command below to download each of your own
HTML files to your computer - change the <SSO> fields to your
username and the <FILENAME> to your fastqc file 

```bash
scp <SSO>@obds:/project/<SSO>/1_linux/rnaseq/fastqc_slurm_exerise/<FILENAME>.html .
```

NOTES:

Alternatively, you may use [Filezilla][filezilla]  or Cyberduck to log into the CCB cluster
and download those files using a drag-and-drop graphical user interface.

## Use MultiQC

### Run MultiQC

back on the cluster run the command below to collate all the FastQC reports into a single MultiQC report.

```bash
multiqc -f .
```

NOTE:
The command is extremely fast and uses very little memory;
you do not need to submit it as a job script to the queue manager.

### Inspect the MultiQC report

Download the MultiQC report file `fastqc.html` to your own computer,
like you did earlier for the FastQC HTML files, e.g.

```bash
# On your own machine terminal run the below
# make sure to change <SSO> for your username and the fastq file name to your match your fastq files
scp <SSO>@obds:/project/<SSO>/1_linux/rnaseq/multiqc_report.html .
```

Then, open the downloaded file in your web browser, and discuss its contents.


We actually then edited our slurm script to run fastq for all the files, 
updating the command so that ./fastq/*.fastqc.gz files were specified, 
the threads were updated to 12 in the command and for the ntasks 
and the memory was updated to 8G

```bash
#!/bin/bash
##########################################################################
## A script template for submitting batch jobs. To submit a batch job, 
## please type
##
##    sbatch myprog.sh
##
## Please note that anything after the characters "#SBATCH" on a line
## will be treated as a Slurm option.
##########################################################################

## Specify a partition. Check available partitions using sinfo Slurm command.
#SBATCH --partition=long

## The following line will send an email notification to your registered email
## address when the job ends or fails.
#SBATCH --mail-type=END,FAIL

## Specify the amount of memory that your job needs. This is for the whole job.
## Asking for much more memory than needed will mean that it takes longer to
## start when the cluster is busy.
#SBATCH --mem=8G

## Specify the number of CPU cores that your job can use. This is only relevant for
## jobs which are able to take advantage of additional CPU cores. Asking for more
## cores than your job can use will mean that it takes longer to start when the
## cluster is busy.
#SBATCH --ntasks=12

## Specify the maximum amount of time that your job will need to run. Asking for
## the correct amount of time can help to get your job to start quicker. Time is
## specified as DAYS-HOURS:MINUTES:SECONDS. This example is one day.
#SBATCH --time=0-02:00:00

## Provide file name (files will be saved in directory where job was ran) or path
## to capture the terminal output and save any error messages. This is very useful
## if you have problems and need to ask for help.
#SBATCH --output=fastqc_slurm_exercise/%j_%x.out
#SBATCH --error=fastqc_slurm_exercise/%j_%x.err

## ################### CODE TO RUN ##########################
# Load modules (if required - e.g. when not using conda) 
# module load R-base/4.3.0

# Execute these commands 
fastqc  --nogroup --threads 2 -o ./fastqc_slurm_exercise  ./fastq/*.fastq.gz
```

## Use HISAT2

### Prepare a job submission script

Make sure your are in your obds conda environment ​if you aren't already

```bash
load_mamba
mamba activate obds-rnaseq
```

Create a new directory for your mapping outputs by go to your 
/project/$USER/1_linux/rnaseq/ directory and create a directory 
called mapped_reads. ​

```bash
cd /project/$USER/1_linux/rnaseq/
mkdir mapped_reads
```

In your rnaseq directory make a copy of your fastqc slurm script and 
call it it slurm_hisat2_script.sh we will edit this to create our hisat 
script ​

```bash
cp slurm_fastqc_script.sh slurm_hisat2_script.sh
```

Find the online HISAT2 manual and read through to establish appropriate 
mapping options​
You can find it [here](http://daehwankimlab.github.io/hisat2/manual/)

Edit the job submission script to include the hisat command from the slides, 
change the number of threads to 12 and make sure the slurm options match!​ 
Also update the paths for the input,output and log files and the index file

```
#!/bin/bash
##########################################################################
## A script template for submitting batch jobs. To submit a batch job, 
## please type
##
##    sbatch myprog.sh
##
## Please note that anything after the characters "#SBATCH" on a line
## will be treated as a Slurm option.
##########################################################################

## Specify a partition. Check available partitions using sinfo Slurm command.
#SBATCH --partition=long

## The following line will send an email notification to your registered email
## address when the job ends or fails.
#SBATCH --mail-type=END,FAIL

## Specify the amount of memory that your job needs. This is for the whole job.
## Asking for much more memory than needed will mean that it takes longer to
## start when the cluster is busy.
#SBATCH --mem=10G

## Specify the number of CPU cores that your job can use. This is only relevant for
## jobs which are able to take advantage of additional CPU cores. Asking for more
## cores than your job can use will mean that it takes longer to start when the
## cluster is busy.
#SBATCH --ntasks=12

## Specify the maximum amount of time that your job will need to run. Asking for
## the correct amount of time can help to get your job to start quicker. Time is
## specified as DAYS-HOURS:MINUTES:SECONDS. This example is one day.
#SBATCH --time=1-00:00:00

## Provide file name (files will be saved in directory where job was ran) or path
## to capture the terminal output and save any error messages. This is very useful
## if you have problems and need to ask for help.
#SBATCH --output=mapped_reads/%j_%x.out
#SBATCH --error=mapped_reads/%j_%x.err

## ################### CODE TO RUN ##########################
# Load modules (if required - e.g. when not using conda) 
# module load R-base/4.3.0

# Execute these commands 
hisat2  -x /project/shared/resources/1_linux/genomes/Mus_musculus/Ensembl/GRCm38/Sequence/HISAT/mm10 \
        --rna-strandness RF \
        --threads 12 \
        -1 fastq/ERR1755082_1.fastq.gz \
        -2 fastq/ERR1755082_2.fastq.gz \
        --summary-file mapped_reads/ERR1755082_stats.txt \
        -S mapped_reads/ERR1755082.sam
```

Submit the script to the queue​

Monitor the job (approximately 20-30 min)​

Examine the HISAT2 output files

Make a new copy of the template Slurm script,
like you did earlier for running FastQC, e.g.

NOTE:
Make sure that the Slurm job options (at the top of the job script)
match the resources required by the `hisat2` command itself;
in particular, the number of CPU cores and threads.

Once the job starts execution, the job may take up to 25-30 minutes to complete.
Try and submit as soon as you can, preferably over a break.

You may also take this opportunity to monitor the queueing and
the execution of the job, e.g.

```bash
squeue
```

### Inspect the HISAT2 output files

Edit and run the command below to interactively view and scroll through
the SAM file that you produced using HISAT2.

```bash
less mapped_reads/ERR1755082.sam 
```

Run the command below to interactively view the log file
that HISAT2 produced for your own FASTQ files.

```bash
less mapped_reads/ERR1755082_stats.txt
```

## Compress, sort, and index the SAM file


Make sure you are in your conda environment and in the rnaseq directory if
not already e.g. 
```bash
cd /project/obds/$USER/1_linux/4_rnaseq
load_mamba
mamba activate obds-rnaseq
```

Make a copy of the hisat Slurm script and call it `slurm_samtools_index.sh`
```bash
cp slurm_hisat2_script.sh 3_analysis/slurm_samtools_index.sh
```

Read the reference manual page of the
`samtools view`, `samtools sort` and `samtools index` commands
to determine the exact commands that you wish to execute. You can also 
see them online [here](http://www.htslib.org/doc/samtools.html)

```bash
samtools view --help
samtools sort --help
samtools index --help
```

Edit the job script as needed to update command and make sure threads match 
number requested in ntasks etc, e.g. 

```
#!/bin/bash
##########################################################################
## A script template for submitting batch jobs. To submit a batch job, 
## please type
##
##    sbatch myprog.sh
##
## Please note that anything after the characters "#SBATCH" on a line
## will be treated as a Slurm option.
##########################################################################

## Specify a partition. Check available partitions using sinfo Slurm command.
#SBATCH --partition=long

## The following line will send an email notification to your registered email
## address when the job ends or fails.
#SBATCH --mail-type=END,FAIL

## Specify the amount of memory that your job needs. This is for the whole job.
## Asking for much more memory than needed will mean that it takes longer to
## start when the cluster is busy.
#SBATCH --mem=10G

## Specify the number of CPU cores that your job can use. This is only relevant for
## jobs which are able to take advantage of additional CPU cores. Asking for more
## cores than your job can use will mean that it takes longer to start when the
## cluster is busy.
#SBATCH --ntasks=12

## Specify the maximum amount of time that your job will need to run. Asking for
## the correct amount of time can help to get your job to start quicker. Time is
## specified as DAYS-HOURS:MINUTES:SECONDS. This example is one day.
#SBATCH --time=0-02:00:00

## Provide file name (files will be saved in directory where job was ran) or path
## to capture the terminal output and save any error messages. This is very useful
## if you have problems and need to ask for help.
#SBATCH --output=./mapped_reads/%j_%x.out
#SBATCH --error=./mapped_reads/%j_%x.err

## ################### CODE TO RUN ##########################
# Load modules (if required - e.g. when not using conda) 
# module load R-base/4.3.0

# Execute these commands 

# convert sam to bam using samtools view
# -h includes the header which some downstream programmes need sometimes
samtools view -b -h --threads 12  mapped_reads/ERR1755082.sam >  mapped_reads/ERR1755082.bam
# sort the bam file -@ specifies threads
samtools sort -@ 12 -o mapped_reads/ERR1755082.sorted.bam mapped_reads/ERR1755082.bam
# index the sorted bam file
samtools index -@ 12  mapped_reads/ERR1755082.sorted.bam

# remove the unsorted bam and the sam file as we no longer need these
rm -rf mapped_reads/ERR1755082.bam && rm -rf mapped_reads/ERR1755082.sam
```

NOTE:
Make sure that the Slurm job options (at the top of the job script)
match the resources required by the `samtools` commands themselves;
in particular, the number of CPU cores and threads. I've also added a 
step at the bottom to delete the intermediate file (ERR1755082.bam) & 
ERR1755082.sam as these take upspace and it is only the sorted bam 
that we will take through to the rest of our analysis

## Mapping quality control

### Run samtools flagstat and samtools idxstats

Read the reference manual page of the commands
`samtools flagstat` and `samtools idxstats`
to determine the full command lines that you wish to execute.

```bash
samtools flagstat --help
samtools idxstats --help
```

Make a new copy of the template Slurm script, named `slurm_samtools_stats.sh`.

```bash
cd /project/obds/$USER/1_linux/rnaseq
cp slurm_samtools_index.sh slurm_samtools_stats.sh
```

Edit the job script as needed, e.g.

```
#!/bin/bash
##########################################################################
## A script template for submitting batch jobs. To submit a batch job, 
## please type
##
##    sbatch myprog.sh
##
## Please note that anything after the characters "#SBATCH" on a line
## will be treated as a Slurm option.
##########################################################################

## Specify a partition. Check available partitions using sinfo Slurm command.
#SBATCH --partition=long

## The following line will send an email notification to your registered email
## address when the job ends or fails.
#SBATCH --mail-type=END,FAIL

## Specify the amount of memory that your job needs. This is for the whole job.
## Asking for much more memory than needed will mean that it takes longer to
## start when the cluster is busy.
#SBATCH --mem=2G

## Specify the number of CPU cores that your job can use. This is only relevant for
## jobs which are able to take advantage of additional CPU cores. Asking for more
## cores than your job can use will mean that it takes longer to start when the
## cluster is busy.
#SBATCH --ntasks=1

## Specify the maximum amount of time that your job will need to run. Asking for
## the correct amount of time can help to get your job to start quicker. Time is
## specified as DAYS-HOURS:MINUTES:SECONDS. This example is one day.
#SBATCH --time=0-02:00:00

## Provide file name (files will be saved in directory where job was ran) or path
## to capture the terminal output and save any error messages. This is very useful
## if you have problems and need to ask for help.
#SBATCH --output=./mapped_reads/%j_%x.out
#SBATCH --error=./mapped_reads/%j_%x.err

## ################### CODE TO RUN ##########################
# Load modules (if required - e.g. when not using conda) 
# module load R-base/4.3.0

# Execute these commands 

# create mapping qc files
samtools idxstat ./mapped_reads/ERR1755082.sorted.bam > ./mapped_reads/ERR1755082.sorted.bam.idxstats
samtools flagstats ./mapped_reads/ERR1755082.sorted.bam > ./mapped_reads/ERR1755082.sorted.bam.flagstat

```

NOTE:
Make sure that the Slurm job options (at the top of the job script)
match the resources required by the commands
`samtools flagstat` and `samtools idxstats` themselves;
in particular, the number of CPU cores and threads. Here there are no extra threads 
specified as they are quite quick tasks so i have set ntasks=1 and reduced the memory
requirements

Edit and run the command below to inspect the output files.

```bash
less mapped_reads/ERR1755082.flagstat
less mapped_reads/ERR1755082.idxstats
```

### Run MultiQC again

Run the command below to collate all the FastQC reports into a single MultiQC report.

```bash
multiqc -f .
```

NOTE:
The command is extremely fast and uses very little memory;
you do not need to submit it as a job script to the queue manager.

### Inspect the MultiQC report

Download the MultiQC report file `fastqc.html` to your own computer,
like you did earlier for the FastQC HTML files, e.g. using filezilla or cyberduck

Then, open the downloaded file in your web browser, and discuss its contents.

## Use featureCounts

here we first need to make sure we have a gtf file to quantify against 
(we sometimes do this in exericise 9 of the data management lesson on 
day 2 but sometimes it is skipped for time, so we do it here instead) 

navigate to the ensembl archieve and download the ensembl 102 mm10 gtf file. 
Go to https://www.ensembl.org/index.html and click on 'Downloads' at the top 
about halfway down in a box called 'complete datasets and databases' on the left hand side is a small link to the FTP site https://ftp.ensembl.org/pub
navigate through this to the 102 archive / gtf / mus_musculus at https://ftp.ensembl.org/pub/release-102/gtf/mus_musculus/ and select 
Mus_musculus.GRCm38.102.gtf.gz and copy link - you want this one as it contains all 
transcripts and the chromosomes are labeled without the chr in so it will match our chromosome 
names in our genome file - you can look at the README file for details 

Move into the genome folder and run wget to download
```bash
cd genomes
wget https://ftp.ensembl.org/pub/release-102/gtf/mus_musculus/Mus_musculus.GRCm38.102.gtf.gz
```
You could check your chromsome names match the ones in the ones your reads are mapped to 
by checking them in the idxstats file you created above and running the below on the gtf file 
to get the chromosome names 

```
zless Mus_musculus.GRCm38.102.gtf.gz | cut -f 1 | sort |uniq 
```

feature counts actually requires a gunzipped gtf so uncompress it
```
gunzip Mus_musculus.GRCm38.102.gtf.gz
```
Now lets actually do our quantification 
Read the reference manual page of the `featureCounts` command
to determine the full command line that you wish to execute.

```bash
featureCounts
```

Make sure your are in your obds-rnaseq conda environment and the rnaseq directory
and make a new directory called `quantification` and the a new copy of the template Slurm script, named `slurm_featurecounts.sh`.

```bash
load_mamba
mamba activate obds-rnaseq
cd /project/obds/$USER/1_linux/rnaseq
mkdir quantification
cp /project/obds/shared/resources/1_linux/rnaseq/slurm_samtools_stats.sh slurm_featurecounts_script.sh
```

Edit the job script as needed, e.g.

```
#!/bin/bash
##########################################################################
## A script template for submitting batch jobs. To submit a batch job, 
## please type
##
##    sbatch myprog.sh
##
## Please note that anything after the characters "#SBATCH" on a line
## will be treated as a Slurm option.
##########################################################################

## Specify a partition. Check available partitions using sinfo Slurm command.
#SBATCH --partition=long

## The following line will send an email notification to your registered email
## address when the job ends or fails.
#SBATCH --mail-type=END,FAIL

## Specify the amount of memory that your job needs. This is for the whole job.
## Asking for much more memory than needed will mean that it takes longer to
## start when the cluster is busy.
#SBATCH --mem=10G

## Specify the number of CPU cores that your job can use. This is only relevant for
## jobs which are able to take advantage of additional CPU cores. Asking for more
## cores than your job can use will mean that it takes longer to start when the
## cluster is busy.
#SBATCH --ntasks=12

## Specify the maximum amount of time that your job will need to run. Asking for
## the correct amount of time can help to get your job to start quicker. Time is
## specified as DAYS-HOURS:MINUTES:SECONDS. This example is one day.
#SBATCH --time=0-02:00:00

## Provide file name (files will be saved in directory where job was ran) or path
## to capture the terminal output and save any error messages. This is very useful
## if you have problems and need to ask for help.
#SBATCH --output=./quantification/%j_%x.out
#SBATCH --error=./quantification/%j_%x.err

## ################### CODE TO RUN ##########################
# Load modules (if required - e.g. when not using conda) 
# module load R-base/4.3.0

# Execute these commands

# quantify sorted bam files - note the gtf needs to be  gunzipped 
featureCounts \
  -a genome/Mus_musculus.GRCm38.102.gtf \
  -t exon \
  -g gene_id \
  -o quantification/counts.tsv \
  -s 2 \
  -p \
  -B -C \
  -T 12 \
  mapped_reads/ERR1755082.sorted.bam

```

Edit and run the command below to inspect the output file.

```bash
less quantification/counts.tsv
less quantification/counts.tsv.summary
```

recompress your gtf file to save space 
```
gzip genomes/Mus_musculus.GRCm38.102.gtf.gz
```

## Use MultiQC (one more time)

### Run MultiQC

Run the command below to collate all the FastQC reports into a single MultiQC report.

```bash
multiqc -f .
```

NOTE:
The command is extremely fast and uses very little memory;
you do not need to submit it as a job script to the queue manager.

### Inspect the MultiQC report

Download the MultiQC report file `fastqc.html` to your own computer,
like you did earlier for the FastQC HTML files, e.g. using filezilla, cyberduck or on the command 
line using scp

Then, open the downloaded file in your web browser, and discuss its contents.

## Wrap-up

Congratulations, you have completed this workshop!

In this workshop, you have learned:

- To set a working directory for a project.
- To create symbolic links to input files for a project.
- To create and manage subdirectories for the various steps of a workflow.
- To activate and use a Conda environment for a project.
- To write and submit job scripts to the Slurm queue manager of the obds cluster.
- To read tool manuals and choose parameters to try
- To write and execute some commands on the login node.
- To use FastQC, MultiQC, HISAT2, SAMtools and featureCounts in a workflow.
- To examine output files - including log files - at the various steps of a workflow.
- But most importantly of all you've learnt how to troubleshoot and spot common errors
  such as typos of file paths, commands, not being in your conda environment, being in the wrong
  directory when submitting scripts so the realtive paths don't work, miss-asigning slurm resources

Well Done! 

Once you have run every thing its good practise to push your scripts to git so you have a copy of them 

to do this 
````
# copy your scripts in the rnaseq directory to your git directory
# you made on day 3 - replace the path below to match what you called it
# where you already have a copy of your conda environment yml file 
cd /project/$USER/git/<obds_course_directory_or_whatever_you_called_it>
cp /project/$USER/1_linux/rnaseq/*.sh .

# do git status to see if there is anything you need to update - you
# should see the files you just copied
git add slurm_fastqc_script.sh slurm_hisat2_script.sh
git add slurm_samtools_index.sh slurm samtools_stats.sh slurm_featurecounts_script.sh

# commit your scripts with a message
# git commit -m 'adding scripts from rnaseq worksfow'

# push to github
git push

# if you have errors at the push stage read them carefully you might need to run
# `git pull` first and set how you want it merge files  

```

<!-- Links -->

[filezilla]: https://filezilla-project.org/
