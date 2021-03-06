---
title:  "bioinformatics-fastqtools"
date: 2017-10-31 00:00:00
author: Alain Domissy
tags: 
- ubuntu
- debian
- bioinformatics
- fastqtools
- fastq
- scif
- singularity
files:
 - fastqtools
 - SingularityApp.fastqtools
 
---

```yaml
%appinstall bioinformatics-fastqtools
    apt-get -y install wget
    apt-get -y install autoconf libtool build-essential
    apt-get -y install libpcre3 libpcre3-dev
    apt-get -y install zlibc libz-dev
    apt-get clean
    wget https://github.com/dcjones/fastq-tools/archive/v0.8.tar.gz -O fastq-tools-0.8.tar.gz
    tar --extract --gzip --file fastq-tools-0.8.tar.gz
    rm fastq-tools-0.8.tar.gz
    cd fastq-tools-0.8
    ./autogen.sh && ./configure && make
    cd ..
    cp  fastq-tools-0.8/src/fastq-grep    bin/grep
    cp  fastq-tools-0.8/src/fastq-kmers   bin/kmers
    cp  fastq-tools-0.8/src/fastq-match   bin/match
    cp  fastq-tools-0.8/src/fastq-uniq    bin/uniq
    cp  fastq-tools-0.8/src/fastq-qual    bin/qual
    cp  fastq-tools-0.8/src/fastq-sample  bin/sample
    cp  fastq-tools-0.8/src/fastq-qualadj bin/qualadj
    cp  fastq-tools-0.8/src/fastq-qscale  bin/qscale
    chmod u+x bin/*
    rm -rf fastq-tools-0.8
%appfiles bioinformatics-fastqtools
    fastqtools bin/
%appenv bioinformatics-fastqtools
    FASTQTOOLS_HOME=/scif/apps/bioinformatics-fastqtools
    export FASTQTOOLS_HOME
%apphelp bioinformatics-fastqtools
    fastq-tools provide a number of small and efficient programs to perform common tasks
    with high throughput sequencing data in the FASTQ format.
    All of the programs work with typical FASTQ files as well as gzipped FASTQ files.
    It is recommended to create the following alias:
    alias fastqtools="singularity run --app bioinformatics-fastqtools \${SINGULARITY_CONTAINER}"
    More help is then available by running
    fastqtools --help
%apprun bioinformatics-fastqtools
    exec /bin/bash fastqtools "$@"
%applabels bioinformatics-fastqtools
    MAINTAINER adomissy@ucsd.edu
    BUILD_VERSION 0.0.1
    WRAPPEDTOOL_VERSION 0.8
    WRAPPEDTOOL_INFO https://homes.cs.washington.edu/~dcjones/fastq-tools/
```
