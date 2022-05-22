FROM php:7.4-fpm-alpine

RUN apk update && apk --no-cache add zlib-dev g++ icu-dev

RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl
RUN docker-php-ext-install pdo pdo_mysql

RUN apk --no-cache add \
        libzip-dev \
        zip \
  && docker-php-ext-install zip

RUN apk update && apk --no-cache add libpng-dev

RUN apk update && \
    apk --no-cache add \
        autoconf make

RUN docker-php-ext-install gd

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --filename=composer \
    && php -r "unlink('composer-setup.php');" \
    && mv composer /usr/local/bin/composer

COPY php.ini /usr/local/etc/php/conf.d/php.ini

RUN pecl install apcu

RUN pear config-set php_ini /application/docker/php-fpm/php.ini

CMD ["php-fpm"]

EXPOSE 9000
