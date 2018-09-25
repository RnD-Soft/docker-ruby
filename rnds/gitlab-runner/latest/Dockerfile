FROM docker:18.03
MAINTAINER Firmhouse "kinnalru@gmail.com"

WORKDIR /home/app

RUN mkdir -p ~/.ssh && echo -e "Host * \
  \n  StrictHostKeyChecking no \
  \n  UserKnownHostsFile=/dev/null\n" >> ~/.ssh/config


RUN set -ex \
  && apk add --no-cache \
    ca-certificates \
    tar \
    xz \
    autoconf \
    bison \
    bzip2 \
    bzip2-dev \
    bash \
    postgresql-dev \
    postgresql-client \
    libstdc++ \
    libressl \
    libressl-dev \
    sqlite \
    sqlite-dev \
    libxml2 \
    wget \
    python \
    curl \
    libcurl \
    curl-dev \
    tzdata \
    pcre \
    git \
    socat \
    openssh

RUN set -ex \
  && apk add --no-cache \
    linux-headers \
    coreutils \
    dpkg-dev \
    dpkg \
    gdbm-dev \
    libffi-dev \
    libxml2-dev \
    libxslt-dev \
    ncurses-dev \
    procps \
    readline-dev \
    make \
    gcc \
    g++ \
    ruby \
    ruby-libs \
    ruby-dev \
    glib-dev \
    libc-dev \
    yaml-dev \
    zlib-dev


RUN echo 'gem: --no-ri --no-rdoc' > ~/.gemrc \
  && gem install docker_toolkit --no-ri --no-rdoc \
  && gem update docker_toolkit --no-ri --no-rdoc

RUN set -ex \
  && apk add --no-cache \
    nodejs \
    python-dev \
    py-setuptools

RUN set -ex \
  && easy_install-2.7 pip && pip install docker-compose==1.20.1

RUN mv -f /usr/bin/docker-compose /usr/bin/docker-compose.orig

COPY docker-compose /usr/bin/

RUN chmod +x /usr/bin/docker-compose

RUN gem install rspec activesupport bigdecimal json awesome_print \
                httparty bundler socksify net-ssh io-console --no-ri --no-rdoc

CMD ["/bin/bash"]




