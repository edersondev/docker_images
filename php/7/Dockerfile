FROM ubuntu
LABEL maintainer="Ederson Ferreira <ederson.dev@gmail.com>"

RUN apt-get update && apt-get install -y \
apache2 \
libapache2-mod-php \
php \
php-cli \
php-common \
php-curl \
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
php-xdebug \
php-xml \
php-zip \
php-apcu \
phpunit \
composer \
mysql-client \
nano \
&& apt-get clean && apt-get autoclean && apt-get autoremove \
&& rm -rf /var/lib/apt/lists/*

RUN a2enmod rewrite

ENV APACHE_LOCK_DIR="/var/lock"
ENV APACHE_PID_FILE="/var/run/apache2.pid"
ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="/var/log/apache2"

LABEL Description="Webserver php 7"

VOLUME /var/www/html

ENV TZ=America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Copia o arquivo de virtualhost
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

# Install and config Laravel
WORKDIR /root
RUN composer global require "laravel/installer"
RUN echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bashrc

EXPOSE 80

ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]