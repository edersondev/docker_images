FROM ubuntu
LABEL maintainer="Ederson Ferreira <ederson.dev@gmail.com>"

RUN apt-get update && apt-get install -y \
php \
php-cli \
php-mysql \
php-odbc \
php-pgsql \
php-sqlite3 \
postgresql-client \
mysql-client \
curl \
nano \
&& apt-get clean && apt-get autoclean && apt-get autoremove \
&& rm -rf /var/lib/apt/lists/*

VOLUME /home

# Install composer
WORKDIR /usr/local/bin/
RUN curl -sS https://getcomposer.org/installer | php
RUN chmod +x composer.phar
RUN mv composer.phar composer
RUN composer self-update

# Install drush
RUN composer global require drush/drush

# Set path bin
WORKDIR /root
RUN echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bashrc

WORKDIR /home