# Pre-processing: Base Quality Recalibration

### Why do we need to recalibrate base quality scores?

The vendors tend to inflate the values of the bases in the reads. The
recalibration tries to lower the scores of some biased motifs for some
technologies.

Base Quality Recalibration runs in 2 steps:

1. Build covariates based on context and known SNP sites.
2. Correct the reads based on these metrics.


Here we will use GATK's `BaseRecalibrator` and `ApplyBQSR`:

```bash
for i in normal tumour
do
    gatk BaseRecalibrator \
    -R ref/human_g1k_v37.fasta \
    --known-sites ref/dbSnp-138_chr4.vcf \
    -L 4:1-100000 \
    -O alignment/${i}/${i}.sorted.dup.recal.table \
    -I alignment/${i}/${i}.sorted.dup.bam

    gatk ApplyBQSR \
    -R ref/human_g1k_v37.fasta \
    -bqsr alignment/${i}/${i}.sorted.dup.recal.table \
    -O alignment/${i}/${i}.sorted.dup.recal.bam \
    -I alignment/${i}/${i}.sorted.dup.bam
done
```
