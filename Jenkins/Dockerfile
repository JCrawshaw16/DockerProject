FROM dockerproject_myjava
MAINTAINER Josh


####Installing Jenkins###
RUN wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | apt-key add -
RUN sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
RUN apt-get update -y
RUN apt-get install jenkins -y
 
###Start Jenkins###
CMD service jenkins start && tail -F /var/log/jenkins/error.log


