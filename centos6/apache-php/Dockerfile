##Docker file
## This is simple webserver with php container for centos 6 
##
FROM centos:centos6
MAINTAINER rupesh rupesh.shewalkar@gmail.com

RUN yum -y update && yum clean all
RUN yum -y install httpd php
ADD ./index.php /var/www/html/index.php
EXPOSE 80
RUN echo "/sbin/service httpd start" >>/root/.bashrc 
