# Pre-processing: Fixmates

Some read entries don’t have their mate information written properly.  

We use `FixMateInformation (Picard)` to do this:

Normal sample:

```bash
$ gatk FixMateInformation \
--VALIDATION_STRINGENCY=SILENT \
--CREATE_INDEX=true \
--SORT_ORDER=coordinate \
--MAX_RECORDS_IN_RAM=500000 \
--INPUT=alignment/normal/normal.sorted.bam \
--OUTPUT=alignment/normal/normal.matefixed.bam
```

Tumour sample:   

```bash
$ gatk FixMateInformation \
--VALIDATION_STRINGENCY=SILENT \
--CREATE_INDEX=true \
--SORT_ORDER=coordinate \
--MAX_RECORDS_IN_RAM=500000 \
--INPUT=alignment/tumour/tumour.sorted.bam \
--OUTPUT=alignment/tumour/tumour.matefixed.bam
```
