FROM php:5.6-fpm-alpine

MAINTAINER Rafael Nery <rafael@nery.info>

ENV PHALCON_VERSION=3.0.1 

RUN apk add --update gcc make autoconf musl-dev file postgresql-dev sqlite-dev mariadb-dev


# Phalcon Compile
RUN curl -LO https://github.com/phalcon/cphalcon/archive/v${PHALCON_VERSION}.tar.gz && \
    tar xzf v${PHALCON_VERSION}.tar.gz && cd cphalcon-${PHALCON_VERSION}/build && sh install && \
    echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini && \
    cd ../.. && rm -rf v${PHALCON_VERSION}.tar.gz cphalcon-${PHALCON_VERSION}
    
# Phalcon DevTools
  
RUN curl -LO https://github.com/phalcon/phalcon-devtools/archive/v${PHALCON_VERSION}.tar.gz && \
    tar xzf v${PHALCON_VERSION}.tar.gz && \    
    mv phalcon-devtools-${PHALCON_VERSION} /usr/local/phalcon-devtools && \
    ln -s /usr/local/phalcon-devtools/phalcon.php /usr/local/bin/phalcon

#Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && php composer-setup.php && php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

#PHPUnit && #Codeception
RUN curl -fsSL https://phar.phpunit.de/phpunit.phar > phpunit.phar && chmod +x phpunit.phar && mv phpunit.phar /usr/local/bin/phpunit && \
    curl -fsSL http://codeception.com/codecept.phar > codecept.phar && chmod +x codecept.phar && mv codecept.phar /usr/local/bin/codecept

#Clean Then All
RUN apk del gcc make autoconf musl-dev file --purge && rm -rf /var/cache/apk/*

#EXTENSIONS
RUN docker-php-ext-install pdo pdo_mysql pdo_pgsql pdo_sqlite

#socket 
EXPOSE 9000

#project
VOLUME ["/var/www/html"]
