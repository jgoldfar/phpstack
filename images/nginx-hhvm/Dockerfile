# Use phusion/baseimage as base image. To make your builds
# reproducible, make sure you lock down to a specific version, not
# to `latest`! See
# https://github.com/phusion/baseimage-docker/blob/master/Changelog.md
# for a list of version numbers.
FROM phusion/baseimage:0.9.13
MAINTAINER jgoldfar@gmail.com
LABEL version="1.0"

# Set correct environment variables.
ENV HOME /root

# Regenerate SSH host keys. baseimage-docker does not contain any, so you
# have to do that yourself. You may also comment out this instruction; the
# init system will auto-generate one during boot.
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# install add-apt-repository
RUN sudo apt-get update
RUN sudo apt-get install -y software-properties-common python-software-properties

# we'll need wget to fetch the key...
RUN sudo apt-get install -y wget

# install nginx
RUN sudo apt-get install -y nginx
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# install hhvm
RUN wget -O - http://dl.hhvm.com/conf/hhvm.gpg.key | apt-key add -
RUN echo deb http://dl.hhvm.com/ubuntu trusty main | tee /etc/apt/sources.list.d/hhvm.list
RUN apt-get update
RUN apt-get install -y hhvm

RUN mkdir /etc/service/nginx
ADD nginx.sh /etc/service/nginx/run
RUN chmod 700 /etc/service/nginx/run

RUN mkdir /etc/service/hhvm
ADD hhvm.sh /etc/service/hhvm/run
RUN chmod 700 /etc/service/hhvm/run

# Add /var/www and sites-enabled to image
VOLUME ["/var/www", "/etc/nginx/sites-enabled"]

RUN sudo /usr/share/hhvm/install_fastcgi.sh

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# expose port 80 and 9000
EXPOSE 80 9000
