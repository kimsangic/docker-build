# base image
FROM ubuntu:20.04

# For easy upgrade later. ARG varibles only persist during docker image build time
LABEL software="Abricate"
LABEL software.version="1.0.0"
LABEL description="Mass screening of contigs for AMR or virulence genes"
LABEL website="https://github.com/tseemann/abricate"

# install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
  bioperl \
  gzip \
  unzip \
  liblist-moreutils-perl \
  libjson-perl \
  libtext-csv-perl \
  libfile-slurp-perl \
  liblwp-protocol-https-perl \
  libwww-perl \
  libpath-tiny-perl \
  git \
  ncbi-blast+ \
  wget && \
  apt-get autoclean && rm -rf /var/lib/apt/lists/*

# install any2fasta
RUN cd /usr/local/bin && \
  wget https://raw.githubusercontent.com/tseemann/any2fasta/master/any2fasta && \
  chmod +x any2fasta

# install abricate 1.0.0
RUN mkdir program && cd program ; \
  wget https://github.com/tseemann/abricate/archive/refs/tags/v1.0.0.tar.gz ; \
  tar -zxvf v1.0.0.tar.gz ; \
    rm -rf v1.0.0.tar.gz

# set $PATH
ENV PATH="${PATH}:/program/abricate-1.0.0/bin:" \
  LC_ALL=C

# test
RUN abricate --check && \
    abricate --setupdb

WORKDIR /data
