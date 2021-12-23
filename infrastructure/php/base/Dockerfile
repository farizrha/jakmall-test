FROM php:8.0.3-fpm-alpine3.13 AS builderfpm

WORKDIR /var/www/html

RUN rm -rf ${PHP_INI_DIR}/php.ini-development \
    && mv ${PHP_INI_DIR}/php.ini-production ${PHP_INI_DIR}/php.ini \
    && apk add --no-cache --virtual .build-deps \
    g++ \
    make \
    autoconf \
    && pecl install -o -f redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis \
    && docker-php-ext-install bcmath pdo_mysql opcache \
    && apk del --purge .build-deps

FROM php:8.0.3-cli-alpine3.13 AS buildercli

WORKDIR /var/www/html

RUN rm -rf ${PHP_INI_DIR}/php.ini-development \
    && mv ${PHP_INI_DIR}/php.ini-production ${PHP_INI_DIR}/php.ini \
    && apk add --no-cache --virtual .build-deps \
    g++ \
    make \
    autoconf \
    && pecl install -o -f redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis \
    && docker-php-ext-install bcmath pdo_mysql \
    && apk del --purge .build-deps
