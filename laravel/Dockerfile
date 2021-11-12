FROM php:8.0-fpm-alpine

ARG TZ
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer

RUN set -eux && \
    apk add --update-cache --no-cache --virtual=.build-dependencies tzdata && \
    apk del .build-dependencies && \
    docker-php-ext-install bcmath pdo_mysql && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
    composer config -g repos.packagist composer https://packagist.jp && \
    composer self-update --1 && \
    apk add npm

ENV APP_ROOT /work
RUN mkdir -p $APP_ROOT
WORKDIR $APP_ROOT
COPY . ${APP_ROOT}
RUN chown www-data storage/ -R
