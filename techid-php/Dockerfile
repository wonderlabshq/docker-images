FROM php:7.2-fpm
MAINTAINER hanif@wonderlabs.io

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    default-libmysqlclient-dev \
    libbz2-dev \
    libmemcached-dev \
    curl \
    git \
    libfreetype6-dev \
    libicu-dev \
    libjpeg-dev \
    libmagickcore-dev \
    libmemcachedutil2 \
    libpng-dev \
    libssl-dev \
    libxml2-dev \
    zlib1g-dev \
    build-essential \
    gnupg --no-install-recommends

RUN curl -sL https://deb.nodesource.com/setup_9.x | bash -
RUN apt-get install -y nodejs

RUN docker-php-ext-install bcmath bz2 calendar iconv intl json mbstring mysqli pdo_mysql phar xml zip
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd
RUN docker-php-ext-install exif
RUN pecl install apcu && docker-php-ext-enable apcu
RUN pecl install memcached && docker-php-ext-enable memcached.so
RUN pecl install redis && docker-php-ext-enable redis.so
RUN apt-get purge -y --auto-remove default-libmysqlclient-dev libbz2-dev libmemcached-dev
RUN rm -r /var/lib/apt/lists/*
RUN npm install -g bower

ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && ln -s $(composer config --global home) /root/composer
ENV PATH $PATH:/root/composer/vendor/bin

RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Asia/Jakarta /etc/localtime
RUN "date"

