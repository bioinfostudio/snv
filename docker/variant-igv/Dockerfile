FROM gcr.io/wise-cycling-267806/igvtools
USER root
RUN conda install -c bioconda ensembl-vep==99.2 
RUN ln -s /mnt/genome/snv/alignment/normal/normal.sorted.dup.recal.bam.tdf /home/bioinfo/snv/alignment/normal/
RUN ln -s /mnt/genome/snv/alignment/tumour/tumour.sorted.dup.recal.bam.tdf /home/bioinfo/snv/alignment/tumour/
WORKDIR /home/bioinfo/snv/variants/
RUN ln -s /mnt/genome/snv/variants/HC.chr5.60Mb.vcf.gz /home/bioinfo/snv/variants/
RUN ln -s /mnt/genome/snv/homo_sapiens /home/bioinfo/snv/homo_sapiens
RUN chown -R bioinfo:bioinfo /home/bioinfo/snv
USER bioinfo
WORKDIR /home/bioinfo/snv/
