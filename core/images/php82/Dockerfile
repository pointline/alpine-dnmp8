FROM php:8.2.33-fpm-alpine3.23
#FROM php:8.0.30-fpm-alpine
LABEL author="peter@xulukun.cn"

# 修改源文件
RUN echo 'https://dl-cdn.alpinelinux.org/alpine/v3.21/main' > /etc/apk/repositories \
    && echo 'https://dl-cdn.alpinelinux.org/alpine/v3.21/community' >> /etc/apk/repositories

# 安装 PHP 依赖

# 运行时依赖
RUN apk add --no-cache \
    curl \
    icu-libs \
    libzip \
    freetype \
    libjpeg-turbo \
    libpng \
    libxml2 \
    libxslt \
    icu-data-full

# 编译依赖
RUN apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS \
    icu-dev \
    libzip-dev \
    oniguruma-dev \
    linux-headers \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libxml2-dev \
    libxslt-dev

# GD
RUN docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg

# Magento 所需 PHP 扩展
RUN docker-php-ext-install -j$(nproc) \
    bcmath \
    gd \
    intl \
    opcache \
    pdo_mysql \
    soap \
    sockets \
    xsl \
    zip

# 删除编译依赖
RUN apk del .build-deps

# 安装 composer
# RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
# RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
# RUN php composer-setup.php
# RUN php -r "unlink('composer-setup.php');"
# RUN mv composer.phar /usr/local/bin/composer
WORKDIR /var/www/html
