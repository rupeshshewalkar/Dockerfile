##Docker file
## This is simple webserver container for centos 6 
##
FROM centos:6
MAINTAINER rupesh rupesh.shewalkar@gmail.com

RUN yum -y update && yum clean all
RUN yum -y install httpd
ADD ./index.html /var/www/html/index.html
EXPOSE 80
RUN echo "/sbin/service httpd start" >>/root/.bashrc 
