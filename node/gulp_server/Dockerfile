FROM       node:4.7.0-alpine
MAINTAINER Rafael Nery <rafael@nery.info>

RUN        mkdir -p /application
RUN        npm -g install gulp bower

WORKDIR    /application

COPY       ./entrypoint.sh /entrypoint.sh
RUN        chmod +x /entrypoint.sh

VOLUME     ["/application"]
ENTRYPOINT ["/entrypoint.sh"] 
