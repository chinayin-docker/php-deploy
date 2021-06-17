#
#--------------------------------------------------------------------------
# php 7.2 srv
#--------------------------------------------------------------------------
#

FROM chinayin/php:7.2-fpm-slim
LABEL maintainer="chinayin <whereismoney@qq.com>"

ENV CYD_APP_NAME="7.2-fpm-srv" \
    CYD_IMAGE_VERSION="v2021-06-17 11:07"

RUN set -eux \
    ## Install PHP opcache
    && docker-php-ext-configure opcache --enable-opcache && docker-php-ext-install -j$(nproc) opcache \
    && echo "opcache.enable=0" >> "$PHP_INI_DIR/conf.d/docker-php-ext-opcache.ini" \
    ## Install gd
    && install_packages libjpeg-dev libpng-dev libwebp-dev libfreetype6-dev \
    && docker-php-ext-configure gd --prefix=/usr --with-gd --with-webp-dir --with-jpeg-dir --with-png-dir --with-zlib-dir --with-freetype-dir \
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
