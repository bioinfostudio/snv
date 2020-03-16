# Introduction

The goal of this course is to present the main steps that are
commonly used to process and to analyze cancer sequencing data. We will
focus only on whole genome data and provide command lines that allow
detecting Single Nucleotide Variants (SNV). This course will show you
how to launch individual steps of a complete DNA-Seq SNV pipeline using
cancer data.

In the second part of the course, we will also be using IGV to
visualise and manually inspect candidate variant calls.


## Prepare the Environment

We will use a dataset(ERP001071) derived from whole genome sequencing of a
33-yr-old lung adenocarcinoma patient, who is a never-smoker and has no
familial cancer history.

The data consists of whole genome sequencing of liver metastatic lung
cancer (frozen), primary lung cancer (FFPE) and blood tissue of a lung
adenocarcinoma patient (AK55).

Go to the `snv` working directory:

```bash
$ cd /home/bioinfo/snv/
```

All commands entered into the terminal for this tutorial should be from
within the `snv` directory.


The BAM alignment files are contained in the subdirectory called
`alignment` and are located in the following subdirectories:

> `normal/normal.sorted.bam` and `normal/normal.sorted.bam.bai`

> `tumour/tumor.sorted.bam` and `tumour/tumour.sorted.bam.bai`

Check that the `alignment` directory contains the above-mentioned files by typing:

```bash
$ ls -l alignment/*
```

These files are based on subsetting the whole genomes derived from blood
and liver metastases to the first 10Mb of chromosome 4. This will allow
our analyses to run in a sufficient time during the course, but it’s
worth being aware that this is less < 0.5% of the genome which
highlights the length of time and resources required to perform cancer
genomics on full genomes!

The initial structure of your folders should look like this (type `ls -l`):

```
-- alignment/       # bam files
  -- normal/        # The blood sample directory containing bam files
  -- tumour/        # The tumour sample directory containing bam files
-- ref/             # Contains reference genome files
```

Make sure you are in the correct directory by typing:

```bash
$ cd /home/bioinfo/snv/
```
