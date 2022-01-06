FROM ubuntu:20.04

# for easy upgrade later. ARG variables only persist during image build time
LABEL container.version="1"
LABEL software1="Mash"
LABEL software1.version="2.3"
LABEL description1="Fast genome and metagenome distance estimation using MinHash"
LABEL website1="http://mash.readthedocs.org"
LABEL maintainer="Sang-Ic Kim"
LABEL maintainer.email="sang-ic.kim@fmc.com"

# install dependencies
RUN apt-get update && apt-get -y install \
  gzip \
  wget \
  zlib1g-dev
  
RUN mkdir program

# install mash 2.3
RUN  cd program ; \
 wget https://github.com/marbl/Mash/releases/download/v2.3/mash-Linux64-v2.3.tar ; \
 tar -xvf mash-Linux64-v2.3.tar ; \
 rm -rf mash-Linux64-v2.3.tar
 
# set path
ENV PATH="$PATH:/program/mash-Linux64-v2.3" \
 LC_ALL=C

# mash db
RUN cd /program/mash-Linux64-v2.3 ; \
 wget https://obj.umiacs.umd.edu/mash/screen/RefSeq88n.msh.gz ; \
 gunzip RefSeq88n.msh.gz ; \
 rm -rf RefSeq88n.msh.gz

ENV MASH_DBHOME="/program/mash-Linux64-v2.3/RefSeq88n.msh"

WORKDIR /data
