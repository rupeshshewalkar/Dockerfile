############################################################
# Dockerfile to
# Based on Ubuntu
############################################################

FROM ubuntu:14.04

MAINTAINER shewalkar.rupesh@gmail.com

# Add User
RUN useradd -ms /bin/bash docker

# Let the conatiner know that there is no tty
#ENV DEBIAN_FRONTEND noninteractive

#Initial Update & upgrade
RUN apt-get update

# TimeZone
RUN ln -sf /usr/share/zoneinfo/Asia/Kolkata /etc/localtime




## Install Basic Requirements
RUN apt-get install -y build-essential git python python-setuptools python-dev rcs emacs24 libjpeg-dev memcached libevent-dev libfreetype6-dev zlib1g-dev nginx curl g++ make python-software-properties software-properties-common supervisor
RUN easy_install pip
RUN apt-get install -y --no-install-recommends ca-certificates numactl

RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
RUN curl -o /usr/local/bin/gosu -SL "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture)" \
        && curl -o /usr/local/bin/gosu.asc -SL "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture).asc" \
        && gpg --verify /usr/local/bin/gosu.asc \
        && rm /usr/local/bin/gosu.asc \
        && chmod +x /usr/local/bin/gosu

RUN apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys 492EAFE8CD016A07919F1D2B9ECBEC467F0CEB10


RUN echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.1 multiverse" > /etc/apt/sources.list.d/mongodb-org.list

# Add External Repos in a conatiner
RUN add-apt-repository -y ppa:nginx/stable
RUN add-apt-repository ppa:mc3man/trusty-media
RUN add-apt-repository ppa:chris-lea/node.js
RUN apt-get update

# install uwsgi now because it takes a little while
RUN pip install uwsgi nodeenv

#Nginx/ffmpeg/nodejs
RUN apt-get install -y sqlite3 ffmpeg gstreamer0.10-ffmpeg nodejs
RUN npm install -g bower
# install our code
ADD . /home/docker/code/
RUN mv /home/docker/code/bower_components /home/docker/code/gstudio/gnowsys-ndf/gnowsys_ndf/ndf/static/ndf/
RUN cp /home/docker/code/emacs /root/.emacs
RUN cp /home/docker/code/gstudio/gnowsys-ndf/gnowsys_ndf/wsgi.py /home/docker/code/gstudio/gnowsys-ndf/wsgi.py

RUN pip install -r /home/docker/code/gstudio/requirements.txt


################## MongoDBINSTALLATION ######################
# Install MongoDB Following the Instructions at MongoDB Docs
# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r mongodb && useradd -r -g mongodb mongodb
RUN set -x \
        && apt-get install -y \
                mongodb-org-unstable \
                mongodb-org-unstable-server \
                mongodb-org-unstable-shell \
                mongodb-org-unstable-mongos \
                mongodb-org-unstable-tools \
        && rm -rf /var/lib/mongodb \
        && mv /etc/mongod.conf /etc/mongod.conf.orig


#Nginx Configuration
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN rm /etc/nginx/sites-enabled/default
RUN ln -s /home/docker/code/nginx-app.conf /etc/nginx/sites-enabled/
RUN ln -s /home/docker/code/supervisor-app.conf /etc/supervisor/conf.d/

# MangoDB Configuration
RUN mkdir -p /data/db && chown -R mongodb:mongodb /data/db
VOLUME /data/db


# Preparation of Gnowsis
RUN pip install -U pyyaml nltk


# Expose Private
EXPOSE 80
EXPOSE 27017

#Run Script


RUN /usr/bin/python "/home/docker/code/nltk-initialization.py"
RUN mkdir -p /home/docker/code/gstudio/gnowsys-ndf/gnowsys_ndf/ndf/management/commands/schema_files
CMD /home/docker/code/initialize.sh
