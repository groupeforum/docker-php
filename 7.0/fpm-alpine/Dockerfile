FROM php:7.0-fpm-alpine

MAINTAINER Florian GIRARDEY <fgirardey@groupeforum.pro>

# install the PHP extensions we need
RUN apk add --update freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev \
    && docker-php-ext-configure gd \
        --with-gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-configure mbstring --enable-mbstring \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install opcache \
    && rm -rf /tmp/* /var/cache/apk/*

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=60'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini

# Set WordPress PHP.ini settings
RUN { \
		echo 'memory_limit=64M'; \
		echo 'max_execution_time=30'; \
		echo 'post_max_size=64M'; \
		echo 'upload_max_filesize=64M'; \
	} > /usr/local/etc/php/conf.d/custom-wordpress.ini