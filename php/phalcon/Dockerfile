FROM php:5.6-fpm-alpine

MAINTAINER Rafael Nery <rafael@nery.info>

ENV PHALCON_VERSION=3.0.1 

RUN apk add --update gcc make autoconf musl-dev file

# Phalcon Compile

RUN set -xe && \
    curl -LO https://github.com/phalcon/cphalcon/archive/v${PHALCON_VERSION}.tar.gz && \
    tar xzf v${PHALCON_VERSION}.tar.gz && cd cphalcon-${PHALCON_VERSION}/build && sh install && \
    echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini && \
    cd ../.. && rm -rf v${PHALCON_VERSION}.tar.gz cphalcon-${PHALCON_VERSION} && \
    curl -LO https://github.com/phalcon/phalcon-devtools/archive/v${PHALCON_VERSION}.tar.gz && \
    tar xzf v${PHALCON_VERSION}.tar.gz
    
RUN set -xe && mv phalcon-devtools-${PHALCON_VERSION} /usr/local/phalcon-devtools && \
    ln -s /usr/local/phalcon-devtools/phalcon.php /usr/local/bin/phalcon

RUN set -xe && mv composer.phar /usr/local/bin/composer \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    php -r "if (hash_file('SHA384', 'composer-setup.php') === 'aa96f26c2b67226a324c27919f1eb05f21c248b987e6195cad9690d5c1ff713d53020a02ac8c217dbf90a7eacc9d141d') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    php composer-setup.php \
    php -r "unlink('composer-setup.php');"
    
