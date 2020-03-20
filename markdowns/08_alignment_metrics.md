# Step 3: BAM QC: Alignment metrics

Alignment metrics tells you if your sample and your reference fit together.

For the alignment metrics, `samtools flagstat` is very fast but
`bwa-mem` breaks some reads into pieces, the numbers can be a bit confusing.

Instead, we will use `CollectAlignmentSummaryMetrics (Picard)` to compute the metrics:

```bash
for i in normal tumour
do
    gatk CollectAlignmentSummaryMetrics \
    --VALIDATION_STRINGENCY=SILENT \
    --REFERENCE_SEQUENCE=ref/human_g1k_v37.fasta \
    --INPUT=alignment/${i}/${i}.sorted.dup.recal.bam \
    --OUTPUT=alignment/${i}/${i}.sorted.dup.recal.metric.alignment.tsv \
    --METRIC_ACCUMULATION_LEVEL=LIBRARY
done
```

Explore the results

    less -S alignment/normal/normal.sorted.dup.recal.metric.alignment.tsv
    less -S alignment/tumour/tumour.sorted.dup.recal.metric.alignment.tsv
