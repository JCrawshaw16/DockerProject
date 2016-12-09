FROM dockerproject_myjava
MAINTAINER Josh

#Use root user privileges

USER root

##Make sure everything is up to date
RUN apt-get update -y
RUN apt-get install -y wget

##Set working directory

WORKDIR /opt

##Pull jira file from online##
RUN wget https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-software-7.3.0-EAP-20161114153314-x64.bin 
RUN chmod a+x atlassian-jira-software-7.3.0-EAP-20161114153314-x64.bin

#COPY response.varfile /opt/
##Start Jira service##

RUN printf "o\n2\n/opt/atlassian/jira\n/var/atlassian/application-data/jira\n2\n8081\n8005\ny\ni\ny\n" | ./atlassian-jira-software-7.3.0-EAP-20161114153314-x64.bin
EXPOSE 8081 

ENTRYPOINT service jira start && bash
