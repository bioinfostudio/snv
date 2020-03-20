# Variant Calling

Most of SNV caller use either a Bayesian, a threshold or a t-test
approach to do the calling

Here we will try 3 variant callers:

* `Varscan`
* `MuTecT`
* `Strelka`

Other candidates:

* `Virmid`
* `Somatic sniper`

Many, MANY others can be found here: https://www.biostars.org/p/19104/

In our case, let’s create a new work directory to start wit:

    mkdir variant_calling


## Varscan

`Varscan` calls somatic variants (SNPs and indels) using a
heuristic method and a statistical test based on the number of aligned
reads supporting each allele. It expects both a normal and a tumour file in
`SAMtools pileup` format from sequence alignments in binary alignment/map
(BAM) format. To build a pileup file, you will need:

* A SAM/BAM file (`*.sorted.dup.recal.bam`) that has been sorted using the `sort` command
of `samtools`.
* The reference sequence (`human_g1k_v37.fasta`) to which reads were aligned, in
FASTA format.
* The `samtools` software package.

```bash
for i in normal tumour
do
  samtools mpileup -L 1000 -B -q 1 \
  -f ref/human_g1k_v37.fasta \
  -r 4:1-100000 \
  alignment/${i}/${i}.sorted.dup.recal.bam \
  > variant_calling/${i}.mpileup
done
```

Notes on `samtools` arguments:

  > **-L**: max per-sample depth for INDEL calling [1000]  
  > **-B**: disable BAQ (per-Base Alignment Quality)  
  > **-q**: skip alignments with mapQ smaller than 1  
  > **-g**: generate genotype likelihoods in BCF format

```bash
$ java -Xmx2G -jar /usr/local/bin/VarScan.jar \
somatic variant_calling/normal.mpileup \
variant_calling/tumour.mpileup \
variant_calling/varscan \
--output-vcf 1 \
--strand-filter 1 \
--somatic-p-value 0.001
```


## MuTect

Now let’s try a different variant caller, `MuTect`.

```bash
$ gatk Mutect2 \
-R ref/human_g1k_v37.fasta \
-I alignment/normal/normal.sorted.dup.recal.bam \
-I alignment/tumour/tumour.sorted.dup.recal.bam \
-normal Blood \
-O variant_calling/mutect.vcf \
-L 4:1-100000
```


## Strelka

And finally let’s try Illumina’s `Strelka`.

```bash
configureStrelkaSomaticWorkflow.py \
--normalBam alignment/normal/normal.sorted.dup.recal.bam \
--tumorBam alignment/tumour/tumour.sorted.dup.recal.bam \
--referenceFasta ref/human_g1k_v37.fasta \
--runDir variant_calling/strelka/ \
--callRegions ref/callable.bed.gz

variant_calling/strelka/runWorkflow.py -m local

cp variant_calling/strelka/results/variants/somatic.snvs.vcf.gz variant_calling/strelka.vcf.gz
```
