# base image
FROM ubuntu:20.04

# metadata
LABEL container.version="1"
LABEL software1="Kraken"
LABEL software1.version="1.1.1"
LABEL description1="Taxonomic sequence classifier"
LABEL website1="https://github.com/DerrickWood/kraken"
LABEL license1="https://github.com/DerrickWood/kraken/blob/master/LICENSE"
LABEL software2="KronaTools"
LABEL software2.version="2.8"
LABEL description2="Interactively explore metagenomes and more from a web browser"
LABEL website2="https://github.com/marbl/Krona"
LABEL license2="https://github.com/marbl/Krona/blob/master/KronaTools/LICENSE.txt"
LABEL maintainer="Sang-Ic Kim"
LABEL maintainer.email="sang-ic.kim@fmc.com"

# install dependencies
RUN apt-get update && apt-get -y install \
  wget \
  curl \
  zlib1g-dev \
  make \
  g++ \
  rsync \
  cpanminus

# download kraken 1.1.1
RUN mkdir program && cd program ; \
  mkdir /program/kraken ; \
  wget https://github.com/DerrickWood/kraken/archive/v1.1.1.tar.gz ; \
  tar -xzf v1.1.1.tar.gz ; \
  rm -rf v1.1.1.tar.gz ; \
  cd kraken-1.1.1 ; \
  ./install_kraken.sh /program/kraken/ ; \
  cd .. ; \
  rm -r /program/kraken-1.1.1

ENV PATH="$PATH:/program/kraken" \
    LC_ALL=C

# install perl module and rsync required for kraken-build
RUN cpanm Getopt::Std

# MiniKraken database: minikraken_20171019_8GB
RUN cd program/kraken ; \
  wget http://ccb.jhu.edu/software/kraken/dl/minikraken_20171019_8GB.tgz ; \
  tar -zxf minikraken_20171019_8GB.tgz ; \
  rm -rf minikraken_20171019_8GB.tgz

ENV KRAKEN_DBHOME="/program/kraken/minikraken_20171019_8GB"

# Install krona 2.8
RUN cd program ; \
  wget https://github.com/marbl/Krona/releases/download/v2.8/KronaTools-2.8.tar ; \
  tar -xvf KronaTools-2.8.tar ; \
  rm -rf KronaTools-2.8.tar ; \
  cd /program/KronaTools-2.8/ ; \
  ./install.pl -prefix /program/KronaTools-2.8  ; \
  ./updateTaxonomy.sh
 
ENV PATH="$PATH:/program/KronaTools-2.8/bin" \
    LC_ALL=C

WORKDIR /data
