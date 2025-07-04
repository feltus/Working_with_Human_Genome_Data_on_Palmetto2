# Working_with_Human_Genome_Data_on_Palmetto2

# Computational Practice: Working with Human Genome Data on a Linux Cluster.

# Overview
In this lab, you will obtain and process human genome files on the Palmetto2 HPC cluster.  Using a remote, high-performance computer is the best way to process huge genomics datasets that will not fit on your laptop.  When you log in to the cluster, you will enter a "bash shell" enivironment that allows you to enter Linux comands (e.g. ls, pwd, mkdir, etc.) that are then executed by the Linux operating system (OS).  By performing real bioinformatics tasks on real genomics data, you will gain experience using Linux to solve complex computational biology problems.  It takes years to get good at this, and the more effort you put into learning the technical langauge of bash, the better scientist you will become :).  

# Learning Objectives
* Access a high-performance computing environment
* Set up a proper working directory
* Download and process genomic data
* Use basic bash commands for bioinformatics file handling

# Instructions

# Setup and Data Acquisition

## Step 1: Log into the Palmetto2 cluster
Open your web browser and navigate to https://ondemand.rcd.clemson.edu/
Enter your university credentials
Complete the two-factor authentication if prompted

## Step 2: Request an interactive Jupyter notebook session
From the dashboard, click on "Interactive Apps" in the top menu
Select "Jupyter Notebook" from the dropdown menu
Configure your session with the following resources:
Number of cores: 4
Memory per core: 8 (This will give you a total of 32 GB)
Wall time: 12:00:00 (12 hours)
Partition: Select an appropriate partition (e.g., Intel, check availability)
QOS: regular
Click "Launch" and wait for your job to start

## Step 3: Start a terminal session
Once your Jupyter session launches, click on "New" in the top right corner
Select "Terminal" from the dropdown menu

## Step 4: Create a working directory in scratch space
```
# Navigate to your scratch space
cd /scratch/`whoami`

# Create a new directory for this assignment
mkdir human_genome_analysis

# Enter the directory
cd human_genome_analysis
```

## Step 5: Download the human genome and cDNA gene set from ENSEMBL

```
# Download the human genome (GRCh38)
wget https://ftp.ensembl.org/pub/release-109/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz

# Download the human cDNA gene set
wget https://ftp.ensembl.org/pub/release-109/fasta/homo_sapiens/cdna/Homo_sapiens.GRCh38.cdna.all.fa.gz
```

## Step 6: Uncompress the files
```
# Uncompress the genome file
gunzip Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz

# Uncompress the cDNA file
gunzip Homo_sapiens.GRCh38.cdna.all.fa.gz
```

## Step 7: Count the sequences in FASTA format
```
# Count sequences in the genome file
echo "Number of sequences in the genome:"
grep -c "^>" Homo_sapiens.GRCh38.dna.primary_assembly.fa

# Count sequences in the cDNA file
echo "Number of sequences in the cDNA:"
grep -c "^>" Homo_sapiens.GRCh38.cdna.all.fa

# Optional: Examine the first few sequences in each file
echo -e "\nFirst 5 sequences in the genome:"
grep "^>" Homo_sapiens.GRCh38.dna.primary_assembly.fa | head -5

echo -e "\nFirst 5 sequences in the cDNA:"
grep "^>" Homo_sapiens.GRCh38.cdna.all.fa | head -5
```
# Questions for Reflection
* Why is it important to work in the scratch space rather than your home directory when dealing with large genomic files?
* What is the difference between the primary assembly genome and the cDNA files you downloaded?
* Approximately how much disk space did each file take before and after decompression?
* What pattern does the grep "^>" command search for, and why is this effective for counting FASTA sequences?

# Generative AI Prompts For a Deeper Dive
## Prompt 1: File Compression in Bioinformatics
```
I'm working with large genomic datasets and need to understand file compression better. Could you explain:
1. The differences between common compression formats used in bioinformatics (.gz, .zip, .bz2, .xz)
2. How compression affects file size and processing speed for genomic data
3. When to use compression vs. when to work with uncompressed files
4. How tools like 'gzip', 'gunzip', and 'zcat' can be integrated into bioinformatics pipelines
5. Best practices for compression when sharing genomic data with collaborators"
```

## Prompt 2: Understanding FASTA and Common Sequence Formats
```
"I'm learning about different sequence file formats in bioinformatics. Could you provide a comprehensive explanation of:
1. The FASTA format - its structure, header conventions, and appropriate uses
2. How FASTA differs from other common formats like FASTQ, SAM/BAM, and VCF
3. Tools and commands for converting between these formats
4. How to efficiently parse and process FASTA files using bash commands and common bioinformatics tools
5. When each format is most appropriate in a typical NGS analysis pipeline
Please include examples of what each format looks like and explain the biological information each one captures."
```
