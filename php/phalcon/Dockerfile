FROM php:5.6-fpm-alpine

MAINTAINER Rafael Nery <rafael@nery.info>

ENV PHALCON_VERSION=3.0.1

RUN apk add --update gcc make autoconf 

# Phalcon Compile

RUN set -xe && \
        curl -LO https://github.com/phalcon/cphalcon/archive/v${PHALCON_VERSION}.tar.gz && \
        tar xzf v${PHALCON_VERSION}.tar.gz && cd cphalcon-${PHALCON_VERSION}/build && sh install && \
        echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini && \
        cd ../.. && rm -rf v${PHALCON_VERSION}.tar.gz cphalcon-${PHALCON_VERSION} && \
    curl -LO https://github.com/phalcon/phalcon-devtools/archive/v${PHALCON_VERSION}.tar.gz && \
    tar xzf v${PHALCON_VERSION}.tar.gz && \
    mv phalcon-devtools-${PHALCON_VERSION} /usr/local/phalcon-devtools && \
    ln -s /usr/local/phalcon-devtools/phalcon.php /usr/local/bin/phalcon
