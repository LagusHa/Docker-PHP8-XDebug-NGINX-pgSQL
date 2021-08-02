FROM php:8.0-cli-alpine

RUN apk add --no-cache postgresql-dev bash coreutils \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo_pgsql

RUN apk add --no-cache unzip \
    libzip-dev \
    zip \
    && docker-php-ext-install zip

COPY ./php/conf.d /usr/local/etc/php/conf.d

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/bin --filename=composer --quiet \
    && rm -rf /root/.composer/cache

ENV COMPOSER_ALLOW_SUPERUSER 1

WORKDIR /var/www