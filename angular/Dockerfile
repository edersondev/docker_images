FROM ubuntu
LABEL maintainer="Ederson Ferreira <ederson.dev@gmail.com>"

RUN apt-get update && apt-get install -y \
curl \
nano

RUN curl -sL https://deb.nodesource.com/setup_8.x
RUN apt-get update && apt-get install -y \
nodejs \
build-essential

RUN npm install -g typescript@latest
RUN npm install -g @angular/cli@latest

VOLUME /home

RUN apt-get clean && apt-get autoclean && apt-get autoremove \
rm -rf /var/lib/apt/lists/*