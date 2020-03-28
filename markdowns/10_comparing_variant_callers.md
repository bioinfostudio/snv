# Comparing variant callers

Now we have variants from all three methods. Let’s compress and index
the VCFs for future visualisation.

```bash
for i in variant_calling/*.vcf; do bgzip $i; done
for i in variant_calling/*.vcf.gz; do tabix -p vcf $i; done
```

Let’s look at a compressed VCF. Details on the VCF spec can be found [here](https://vcftools.github.io/specs.html).

    zless -S variant_calling/varscan.snp.vcf.gz

Fields vary from caller to caller. Some values are almost always there:

* Ref vs. alt alleles
* Variant quality (QUAL column)
* The per-sample genotype (GT) values.

Note on VCF fields:

  > **DP**: Raw read depth  
  > **GT**: Genotype  
  > **PL**: List of Phred-scaled genotype likelihoods. (min is better)  
  > **SP**: Phred-scaled strand bias P-value  
  > **GQ**: Genotype Quality  


## Looking at the three vcf files, how can we detect only somatic variants?

Some commands to find somatic variant in the vcf file:

varscan:

    zcat variant_calling/varscan.snp.vcf.gz | grep -v "^#" | grep SOMATIC

MuTecT:

    zcat variant_calling/mutect.filtered.vcf.gz | grep -v "^#"

Strelka:

    zcat variant_calling/strelka.vcf.gz | grep -v "^#"
