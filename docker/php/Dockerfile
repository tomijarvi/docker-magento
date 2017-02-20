FROM php:5.6-fpm-alpine

MAINTAINER Tomi Jarvi <tomi@jarvi.pro>

RUN apk upgrade --update \
    && apk add bash \
	&& apk add --no-cache --virtual .build-deps \
        autoconf \
        curl-dev \
		freetype-dev \
        g++ \
        icu-dev \
        libjpeg-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libxml2-dev \
        make \
        openssl-dev \
        sqlite-dev \ 
        ssmtp \
    && docker-php-ext-install \
        curl ftp hash iconv intl json mcrypt mbstring mysql mysqli pdo_mysql pdo_sqlite pcntl phar session simplexml tokenizer xml xmlrpc zip \
    && docker-php-ext-configure \
        gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install \
        gd \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && sed -i '1 a xdebug.remote_autostart=1' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && sed -i '1 a xdebug.remote_enable=1' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && find / -type f -iname \*.apk-new -delete \
    && rm -rf /var/cache/apk/*

COPY php.ini /usr/local/etc/php/conf.d/php.ini

WORKDIR /var/www/html

CMD ["php-fpm"]