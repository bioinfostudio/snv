# Pre-processing: Mark Duplicates

Here we will use `MarkDuplicates (Picard)`'s approach:

Normal Sample:

```bash
$ gatk MarkDuplicates \
--REMOVE_DUPLICATES=false \
--CREATE_MD5_FILE=true \
--VALIDATION_STRINGENCY=SILENT \
--CREATE_INDEX=true \
--INPUT=alignment/normal/normal.matefixed.bam \
--OUTPUT=alignment/normal/normal.sorted.dup.bam \
--METRICS_FILE=alignment/normal/normal.sorted.dup.metrics
```

Tumour Sample:  

```bash
$ gatk MarkDuplicates \
--REMOVE_DUPLICATES=false \
--CREATE_MD5_FILE=true \
--VALIDATION_STRINGENCY=SILENT \
--CREATE_INDEX=true \
--INPUT=alignment/tumour/tumour.matefixed.bam \
--OUTPUT=alignment/tumour/tumour.sorted.dup.bam \
--METRICS_FILE=alignment/tumour/tumour.sorted.dup.metrics
```

We can look in the metrics output to see what happened.

```bash
$ less alignment/normal/normal.sorted.dup.metrics
```
