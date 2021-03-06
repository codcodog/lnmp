ARG PHP_VERSION
FROM php:${PHP_VERSION}-fpm

LABEL maintainer "codcodog codcodog@gmail.com"

RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list \
    && apt-get update && apt-get install -y \
            libfreetype6-dev \
            libjpeg62-turbo-dev \
            libpng-dev \
            libmcrypt-dev \
            git \
            unzip \
            --no-install-recommends \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && pecl install mcrypt-1.0.2 \
    && docker-php-ext-enable mcrypt \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-install -j$(nproc) mysqli \
    && docker-php-ext-install -j$(nproc) bcmath \
    && pecl install -o -f redis \
    && rm -rf /tmp/pear

RUN ["/bin/bash", "-c", "set -o pipefail \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://mirrors.cloud.tencent.com/composer/"]

CMD ["php-fpm"]
