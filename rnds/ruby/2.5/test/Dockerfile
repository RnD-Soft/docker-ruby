FROM rnds/ruby:2.5

RUN set -ex && \
  apk add --no-cache \
    xvfb \
    unixodbc-dev \
    libltdl \
    gconf \
    imagemagick \
    ttf-liberation \
    pango \
    proxychains-ng \
    binutils

ENV CHROMIUM=/usr/bin/chromium-browser

RUN set -ex && \
  apk add --no-cache chromium chromium-chromedriver \
  && mv ${CHROMIUM} ${CHROMIUM}.orig \
  && echo "#!/bin/sh" >> ${CHROMIUM} \
  && echo "exec ${CHROMIUM}.orig --no-sandbox --disable-gpu --disable-sandbox --user-data-dir=/tmp/ \$@" >> ${CHROMIUM} \
  && chmod 777 ${CHROMIUM}  \
  && gem install docker_toolkit \
  && gem update docker_toolkit \
  && apk add --no-cache docker \
  && curl -sSLo /tmp/consul.zip https://releases.hashicorp.com/consul/1.2.2/consul_1.2.2_linux_amd64.zip \
  && unzip -d /bin /tmp/consul.zip && strip /bin/consul && rm -rf /tmp/consul.zip \
  && mkdir -p /tmp/consul \
  && curl https://releases.rancher.com/cli2/v2.0.5/rancher-linux-amd64-v2.0.5.tar.gz | tar -xz \
  && cp ./rancher-*/rancher /bin/rancher \
  && rm -rf rancher-* \
  && curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl \
  && mv ./kubectl /bin \
  && chmod +x /bin/kubectl \
  && apk add --no-cache py-pip python-dev \
  && pip install docker-compose \
  && apk del python-dev py-pip

WORKDIR /home/app

 
CMD ["tail", "-f", "/dev/null"]


