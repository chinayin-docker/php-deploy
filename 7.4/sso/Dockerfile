#
#--------------------------------------------------------------------------
# php 7.4 sso
#--------------------------------------------------------------------------
#

ARG PHP_VERSION=7.4.29
FROM chinayin/php:${PHP_VERSION}-fpm-slim
LABEL maintainer="chinayin <whereismoney@qq.com>"

RUN set -eux \
    ## Install gd
    && install_packages libjpeg-dev libpng-dev libwebp-dev libfreetype6-dev \
    && docker-php-ext-configure gd --prefix=/usr --enable-gd --with-webp --with-jpeg --with-freetype \
    && docker-php-ext-install -j$(nproc) gd \
    ## Clean up
    && rm -rf /tmp/* /var/tmp/* \
    && rm -f /var/log/lastlog /var/log/faillog \
    ## Check PHP version
    && php -v
