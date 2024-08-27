#
#--------------------------------------------------------------------------
# php 7.4 cli-imap
#--------------------------------------------------------------------------
#

ARG PHP_VERSION=7.4.33
FROM chinayin/php:${PHP_VERSION}-cli-slim
LABEL maintainer="chinayin <whereismoney@qq.com>"

RUN set -eux \
  && pecl channel-update pecl.php.net \
  && docker-php-source extract \
  ## install all required dependencies
  && install_packages \
    # gd
      libjpeg-dev libpng-dev libwebp-dev libfreetype6-dev  \
    # swoole \
      libcurl4-openssl-dev \
    # imap
      libc-client-dev libkrb5-dev \
  ## install extensions \
  ## ext-gd
  && docker-php-ext-configure gd --prefix=/usr --enable-gd --with-webp --with-jpeg --with-freetype \
  && docker-php-ext-install -j$(nproc) gd \
  ## ext-swoole
  && ( \
    pecl bundle -d /usr/src/php/ext swoole-4.8.13 \
    && docker-php-ext-configure swoole --enable-swoole-json --enable-http2 --enable-swoole-curl \
    && docker-php-ext-install -j$(nproc) swoole \
  ## ext-imap
  && docker-php-ext-configure imap --with-imap --with-imap-ssl --with-kerberos \
  && docker-php-ext-install -j$(nproc) imap \
  ) \
  ## install supervisord \
  && ( \
    install_packages supervisor \
  ) \
  ## Clean up
  && ( \
    docker-php-source delete \
    && pecl clear-cache \
    && rm -rf /tmp/* /var/tmp/* \
    && rm -f /var/log/lastlog /var/log/faillog \
  ) \
  ## Check PHP version
  && php -v

WORKDIR /var/www
