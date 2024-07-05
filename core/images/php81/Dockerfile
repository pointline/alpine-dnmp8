FROM php:8.1.29-fpm-alpine
#FROM php:8.0.30-fpm-alpine

LABEL author="peter@xulukun.cn"

# 安装 PHP 依赖
RUN apk add --no-cache curl icu-dev libzip-dev oniguruma-dev autoconf build-base freetype-dev libjpeg-turbo-dev libpng-dev libxml2-dev libxslt-dev icu-data-full
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install bcmath gd intl opcache pdo_mysql zip soap xsl sockets

# 清理不再需要的文件
RUN apk del autoconf build-base

# 安装 composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer
RUN export PATH="$PATH:/usr/local/bin"
