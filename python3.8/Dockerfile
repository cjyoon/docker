# cjyoon/python3.8:1.0.0
FROM python:3.8
RUN pip3 install pysam cyvcf2 snakemake matplotlib pandas
RUN apt-get update && apt-get install -y bwa bedtools
RUN mkdir tools && cd tools & git clone git://github.com/GregoryFaust/samblaster.git && cd samblaster && make && cp samblaster /usr/local/bin/ && cd $HOME
RUN cd tools && wget https://github.com/samtools/htslib/releases/download/1.11/htslib-1.11.tar.bz2 && \
    tar xvfj htslib-1.11.tar.bz2 && \
    cd htslib-1.11 &&  ./configure && make && make install && cd $HOME 
RUN cd tools && wget https://github.com/samtools/samtools/releases/download/1.11/samtools-1.11.tar.bz2 && \
    tar xvfj samtools-1.11.tar.bz2 && \
    cd samtools-1.11 &&  ./configure && make && make install && cd $HOME
