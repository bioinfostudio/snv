# Variant Annotation

Following variant calling, we end up with a VCF file of genomic
coordinates with the genotype(s) and quality information for each
variant. By itself, this information is not much use to us unless there
is a specific genomic location we are interested in. Generally, we next
want to annotate these variants to determine whether they impact any
genes and if so what is their level of impact (e.g. are they causing a
premature stop codon gain or are they likely less harmful missense
mutations).

The sections above have dealt with calling somatic variants from the
first 10Mb of chromosome 4. This is important in finding variants that
are unique to the tumour sample(s) and may have driven both tumour
growth and/or metastasis. An important secondary question is whether the
germline genome of the patient contains any variants that may have
contributed to the development of the initial tumour through
predisposing the patient to cancer. These variants *may not* be captured
by somatic variant analysis as their allele frequency may not change in
the tumour genome compared with the normal.

For this section, we will use **all** variants from the first 60Mb of
chromosome 5 that have been pre-generated using the GATK `HaplotypeCaller`
variant caller on both the normal and tumour genomes. The output of this
was GVCF files which were fed into GATK `GenotypeGVCFs` to produce a
merged VCF file. We will use this pre-generated file as we are primarily
interested in the annotation of variants rather than their generation.
The annotation method we will use is called `Variant Effect Predictor`
or `VEP` for short and is available from Ensembl [here](http://ensembl.org/info/docs/tools/vep/index.html).

Our pre-generated VCF file is located in the `variants` folder. Let’s
have a quick look at the variants:

    zless variants/HC.chr5.60Mb.vcf.gz

Notice how there are two genotype blocks at the end of each line for the
normal (`Blood`) and tumour (`liverMets`) samples.

Let’s now run `VEP` on this VCF file to annotate each variant with its
impact(s) on the genome.

```bash
vep --dir_cache /home/bioinfo/snv -i variants/HC.chr5.60Mb.vcf.gz --vcf -o variants/HC.chr5.60Mb.vep.vcf --stats_file variants/HC.chr5.60Mb.vep.html --format vcf --offline -fork 1 --fasta ref/human_g1k_v37.fasta --fields Consequence,Codons,Amino_acids,Gene,SYMBOL,Feature,EXON,PolyPhen,SIFT,Protein_position,BIOTYPE --species homo_sapiens
```

`VEP` will take approximately 10 minutes to run and once it is finished
you will have a new VCF file with all of the information in the input
file but with added annotations in the INFO block. `VEP` also produces an
HTML report summarising the distribution and impact of variants
identified.

Once `VEP` is done running, let’s first look at the HTML report it
produced with the following command:

- [HC.chr5.60Mb.vep.html](http://storage.googleapis.com/bioinfostudio/snv/variants/HC.chr5.60Mb.vep.html){:target="_blank"}

This report shows information on the `VEP` run, the number of variants,
the classes of variants detected, the variant consequences and the
distributions of variants through the genome. Close Firefox to resume
the terminal prompt.

Now let’s look at the variant annotations that `VEP` has added to the VCF
file by focussing on a single variant. Let’s fetch the same variant from
the original VCF file and the annotated VCF file to see what has been
changed.

    zcat variants/HC.chr5.60Mb.vcf.gz | grep '5\s174106\s'
    grep '5\s174106\s' variants/HC.chr5.60Mb.vep.vcf

These commands give us the original variant:

    5   174106  .   G   A   225.44  .   AC=2;AF=0.500;AN=4;BaseQRankSum=1.22;ClippingRankSum=0.811;DP=21;FS=0.000;GQ_MEAN=127.00;GQ_STDDEV=62.23;MLEAC=2;MLEAF=0.500;MQ=60.00;MQ0=0;MQRankSum=0.322;NCC=0;QD=10.74;ReadPosRankSum=0.377;SOR=0.446   GT:AD:DP:GQ:PL  0/1:7,6:13:99:171,0,208 0/1:5,3:8:83:83,0,145

and the same variant annotated is:

    5   174106  .   G   A   225.44  .   AC=2;AF=0.500;AN=4;BaseQRankSum=1.22;ClippingRankSum=0.811;DP=21;FS=0.000;GQ_MEAN=127.00;GQ_STDDEV=62.23;MLEAC=2;MLEAF=0.500;MQ=60.00;MQ0=0;MQRankSum=0.322;NCC=0;QD=10.74;ReadPosRankSum=0.377;SOR=0.446;CSQ=missense_variant|cGg/cAg|R/Q|ENSG00000153404|PLEKHG4B|ENST00000283426|16/18|||1076|protein_coding,non_coding_transcript_exon_variant&non_coding_transcript_variant|||ENSG00000153404|PLEKHG4B|ENST00000504041|5/8||||retained_intron  GT:AD:DP:GQ:PL  0/1:7,6:13:99:171,0,208 0/1:5,3:8:83:83,0,145

You can see that `VEP` has added:

```
CSQ=missense_variant|cGg/cAg|R/Q|ENSG00000153404|PLEKHG4B|ENST00000283426|16/18|||1076|protein_coding,non_coding_transcript_exon_variant&non_coding_transcript_variant|||ENSG00000153404|PLEKHG4B|ENST00000504041|5/8||||retained_intron
```

This is further composed of two annotations for this variant:

```
missense_variant|cGg/cAg|R/Q|ENSG00000153404|PLEKHG4B|ENST00000283426|16/18|||1076|protein_coding
```

and

```
non_coding_transcript_exon_variant&non_coding_transcript_variant|||ENSG00000153404|PLEKHG4B|ENST00000504041|5/8||||retained_intron
```

The first of these is saying that this variant is a missense variant in
the gene PLEKHG4B for the transcript ENST00000283426 and the second that
it is also a non_coding_transcript_exon_variant in the transcript
ENST00000504041.
