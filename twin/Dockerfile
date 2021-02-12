# cjyoon/python3.8:1.0.0
#FROM python:3.8
FROM ubuntu:focal 
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y -f autoconf automake make gcc perl zlib1g-dev libbz2-dev liblzma-dev libcurl4-gnutls-dev libssl-dev libncurses5-dev default-jre bwa bedtools build-essential python3.8 python3-pip python3.8-dev git wget 
RUN pip3 install pysam cyvcf2 snakemake matplotlib pandas scipy
RUN mkdir tools && cd tools & git clone git://github.com/GregoryFaust/samblaster.git && cd samblaster && make && cp samblaster /usr/local/bin/ && cd $HOME
RUN cd tools && wget https://github.com/samtools/htslib/releases/download/1.11/htslib-1.11.tar.bz2 && \
    tar xvfj htslib-1.11.tar.bz2 && \
    mv htslib-1.11 htslib && cd htslib &&  ./configure && make && make install && cd $HOME
RUN cd tools && wget https://github.com/samtools/samtools/releases/download/1.11/samtools-1.11.tar.bz2 && \
    tar xvfj samtools-1.11.tar.bz2 && \
    cd samtools-1.11 &&  ./configure && make && make install && cd $HOME


# Install Java requirement and Varscan
RUN wget  -O /usr/local/bin/VarScan.jar https://github.com/dkoboldt/varscan/releases/download/2.4.2/VarScan.v2.4.2.jar

# Install VT 
RUN cd tools && wget https://github.com/atks/vt/archive/0.5772.tar.gz && tar -zxvf 0.5772.tar.gz && cd vt-0.5772/ && make && cp vt /usr/local/bin/ && cd $HOME

# Install bcftools
RUN cd tools && wget https://github.com/samtools/bcftools/archive/1.9.tar.gz && tar -zxvf 1.9.tar.gz && cd bcftools-1.9 && make && make install && cd $HOME 
