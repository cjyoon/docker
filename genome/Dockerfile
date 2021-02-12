# cjyoon/python3.8:1.0.0
FROM ubuntu:focal
ENV DEBIAN_FRONTEND noninteractive

# Upgrade installed packages
RUN apt-get update && apt-get install -y -f autoconf automake make gcc perl zlib1g-dev libbz2-dev liblzma-dev libcurl4-gnutls-dev libssl-dev libncurses5-dev default-jre bwa bedtools build-essential python3.8 python3.8-venv python3-pip python3.8-dev git wget vim less software-properties-common python-is-python3

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
RUN wget  -O /usr/local/bin/VarScan.jar https://github.com/dkoboldt/varscan/releases/download/2.4.2/VarScan.v2.4.2.jar

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