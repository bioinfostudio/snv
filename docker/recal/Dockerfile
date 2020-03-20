FROM gcr.io/wise-cycling-267806/markdup
USER root
RUN conda install mosdepth
USER bioinfo
RUN ln -s /mnt/genome/snv/alignment/normal/normal.sorted.dup.recal.bam /home/bioinfo/snv/alignment/normal/
RUN ln -s /mnt/genome/snv/alignment/normal/normal.sorted.dup.recal.bai /home/bioinfo/snv/alignment/normal/
RUN ln -s /mnt/genome/snv/alignment/normal/normal.sorted.dup.recal.table /home/bioinfo/snv/alignment/normal/
RUN ln -s /mnt/genome/snv/alignment/tumour/tumour.sorted.dup.recal.bam /home/bioinfo/snv/alignment/tumour/
RUN ln -s /mnt/genome/snv/alignment/tumour/tumour.sorted.dup.recal.bai /home/bioinfo/snv/alignment/tumour/
RUN ln -s /mnt/genome/snv/alignment/tumour/tumour.sorted.dup.recal.table /home/bioinfo/snv/alignment/tumour/
