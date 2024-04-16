#
#--------------------------------------------------------------------------
# php 8.2 cli-imagick
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
    # imagick
    libjpeg-dev libpng-dev libgif-dev libwebp-dev libtiff-dev libfreetype6-dev librsvg2-dev libheif-dev ghostscript libltdl-dev \
  ## temp directory
  && temp_dir=$(mktemp -d) \
  ## install extensions \
  && pecl channel-update pecl.php.net \
  && docker-php-source extract \
  ## ext-swoole
  && ( \
    pecl bundle -d /usr/src/php/ext swoole-5.1.2 \
    && docker-php-ext-configure swoole --enable-openssl --enable-swoole-curl \
    && docker-php-ext-install -j$(nproc) swoole \
  ) \
  ## install supervisord
  && ( \
    install_packages supervisor \
  ) \
  ## install ImageMagick-7
  && ( \
    curl -fsSL --compressed -o "${temp_dir}/ImageMagick.tar.gz" "https://github.com/ImageMagick/ImageMagick/archive/refs/tags/7.1.1-30.tar.gz" \
    && mkdir -p "${temp_dir}/ImageMagick" \
    && tar -xzf "${temp_dir}/ImageMagick.tar.gz" -C "${temp_dir}/ImageMagick" --strip-components=1  \
    && cd "${temp_dir}/ImageMagick" \
    && ./configure --with-modules \
    && make -j$(nproc) && make install  \
    && ldconfig /usr/local/lib \
    && convert -version \
  ) \
  # ext-imagick
  && pecl install imagick \
  && docker-php-ext-enable imagick \
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
