FROM ubuntu:latest
MAINTAINER Josh

###Install postfix and make the set up non-responsive###
RUN apt-get update -y \
&& DEBIAN_FRONTEND=noninteractive \
&& echo "postfix postfix/mailname string localdomain" | debconf-set-selections \
&& echo "postfix postfix/main_mailer_type string 'Internet Site' " | debconf-set-selections \
&& apt-get install -y postfix rsyslog

ENTRYPOINT service postfix start && bash


