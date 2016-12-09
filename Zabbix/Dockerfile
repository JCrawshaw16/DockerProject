FROM ubuntu:latest
MAINTAINER Josh

##Set up LAMP server###

RUN apt-get update -y \
&& apt-get -y install debconf-utils \
apache2 \
mysql-client \
php7.0-mysql php7.0-curl php7.0-json php7.0-cgi php7.0 libapache2-mod-php7.0 php7.0-bcmath php7.0-mbstring php7.0-xml \
wget

RUN sed -i '/;date.timezone =/c\date.timezone = UTC /' /etc/php/7.0/apache2/php.ini

###Automate mySQL password ###
RUN \
echo 'mysql-server mysql-server/root_password password 123' | debconf-set-selections \
&& echo 'mysql-server mysql-server/root_password_again password 123' | debconf-set-selections
RUN apt-get install -y mysql-server

##Install and unpackage Zabbix##
WORKDIR /opt/
RUN wget http://repo.zabbix.com/zabbix/3.2/ubuntu/pool/main/z/zabbix-release/zabbix-release_3.2-1+xenial_all.deb
RUN dpkg -i zabbix-release_3.2-1+xenial_all.deb
RUN apt-get update -y
RUN apt-get -y install zabbix-server-mysql zabbix-frontend-php zabbix-agent


##Create database schema###

RUN \
service mysql start \
#&& mysql -u root -p123 -e "create user 'zabbix';" \
&& mysql -u root -p123 -e "CREATE DATABASE zabbixdb character set utf8 collate utf8_bin;" \
&& mysql -u root -p123 -e "GRANT ALL PRIVILEGES on zabbixdb.* to zabbix@localhost IDENTIFIED by '123';" \
&& mysql -u root -p123 -e "FLUSH PRIVILEGES;"

WORKDIR /usr/share/doc/zabbix-server-mysql
  
RUN \
service mysql start \
&& zcat create.sql.gz | mysql -u root -p123 zabbixdb

###Edit zabbix configuration file###

WORKDIR /etc/zabbix/

RUN \
sed -i '/# DBHost=/c\DBHost=localhost' zabbix_server.conf \
&& sed -i '/DBName=zabbix/c\DBName=zabbixdb' zabbix_server.conf \
&& sed -i '/# DBPassword=/c\DBPassword=123' zabbix_server.conf \
&& sed -i '/# DBPort=/c\DBPort=3306' zabbix_server.conf

RUN service apache2 restart && service zabbix-server restart

ENTRYPOINT service mysql start && service apache2 start && service zabbix-server start && service zabbix-agent start && bash


