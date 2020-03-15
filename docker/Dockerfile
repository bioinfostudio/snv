FROM broadinstitute/gatk
WORKDIR /
RUN apt-get update --fix-missing
RUN apt-get install -qq bzip2 git gcc g++ make python zlib1g-dev wget
RUN apt-get clean && apt-get purge && rm -rf /var/lib/apt/lists/* /tmp/*

RUN curl -LO https://github.com/Illumina/strelka/releases/download/v2.9.10/strelka-2.9.10.release_src.tar.bz2 && \
    tar -xvf strelka-2.9.10.release_src.tar.bz2 && \
    rm -rf strelka-2.9.10.release_src.tar.bz2 && \
    mkdir build && cd build && \
    ../strelka-2.9.10.release_src/configure && \
    make install

RUN wget -O /usr/local/bin/VarScan.jar https://github.com/dkoboldt/varscan/releases/download/2.4.2/VarScan.v2.4.2.jar
RUN conda config --add channels bioconda
RUN conda install ensembl-vep

## create a non-root user
RUN useradd -ms /bin/bash bioinfo
WORKDIR /home/bioinfo/snv
RUN ln -s /mnt/genome/snv /home/bioinfo/snv/
# setup the user directory
RUN chown -R bioinfo:bioinfo /home/bioinfo
RUN echo 'export PS1=" \W\$ "' >> /home/bioinfo/.bashrc
# become the bioinfo
USER bioinfo
ENV HOME /home/bioinfo
WORKDIR /home/bioinfo/
