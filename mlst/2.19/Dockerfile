FROM ubuntu:20.04

LABEL software="mlst"
LABEL software.version="2.19.0"
LABEL description="Scan contig files against PubMLST typing schemes"
LABEL website="https://github.com/tseemann/mlst"
LABEL license="https://github.com/tseemann/mlst/blob/master/LICENSE"
LABEL maintainer="Sang-Ic Kim"
LABEL maintainer.email="sang-ic.kim@fmc.com"

# install dependencies
RUN apt-get update && apt-get install -y wget \
 libmoo-perl \
 liblist-moreutils-perl \
 libjson-perl \
 gzip \
 file

# install ncbi-blast+

RUN mkdir program

RUN cd /program ; \
 wget ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/2.12.0/ncbi-blast-2.12.0+-x64-linux.tar.gz ; \
 tar -xzf ncbi-blast-2.12.0+-x64-linux.tar.gz ; \
 rm ncbi-blast-2.12.0+-x64-linux.tar.gz

ENV PATH="$PATH:/program/ncbi-blast-2.12.0+/bin" \
 LC_ALL=C

# install any2fasta
RUN cd /program ; \
  mkdir any2fasta && cd any2fasta ; \
  wget https://raw.githubusercontent.com/tseemann/any2fasta/master/any2fasta ; \
  chmod +x any2fasta

ENV PATH="$PATH:/program/any2fasta" \
 LC_ALL=C

# install mlst 2.19
RUN cd /program ; \
 wget https://github.com/tseemann/mlst/archive/v2.19.0.tar.gz ; \
 tar -xzf v2.19.0.tar.gz ; \
 rm v2.19.0.tar.gz

ENV PATH="$PATH:/program/mlst-2.19.0/bin" \
 LC_ALL=C

# check dependencies and list available schemes
RUN mlst --check && mlst --list

WORKDIR /data
