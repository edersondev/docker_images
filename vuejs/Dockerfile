FROM ubuntu
LABEL maintainer="Ederson Ferreira <ederson.dev@gmail.com>"

RUN groupadd --gid 1000 node \
  && useradd --uid 1000 --gid node --shell /bin/bash --create-home node

RUN apt-get update && apt-get install -y \
curl \
nano \
gnupg

RUN curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get update && apt-get install -y \
nodejs 

RUN npm i -g @vue/cli

VOLUME /home

WORKDIR /home

RUN apt-get clean && apt-get autoclean && apt-get autoremove \
&& rm -rf /var/lib/apt/lists/*

EXPOSE 8080