FROM php:5.6-apache

# apache mod rewrite
RUN a2enmod rewrite \
    && a2enmod headers \
    && a2enconf other-vhosts-access-log

# xdebug
RUN pecl install xdebug \
	&& docker-php-ext-enable xdebug

# composer
RUN curl -sS https://getcomposer.org/installer | php \
	&& mv composer.phar /usr/bin/composer

COPY ./config/php.ini /usr/local/etc/php/conf.d/php-additional.ini

ENV PHPREDIS_VERSION=2.2.7

# additional packages
RUN apt-get update \
	&& apt-get install -y \
		git \
		php5-mysql \
		libssl-dev \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libicu-dev \
    && cd /usr/src/php/ext \
    && curl -q https://codeload.github.com/phpredis/phpredis/tar.gz/$PHPREDIS_VERSION | tar -xz \
    && docker-php-ext-install -j$(nproc) mcrypt pdo_mysql zip mysqli intl phpredis-$PHPREDIS_VERSION \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
	&& rm -rf /var/lib/apt/lists/*
