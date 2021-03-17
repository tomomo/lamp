FROM php:8.0-apache

LABEL maintainer "tomomo <eclairpark@gmail.com>"

RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
 && apt-get update \
 && apt-get install -y \
 vim \
 msmtp msmtp-mta \
 libxml2-dev \
 libcurl3-dev libonig-dev \
 sqlite3 libsqlite3-dev \
 libpq-dev \
 libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
 imagemagick libmagickwand-dev \
 libzip-dev \
 libc-client-dev libkrb5-dev libpspell-dev \
 # NOTE: imagick-3.4.4 が使えない
 && pecl install redis-5.3.3 \
 && apt clean \
 && rm -rf /var/lib/apt/lists/*

# NOTE: https://github.com/Imagick/imagick/issues/331
RUN mkdir -p /usr/src/php/ext/imagick \
 && curl -fsSL https://github.com/Imagick/imagick/archive/06116aa24b76edaf6b1693198f79e6c295eda8a9.tar.gz | tar xvz -C "/usr/src/php/ext/imagick" --strip 1

RUN NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
 && docker-php-ext-configure gd --with-freetype --with-jpeg \
 && docker-php-ext-enable redis \
 && docker-php-ext-install -j${NPROC} \
  bcmath \
  bz2 \
  ctype \
  curl \
  exif \
  gd \
  imagick \
  intl \
  mbstring \
  mysqli pdo_mysql \
  pgsql pdo_pgsql \
  pspell \
  tokenizer \
  xml \
  zip

RUN a2enmod authn_socache cache deflate expires headers http2 proxy proxy_fcgi rewrite socache_shmcb ssl \
 && a2dissite 000-default

RUN mkdir -p /etc/apache2/certs \
 && openssl req \
  -x509 \
  -newkey rsa:2048 \
  -keyout /etc/apache2/certs/localhost.key \
  -out    /etc/apache2/certs/localhost.crt \
  -days 365 \
  -nodes \
  -subj "/C=JP/ST=Tokyo/L=Minato-ku/O=None/OU=Org/CN=localhost" \
 && chmod 644 -R /etc/apache2/certs

# COPY ./vhosts /etc/apache2/sites-enabled
# MEMO: used context for docker-compose.yml
COPY ./containers/apache24/sites-enabled /etc/apache2/sites-enabled

ARG UID=33

RUN usermod -u ${UID} www-data
