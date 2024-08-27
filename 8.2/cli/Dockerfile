#
#--------------------------------------------------------------------------
# php 8.2 cli
#--------------------------------------------------------------------------
#

ARG PHP_VERSION=8.2.16
FROM chinayin/php:${PHP_VERSION}-cli-slim
LABEL maintainer="chinayin <whereismoney@qq.com>"

RUN set -eux \
  ## install all required dependencies
  && install_packages \
    # swoole
    libcurl4-openssl-dev \
  ## temp directory
  && temp_dir=$(mktemp -d) \
  ## install extensions
  && pecl channel-update pecl.php.net \
  && docker-php-source extract \
  ## ext-swoole
  && ( \
    pecl bundle -d /usr/src/php/ext swoole-5.1.4 \
    && docker-php-ext-configure swoole --enable-openssl --enable-swoole-curl \
    && docker-php-ext-install -j$(nproc) swoole \
  ) \
  ## install supervisord
  && ( \
    install_packages supervisor \
  ) \
  ## Clean up
  && ( \
    docker-php-source delete \
    && pecl clear-cache \
    && rm -rf /tmp/* /var/tmp/* \
    && rm -f /var/log/lastlog /var/log/faillog \
    && rm -rf "${temp_dir}" \
  ) \
  ## Check PHP version
  && php -v && php -m

WORKDIR /var/www
