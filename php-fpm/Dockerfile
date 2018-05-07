######
# See: https://hub.docker.com/_/php/
######

FROM php:7.1-fpm

#RUN usermod -u 1000 www-data

######
# You can install php extensions using docker-php-ext-install
######

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install pdo pdo_mysql mysqli
#&& pecl install -o -f redis \
#&& rm -rf /tmp/pear \
#    && docker-php-ext-enable redis

