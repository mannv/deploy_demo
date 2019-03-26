# Use an official Python runtime as a parent image
FROM jenkins/jenkins:latest

USER root

RUN apt-get update && \
	apt-get install -y wget curl git

#https://www.rosehosting.com/blog/install-ruby-on-rails-on-ubuntu-16-04/
#install ruby to install capistrano
RUN gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB && \
	cd /tmp && \curl -sSL https://get.rvm.io -o rvm.sh && \
	cat /tmp/rvm.sh | bash -s stable

RUN /bin/bash -c "source /usr/local/rvm/scripts/rvm" && \
	/bin/bash -l -c "rvm install 2.3.0"

#install capistrano http://capistranorb.com/
RUN /bin/bash -l -c "gem install capistrano"
RUN /bin/bash -l -c "gem install capistrano-locally"

#init ruby evironment
RUN echo 'source /usr/local/rvm/scripts/rvm' >> /etc/bash.bashrc

#install php
RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get install -y apt-transport-https lsb-release ca-certificates

RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
	echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list && \
	apt update


RUN apt-get install -y php7.2-cli \
    php7.2-common \
    php7.2-curl \
    php7.2-intl \
    php7.2-json \
    php7.2-xml \
    php7.2-mbstring \
    php7.2-mysql \
    php7.2-pgsql \
    php7.2-sqlite \
    php7.2-sqlite3 \
    php7.2-zip \
    php7.2-bcmath \
    php7.2-gd \
    php7.2-dev

RUN apt-get install -y pkg-config \
    libcurl4-openssl-dev \
    libedit-dev \
    libssl-dev \
    libxml2-dev \
    xz-utils \
    libsqlite3-dev \
    sqlite3 \
    curl \
    nano \
    postgresql-client