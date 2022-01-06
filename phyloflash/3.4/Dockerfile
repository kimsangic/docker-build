# base image
FROM ubuntu:20.04
ENV DEBIAN_FRONTEND=nonintercative

# metadata
LABEL container.version="1"
LABEL software="phylofalsh"
LABEL software.version="3.4"
LABEL description="Taxonomic sequence classifier"
LABEL website="https://github.com/HRGV/phyloFlash"
LABEL license="https://github.com/HRGV/phyloFlash/blob/master/LICENSE"
LABEL maintainer="Sang-Ic Kim"
LABEL maintainer.email="sang-ic.kim@fmc.com"

# install dependencies
RUN apt-get update && apt-get -y install \
  bowtie \
  cpanminus \
  default-jre \
  g++ \
  libbz2-dev \
  libclang-dev \
  liblzma-dev \
  mafft \
  make \
  perl \
  python\
  rsync \
  samtools \
  wget \
  zlib1g-dev

## phyloflash

# install bbmap 38.94
RUN mkdir program && cd program ; \
  cd program ; \
  wget https://sourceforge.net/projects/bbmap/files/BBMap_38.94.tar.gz -P /program ; \
  tar -zxf BBMap_38.94.tar.gz ; \
  rm -rf BBMap_38.94.tar.gz

ENV PATH="$PATH:/program/bbmap:" \
  LC_ALL=C

# install vsearch 2.18.0
RUN wget https://github.com/torognes/vsearch/releases/download/v2.18.0/vsearch-2.18.0-linux-x86_64.tar.gz ; \
  tar xzf vsearch-2.18.0-linux-x86_64.tar.gz ; \
  rm -rf vsearch-2.18.0-linux-x86_64.tar.gz ; \
  mv ./vsearch-2.18.0-linux-x86_64/bin/vsearch /usr/bin ; \
  chmod a+X /usr/bin/vsearch

# install spades 2.29.1
RUN  wget http://cab.spbu.ru/files/release3.15.3/SPAdes-3.15.3-Linux.tar.gz ; \
  tar -xzf SPAdes-3.15.3-Linux.tar.gz ; \
  rm -rf SPAdes-3.15.3-Linux.tar.gz

ENV PATH="$PATH:/program/SPAdes-3.15.3-Linux/bin:" \
  LC_ALL=C

# install bedtools 2.30.0
RUN wget https://github.com/arq5x/bedtools2/releases/download/v2.29.1/bedtools-2.29.1.tar.gz ; \
  tar -zxvf bedtools-2.29.1.tar.gz ; \
  rm -rf bedtools-2.29.1.tar.gz ; \
  cd bedtools2 ; \
  make ; \
  make install

# install phyloflash 3.4
RUN cd program ; \
  wget https://github.com/HRGV/phyloFlash/archive/pf3.4.tar.gz ; \
  tar -xzf pf3.4.tar.gz

ENV PATH="$PATH:/program/phyloFlash-pf3.4:" \
  LC_ALL=C

# 16S database SILVA_138.1
RUN cd program/phyloFlash-pf3.4 ; \
  wget https://ftp.ncbi.nlm.nih.gov/pub/UniVec/UniVec ; \
  wget https://www.arb-silva.de/fileadmin/silva_databases/release_138/Exports/SILVA_138_SSURef_NR99_tax_silva_trunc.fasta.gz ; \
  phyloFlash_makedb.pl \
      --univec_file ./UniVec \
      --silva_file ./SILVA_138_SSURef_NR99_tax_silva_trunc.fasta.gz \
  rm UniVec/UniVec ; \
  rm SILVA_138_SSURef_NR99_tax_silva_trunc.fasta.gz
    
ENV PHYLOFLASH_DBHOME="/program/phyloFlash-pf3.5/138"

WORKDIR /data
