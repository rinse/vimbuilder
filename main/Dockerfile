FROM ubuntu AS builder

MAINTAINER rinse

ENV DEBIAN_FRONTEND="noninteractive"

RUN set -x \
  && sed -i 's/^#\s*deb-src/deb-src/g' /etc/apt/sources.list \
  && apt update \
  && apt build-dep -y vim \
  && apt install -y \
    build-essential \
    git \
  && :

ARG version=master
ARG config_args="--with-features=huge \
                 --enable-fail-if-missing \
                 --enable-fontset \
                 --enable-multibyte \
                 --enable-terminal \
                 "

WORKDIR /usr/local/src/

RUN git clone https://github.com/vim/vim.git \
  && cd ./vim \
    && git pull \
    && git checkout $version \
  && cd ./src \
    && ./configure $config_args \
    && make \
    && make install \
    && :

