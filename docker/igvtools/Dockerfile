FROM gcr.io/wise-cycling-267806/alignment-metrics
USER root
RUN conda install -c bioconda/label/cf201901 igvtools
COPY variant_calling /home/bioinfo/snv/variant_calling/
RUN chown -R bioinfo:bioinfo /home/bioinfo/snv/variant_calling
USER bioinfo
