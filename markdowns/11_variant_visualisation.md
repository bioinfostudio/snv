# Variant Visualisation

The Integrative Genomics Viewer (`IGV`) is an efficient visualization tool
for interactive exploration of large genome datasets.

Before jumping into `IGV`, we’ll generate a track IGV that can be used to plot
coverage:

```bash
for i in normal tumour
do
    igvtools count \
    -f min,max,mean \
    alignment/${i}/${i}.sorted.dup.recal.bam \
    alignment/${i}/${i}.sorted.dup.recal.bam.tdf \
    b37
done
```

Open `IGV`

Then:

1. Choose the reference genome corresponding to those use for alignment (b37).
2. Load BAM files from the `alignment` folder (`tumour.sorted.dup.recal.bam` and `normal.sorted.dup.recal.bam`).
3. Load three VCF files (from `variant_calling` directory).

!!! note ""
    Explore and play with the data:

    - Find germline variants
    - Find somatic variants
    - Look around...
