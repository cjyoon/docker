FROM ubuntu:focal
ENV DEBIAN_FRONTEND noninteractive

# Upgrade installed packages
RUN apt-get update && apt-get install -y -f autoconf automake make gcc perl zlib1g-dev libbz2-dev liblzma-dev libcurl4-gnutls-dev libssl-dev libncurses5-dev bwa bedtools build-essential python3.8 python3.8-venv python3-pip python3.8-dev git wget vim less software-properties-common python-is-python3 openjdk-8-jdk

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9 && \
	add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/' && \
	apt update && apt install -y r-base-dev libxml2 libxml2-dev

# Install samblater
RUN mkdir tools && cd tools & git clone git://github.com/GregoryFaust/samblaster.git && cd samblaster && make && cp samblaster /usr/local/bin/ && cd $HOME

# Install Htslib
RUN cd tools && wget https://github.com/samtools/htslib/releases/download/1.11/htslib-1.11.tar.bz2 && \
    tar xvfj htslib-1.11.tar.bz2 && \
    cd htslib-1.11 &&  ./configure && make && make install && cd $HOME 

# Install samtools
RUN cd tools && wget https://github.com/samtools/samtools/releases/download/1.11/samtools-1.11.tar.bz2 && \
    tar xvfj samtools-1.11.tar.bz2 && \
    cd samtools-1.11 &&  ./configure && make && make install && cd $HOME


# Install Java requirement and Varscan
RUN wget  -O /tools/VarScan.jar https://github.com/dkoboldt/varscan/releases/download/2.4.2/VarScan.v2.4.2.jar

# Install VT 
RUN cd tools && wget https://github.com/atks/vt/archive/0.5772.tar.gz && tar -zxvf 0.5772.tar.gz && cd vt-0.5772/ && make && cp vt /usr/local/bin/ && cd $HOME

# Install bcftools
RUN cd tools && wget https://github.com/samtools/bcftools/releases/download/1.9/bcftools-1.9.tar.bz2 && tar --bzip2 -xf bcftools-1.9.tar.bz2 && cd bcftools-1.9 && make && make install && cd $HOME


# Install R packages
RUN R -e "install.packages('BiocManager', dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "BiocManager::install('ComplexHeatmap')"
RUN R -e "install.packages('circlize', dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('gridBase', dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('optparse', dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('tidyverse', dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('gridExtra', dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('cowplot', dependencies=TRUE, repos='http://cran.rstudio.com/')"

# Install python3 packages
RUN pip3 install pysam cyvcf2 snakemake numpy pandas matplotlib scipy 

# Download GATK3.8 
RUN cd tools && wget https://storage.googleapis.com/gatk-software/package-archive/gatk/GenomeAnalysisTK-3.8-1-0-gf15c1c3ef.tar.bz2 && tar xjvf GenomeAnalysisTK-3.8-1-0-gf15c1c3ef.tar.bz2 && mv GenomeAnalysisTK-3.8-1-0-gf15c1c3ef/GenomeAnalysisTK.jar . && rm -rf GenomeAnalysisTK-3.8-1-0-gf15c1c3ef* && cd $HOME
# Download picard
RUN cd tools && wget https://github.com/broadinstitute/picard/releases/download/2.25.0/picard.jar && cd $HOME

# Download Sambamba
RUN cd tools && wget https://github.com/biod/sambamba/releases/download/v0.6.8/sambamba-0.6.8-linux-static.gz && gunzip sambamba-0.6.8-linux-static.gz && mv sambamba-0.6.8-linux-static /usr/local/bin/sambamba && chmod +x /usr/local/bin/sambamba && cd $HOME 

# Clean up
RUN cd tools && rm -f *.tar.bz2 && rm -f *.tar.gz && cd $HOME 

