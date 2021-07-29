FROM php:8.0-cli-alpine AS builder

RUN apk add --no-cache postgresql-dev \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo_pgsql opcache

RUN apk add --no-cache unzip

ENV COMPOSER_ALLOW_SUPERUSER 1

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/bin --filename=composer --quiet \
    && rm -rf /root/.composer/cache

WORKDIR /var/www

COPY ./composer.json ./composer.lock ./

RUN composer install --no-dev --no-scripts --prefer-dist --optimize-autoloader \
    && rm -rf /root/.composer/cache

### CLI ###

FROM php:8.0-cli-alpine

RUN apk add --no-cache postgresql-dev bash coreutils \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo_pgsql opcache

COPY ./docker/production/php/conf.d /usr/local/etc/php/conf.d

WORKDIR /var/www

COPY --from=builder /var/www ./
COPY ./ ./

RUN php bin/console cache:warmup