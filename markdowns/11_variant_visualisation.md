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

!!! note ""
    Explore and play with the data:

    - Find germline variants
    - Find somatic variants
    - Look around...

<div id="igv-div"></div>

<script type="text/javascript">
  var igvDiv = document.getElementById("igv-div");
  var options =
    {
        genome: "hg19",
        locus: "chr4:1-100000",
        tracks: [
            {
                type: "alignment",
                format: "bam",
                name: "Tumour",
                url: "gs://bioinfostudio/snv/alignment/tumour/tumour.sorted.dup.recal.bam",
                indexURL: "gs://bioinfostudio/snv/alignment/tumour/tumour.sorted.dup.recal.bai",
            },
            {
                type: "alignment",
                format: "bam",
                name: "Normal",
                url: "gs://bioinfostudio/snv/alignment/normal/normal.sorted.dup.recal.bam",
                indexURL: "gs://bioinfostudio/snv/alignment/normal/normal.sorted.dup.recal.bai",
            },
            {
                type: "variant",
                format: "vcf",
                name: "varscan",
                url: "gs://bioinfostudio/snv/variant_calling/varscan.snp.vcf.gz",
                indexed: "gs://bioinfostudio/snv/variant_calling/varscan.snp.vcf.gz.tbi",
            },
            {
                type: "variant",
                format: "vcf",
                name: "mutect",
                url: "gs://bioinfostudio/snv/variant_calling/mutect.vcf.gz",
                indexed: "gs://bioinfostudio/snv/variant_calling/mutect.vcf.gz.tbi",
            },
            {
                type: "variant",
                format: "vcf",
                name: "strelka",
                url: "gs://bioinfostudio/snv/variant_calling/strelka.vcf.gz",
                indexed: "gs://bioinfostudio/snv/variant_calling/strelka.vcf.gz.tbi",
            },
       ]
    };
    igv.createBrowser(igvDiv, options)
</script>
