FROM php:5-fpm

RUN apt-get update && apt-get install --no-install-recommends -y \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libmcrypt-dev \
  libpng12-dev \
  mcrypt \
  libmcrypt-dev \
  libjpeg-dev \
  pkg-config libmagickwand-dev imagemagick \
  zlib1g-dev libicu-dev g++ \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd pdo pdo_mysql mbstring iconv mcrypt zip bcmath intl exif fileinfo\
  && docker-php-ext-enable opcache

RUN curl -L -o /tmp/imagick.tgz http://pecl.php.net/get/imagick-3.4.2.tgz \
  && tar xfz /tmp/imagick.tgz -C /tmp \
  && mkdir -p /usr/src/php/ext/ \
  && rm -r /tmp/imagick.tgz \
  && mv /tmp/imagick-3.4.2 /usr/src/php/ext/imagick \
  && docker-php-ext-install imagick

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*