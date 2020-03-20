FROM gcr.io/wise-cycling-267806/variantcall
USER root
RUN conda install -c bioconda/label/cf201901 igvtools
COPY *.vcf.gz /home/bioinfo/snv/variant_calling/
COPY *.vcf.gz.tbi /home/bioinfo/snv/variant_calling/
RUN chown -R bioinfo:bioinfo /home/bioinfo/snv/variant_calling
USER bioinfo
