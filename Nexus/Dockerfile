FROM dockerproject_myjava
MAINTAINER Josh

##Get updates##
RUN apt-get update -y
RUN apt-get install -y wget

##Change working directory
WORKDIR /opt

##Get nexus tarball and unzip

RUN wget http://download.sonatype.com/nexus/3/latest-unix.tar.gz
 
RUN tar zxvf latest-unix.tar.gz

ENTRYPOINT ./nexus-3.1.0-04/bin/nexus start && bash
