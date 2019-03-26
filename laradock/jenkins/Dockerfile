# Use an official Python runtime as a parent image
FROM jenkins/jenkins:latest

USER root

RUN apt-get update && \
	apt-get install -y ruby-full wget curl git

#install capistrano http://capistranorb.com/
RUN /bin/bash -l -c "gem install capistrano"
RUN /bin/bash -l -c "gem install capistrano-locally"

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

# Install composer and add its bin to the PATH.
RUN curl -s http://getcomposer.org/installer | php && \
    echo "export PATH=${PATH}:/var/www/vendor/bin" >> ~/.bashrc && \
    mv composer.phar /usr/local/bin/composer