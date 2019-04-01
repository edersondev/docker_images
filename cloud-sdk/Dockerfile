FROM ubuntu
LABEL maintainer="Ederson Ferreira <ederson.dev@gmail.com>"

RUN groupadd --gid 1000 node \
  && useradd --uid 1000 --gid node --shell /bin/bash --create-home googlecloud

RUN apt-get update && apt-get install -y \
lsb-release \
curl \
nano \
wget \
gnupg

RUN export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
    echo "deb https://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" > /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    apt-get update -y && apt-get install google-cloud-sdk -y

RUN apt-get install kubectl

RUN apt-get clean && apt-get autoclean && apt-get autoremove \
&& rm -rf /var/lib/apt/lists/*

VOLUME /home

WORKDIR /home
