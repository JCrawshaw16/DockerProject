FROM ubuntu:latest
MAINTAINER Josh

#Get wget command 
RUN apt-get update -y
RUN apt-get install wget -y


##Pull java tar file from the internet and store in /opt##
WORKDIR /opt
RUN wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u112-b15/jdk-8u112-linux-x64.tar.gz

#Unzip java file 
RUN tar zxvf jdk-8u112-linux-x64.tar.gz

#Install java##

RUN update-alternatives --install /usr/bin/java java /opt/jdk1.8.0_112/bin/java 100
RUN update-alternatives --install /usr/bin/javac javac /opt/jdk1.8.0_112/bin/javac 100

