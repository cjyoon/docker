# cjyoon/r4:1.1.0
FROM rocker/verse:4.0.1
RUN R -e "install.packages('BiocManager',dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "install.packages(c('cowplot', 'gridExtra'), dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "BiocManager::install('ComplexHeatmap')"
RUN R -e "install.packages('circlize', dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('gridBase', dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('optparse', dependencies=TRUE, repos='http://cran.rstudio.com/')"

