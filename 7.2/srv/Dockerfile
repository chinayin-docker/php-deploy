#
#--------------------------------------------------------------------------
# php 7.2 srv
#--------------------------------------------------------------------------
#

FROM chinayin/php:7.2-fpm-slim
LABEL maintainer="chinayin <whereismoney@qq.com>"

ENV CYD_APP_NAME="7.2-fpm-srv" \
    CYD_IMAGE_VERSION="v2021-03-22 19:31"

RUN set -eux \
    && pecl channel-update pecl.php.net && mkdir -p /tmp/pear/cache \
    ## Install pdftk (https://www.pdflabs.com/docs/install-pdftk-on-redhat-or-centos)
    ## fix error processing package openjdk-11-jre-headless:amd64
    && mkdir -p /usr/share/man/man1 \
    && install_packages pdftk \
    ## Clean up
    && pecl clear-cache \
    && rm -rf /tmp/* /var/tmp/* \
    && rm -f /var/log/lastlog /var/log/faillog \
    ## Check PHP version
    && php -v
