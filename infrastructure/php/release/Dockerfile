FROM php-fpm AS builderfpm

WORKDIR /var/www/html

FROM php-cli AS buildercli

WORKDIR /var/www/html

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=./ --filename=composer \

ENTRYPOINT php artisan config:cache
