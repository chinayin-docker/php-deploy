#
#--------------------------------------------------------------------------
# php 7.4 crm
#--------------------------------------------------------------------------
#

FROM chinayin/php:7.4-fpm-slim
LABEL maintainer="chinayin <whereismoney@qq.com>"

ENV CYD_APP_NAME="7.4-fpm-crm" \
    CYD_IMAGE_VERSION="v2021-06-16 14:13"

RUN set -eux \
    ## Install PHP opcache
    && docker-php-ext-configure opcache --enable-opcache && docker-php-ext-install -j$(nproc) opcache \
    && echo "opcache.enable=0" >> "$PHP_INI_DIR/conf.d/docker-php-ext-opcache.ini" \
    ## Install gd
    && install_packages libjpeg-dev libpng-dev libwebp-dev libfreetype6-dev \
    && docker-php-ext-configure gd --prefix=/usr --enable-gd --with-webp --with-jpeg --with-freetype \
    && docker-php-ext-install -j$(nproc) gd \
    ## Clean up
    && rm -rf /tmp/* /var/tmp/* \
    && rm -f /var/log/lastlog /var/log/faillog \
    ## Check PHP version
    && php -v
