FROM ubuntu
LABEL maintainer="Ederson Ferreira <ederson.dev@gmail.com>"

ENV TZ=America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

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
php-pclzip \
php-soap \
php-xdebug \
php-xml \
php-zip \
php-apcu \
php-pear \
php-dev \
phpunit \
curl \
nano \
alien \
&& apt-get clean && apt-get autoclean && apt-get autoremove \
&& rm -rf /var/lib/apt/lists/*

RUN a2enmod rewrite

ENV APACHE_LOCK_DIR="/var/lock"
ENV APACHE_PID_FILE="/var/run/apache2.pid"
ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="/var/log/apache2"

LABEL Description="Webserver php 7 and mod oci"

VOLUME /var/www/html

ENV TZ=America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Copia o arquivo de virtualhost
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

# Install composer
WORKDIR /usr/local/bin/
RUN curl -sS https://getcomposer.org/installer | php
RUN chmod +x composer.phar
RUN mv composer.phar composer
RUN composer self-update

# Set path bin
WORKDIR /root
RUN echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bashrc

# Install Oracle Instant Client
COPY ./oracle_instantclient /root/oracle_instantclient
WORKDIR /root/oracle_instantclient
RUN alien -i oracle-instantclient12.2-basic-*.rpm
RUN alien -i oracle-instantclient12.2-sqlplus-*.rpm
RUN alien -i oracle-instantclient12.2-devel-*.rpm

# Install oci8 extension to access Oracle Database
RUN pecl install oci8

# Create file on modules availabe
RUN echo -e "; configuration for php oracle module\nextension=oci8.so" > /etc/php/7.2/mods-available/oci8.ini

# Enable mod
RUN phpenmod oci8

WORKDIR /var/www/html

# Remove alien
RUN apt-get purge -y alien
RUN apt-get -y autoremove

# Remove files oracle instant client
RUN rm -rf /root/oracle_instantclient

COPY apache2-foreground.sh /scripts/
RUN chmod +x /scripts/*

EXPOSE 80

CMD ["/scripts/apache2-foreground.sh"]
