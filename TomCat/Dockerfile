FROM dockerproject_myjava
MAINTAINER Josh

RUN apt-get install wget -y \
&& apt-get update -y

##Get tar file and unzip ##

WORKDIR /opt/

RUN wget http://mirror.catn.com/pub/apache/tomcat/tomcat-9/v9.0.0.M13/bin/apache-tomcat-9.0.0.M13.tar.gz
RUN tar zvxf apache-tomcat-9.0.0.M13.tar.gz

WORKDIR ~
RUN echo "export JAVA_HOME="/opt/jdk1.8.0_112"" >> /etc/environment \
&& echo "export JRE_HOME="/opt/jdk1.8.0_122/jre"" >> /etc/environment \
&& echo "export CATALINA_HOME="/opt/apache-tomcat-9.0.0.M13"" >> /etc/environment
RUN sh -c . /.bashrc

###Create a manager login with username tomcat and password s3cret###
RUN sed -i '/<Context>/c\<Context reloadable="true">' /opt/apache-tomcat-9.0.0.M13/conf/context.xml \
&& sed -i '22i <role rolename="manager-gui"/>' /opt/apache-tomcat-9.0.0.M13/conf/tomcat-users.xml \
&& sed -i '22i <user username="tomcat" password="s3cret" roles="manager-gui"/>' /opt/apache-tomcat-9.0.0.M13/conf/tomcat-users.xml   



#WORKDIR /usr/local/tomcat
#RUN useradd -s /sbin/nologin -d /opt/tomcat/temp tomcat
#RUN chown -R tomcat:tomcat /opt/apache-tomcat-9.0.0.M13 \
#&& chmod -R 750 /opt/apache-tomcat-9.0.0.M13

###Manually start tomcat server###
WORKDIR /opt
ENTRYPOINT ./apache-tomcat-9.0.0.M13/bin/startup.sh && tail -F /var/lib/tomcat/error.log

