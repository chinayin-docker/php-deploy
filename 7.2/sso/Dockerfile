#
#--------------------------------------------------------------------------
# php 7.2 sso
#--------------------------------------------------------------------------
#

ARG PHP_VERSION=7.2.34
FROM chinayin/php:${PHP_VERSION}-fpm-slim
LABEL maintainer="chinayin <whereismoney@qq.com>"

RUN set -eux \
    ## Install PHP opcache
    && docker-php-ext-configure opcache --enable-opcache && docker-php-ext-install -j$(nproc) opcache \
    && echo "opcache.enable=0" >> "$PHP_INI_DIR/conf.d/docker-php-ext-opcache.ini" \
    ## Install gd
    && install_packages libjpeg-dev libpng-dev libwebp-dev libfreetype6-dev \
    && docker-php-ext-configure gd --prefix=/usr --with-gd --with-webp-dir --with-jpeg-dir --with-png-dir --with-zlib-dir --with-freetype-dir \
    && docker-php-ext-install -j$(nproc) gd \
    ## Clean up
    && rm -rf /tmp/* /var/tmp/* \
    && rm -f /var/log/lastlog /var/log/faillog \
    ## Check PHP version
    && php -v
