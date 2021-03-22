#
#--------------------------------------------------------------------------
# php 7.2 sso
#--------------------------------------------------------------------------
#

FROM chinayin/php:7.2-fpm-slim
LABEL maintainer="chinayin <whereismoney@qq.com>"

ENV CYD_APP_NAME="7.2-fpm-sso" \
    CYD_IMAGE_VERSION="v2021-03-22 19:31"

RUN set -eux \
    ## Install gd
    && install_packages libjpeg-dev libpng-dev libwebp-dev libfreetype6-dev \
    && docker-php-ext-configure gd --prefix=/usr --with-gd --with-webp-dir --with-jpeg-dir --with-png-dir --with-zlib-dir --with-freetype-dir \
    && docker-php-ext-install -j$(nproc) gd \
    ## Clean up
    && rm -rf /tmp/* /var/tmp/* \
    && rm -f /var/log/lastlog /var/log/faillog \
    ## Check PHP version
    && php -v
