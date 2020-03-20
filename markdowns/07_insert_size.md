# Step 2: BAM QC: Insert Size

Insert size corresponds to the size of DNA fragments sequenced. It is different
from the gap size (= distance between reads)!

These metrics are computed using `CollectInsertSizeMetrics (Picard)`:

```bash
for i in normal tumour
do
    gatk CollectInsertSizeMetrics \
    --VALIDATION_STRINGENCY=SILENT \
    --REFERENCE_SEQUENCE=ref/human_g1k_v37.fasta \
    --INPUT=alignment/${i}/${i}.sorted.dup.recal.bam \
    --OUTPUT=alignment/${i}/${i}.sorted.dup.recal.metric.insertSize.tsv \
    --Histogram_FILE=alignment/${i}/${i}.sorted.dup.recal.metric.insertSize.histo.pdf \
    --METRIC_ACCUMULATION_LEVEL=LIBRARY
done
```

Look at the output:

    less -S alignment/normal/normal.sorted.dup.recal.metric.insertSize.tsv
    less -S alignment/tumour/tumour.sorted.dup.recal.metric.insertSize.tsv
