#
#--------------------------------------------------------------------------
# php 7.4 srv
#--------------------------------------------------------------------------
#

ARG PHP_VERSION=7.4.28
FROM chinayin/php:${PHP_VERSION}-fpm-slim
LABEL maintainer="chinayin <whereismoney@qq.com>"

RUN set -eux \
    ## Install gd
    && install_packages libjpeg-dev libpng-dev libwebp-dev libfreetype6-dev \
    && docker-php-ext-configure gd --prefix=/usr --enable-gd --with-webp --with-jpeg --with-freetype \
    && docker-php-ext-install -j$(nproc) gd \
    ## Install pdftk (https://www.pdflabs.com/docs/install-pdftk-on-redhat-or-centos)
    ## fix error processing package openjdk-11-jre-headless:amd64
    && mkdir -p /usr/share/man/man1 \
    && install_packages pdftk \
    ## Clean up
    && rm -rf /tmp/* /var/tmp/* \
    && rm -f /var/log/lastlog /var/log/faillog \
    ## Check PHP version
    && php -v
