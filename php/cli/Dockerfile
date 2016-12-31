FROM php:5.6-alpine
MAINTAINER Rafael Nery <rafael@nery.info>
#dependencies
RUN apk add --update postgresql-dev sqlite-dev mariadb-dev && mkdir /app

#Composer && PHPUNI
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && php composer-setup.php && php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer \
    curl -fsSL https://phar.phpunit.de/phpunit.phar > phpunit.phar && chmod +x phpunit.phar && mv phpunit.phar /usr/local/bin/phpunit

#Extensions
RUN docker-php-ext-install pdo pdo_mysql pdo_pgsql pdo_sqlite iconv

#socket 
EXPOSE 9000
workdir "/app"
#project
VOLUME ["/app"]
