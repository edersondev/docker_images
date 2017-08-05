FROM ubuntu

RUN apt-get update && apt-get install -y \
apache2 \
php \
php-cli \
php-common \
php-curl \
php-dev \
php-gd \
php-ldap \
php-mysql \
php-odbc \
php-pgsql \
php-sqlite3 \
php-bz2 \
php-imagick \
php-json \
php-mbstring \
php-mcrypt \
php-pclzip \
php-soap \
php-twig \
php-xdebug \
php-xml \
php-zip \
php-apcu \
phpunit \
composer \
mysql-client \
nano \
&& apt-get clean

RUN a2enmod rewrite

ENV APACHE_LOCK_DIR="/var/lock"
ENV APACHE_PID_FILE="/var/run/apache2.pid"
ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="/var/log/apache2"

LABEL Description="Webserver php 7"

VOLUME /var/www/html

# Copia o arquivo de virtualhost
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

EXPOSE 80

ENTRYPOINT service apache2 start && /bin/bash