FROM ubuntu:20.04
ENV DEBIAN_FRONTEND=nonintercative

LABEL version="1"
LABEL software="PlasmidSeeker"
LABEL software.version="1.0"
LABEL description="A k-mer based program for the identification of known plasmids from bacterial whole genome sequencing reads"
LABEL website="https://github.com/bioinfo-ut/PlasmidSeeker"
LABEL license="https://github.com/bioinfo-ut/PlasmidSeeker/blob/master/LICENSE"

# install dependencies
RUN apt-get update && apt-get -y install \
  perl \
  r-base-core \
  r-base \
  r-base-dev \
  wget \
  libclang-dev && apt-get clean

# install perl and git

RUN mkdir program && cd program ; \
  wget https://github.com/bioinfo-ut/PlasmidSeeker/archive/refs/tags/1.3.tar.gz ;\
  tar -zxf 1.3.tar.gz ; \
  rm -rf 1.3.tar.gz
  
ENV PATH="${PATH}:/program/PlasmidSeeker-1.3:/program/PlasmidSeeker-1.3/GenomeTester4:" \
  LC_ALL=C

# PlasmidSeeker databse
RUN cd /program/PlasmidSeeker-1.3 ; \
  wget http://bioinfo.ut.ee/plasmidseeker/plasmidseeker_db_w20_Nov-2021.tar.gz ; \
  tar -vzxf plasmidseeker_db_w20_Nov-2021.tar.gz ; \
  rm plasmidseeker_db_w20_Nov-2021.tar.gz

ENV PLASMIDSEEKER_DBHOME="/program/PlasmidSeeker-1.3/db_w20"

ENV LC_ALL=C

WORKDIR /data
