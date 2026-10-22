#
#--------------------------------------------------------------------------
# php 7.4 pay
#--------------------------------------------------------------------------
#

ARG PHP_VERSION=7.4.34
FROM chinayin/php:${PHP_VERSION}-fpm-slim
LABEL maintainer="chinayin <whereismoney@qq.com>"

RUN set -eux \
  ## Install gd
  && install_packages cmake \
  ## Install gmssl && gmssl-php \
  && ( \
    mkdir -p /tmp/gmssl && cd /tmp/gmssl \
    && curl -fsSL -o gmssl.tar.gz "https://github.com/guanzhi/GmSSL/archive/refs/tags/v3.1.0.tar.gz" \
    && tar -xzvf gmssl.tar.gz --strip-components=1 \
    && mkdir build \ && cd build \
    && cmake .. && make && make test && make install \
    && cp /usr/local/lib/libgmssl.so.3 /usr/lib/ \
    && ldconfig \
    && cd /tmp/gmssl \
    && curl -fsSL -o gmssl-php.tar.gz "https://github.com/chinayin/GmSSL-PHP/archive/refs/tags/v1.0.0.tar.gz" \
    && tar -xzvf gmssl-php.tar.gz --strip-components=1 \
    && phpize \
    && ./configure \
    && make && make install \
    && docker-php-ext-enable gmssl \
  ) \
  ## Clean up \
  && rm -rf /tmp/gmssl \
  && rm -rf /tmp/* /var/tmp/* \
  && rm -f /var/log/lastlog /var/log/faillog \
  ## Check PHP version
  && php -v
