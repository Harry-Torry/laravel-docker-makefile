FROM php:7.1-fpm

RUN apt-get update && apt-get install -y \
    curl \
    git-all \
    unzip \
    libssl-dev \
    zlib1g-dev \
    libicu-dev \
    libpng12-dev \
    libmcrypt-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libzip-dev

RUN docker-php-ext-install pdo_mysql mbstring mcrypt zip intl opcache && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-configure intl && \
    docker-php-ext-install -j$(nproc) gd

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

RUN usermod -u 1000 www-data
WORKDIR /var/www/html
