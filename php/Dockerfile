FROM php:8.2-fpm

# timezone
ENV TZ=Asia/Tokyo

# change owner
RUN chown www-data:www-data -R ./

RUN apt-get update \
    && apt-get -y install git \
    zip \
    unzip \
    g++ \
    vim
    # libzip-dev \
    # libonig-dev \
    # libbz2-dev \
    # libmcrypt-dev \
    # libxml2-dev \
    # libjpeg-dev \
    # nodejs \
    # npm \

# PHP拡張
RUN docker-php-ext-install \
    pdo \
    # pdo_mysql
    bcmath

# php zip
RUN apt-get install -y zip \
    libzip-dev \
    && docker-php-ext-install zip \
    && docker-php-ext-configure zip

# php pdo_pgsql
RUN apt-get install -y libpq-dev \
    && docker-php-ext-install pdo_pgsql

# php intl
RUN apt-get install -y libicu-dev \
    && docker-php-ext-install intl

# php gd
RUN apt-get install -y zlib1g-dev \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    && docker-php-ext-install gd \
    && docker-php-ext-configure gd \
    --with-freetype=/usr/include/ \
    --with-jpeg=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# Composer
# RUN curl -sS https://getcomposer.org/installer | php && \
#     mv composer.phar /usr/local/bin/composer && \
#     chmod +x /usr/local/bin/composer


RUN apt-get clean
