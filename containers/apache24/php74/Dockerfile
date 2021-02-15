FROM php:7.4-apache

LABEL maintainer "tomomo <eclairpark@gmail.com>"

ENV DEBIAN_FRONTEND=noninteractive

RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
 apt-get update -y && apt-get upgrade -y && \
 apt-get install -y \
 vim \
 msmtp msmtp-mta \
 libxml2-dev \
 libcurl3-dev libonig-dev \
 sqlite3 libsqlite3-dev \
 libpq-dev \
 libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
 imagemagick libmagickwand-dev \
  && \
 apt-get clean \
  && \
 pecl install imagick-3.4.4 redis-5.3.3

RUN NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
 docker-php-ext-configure gd --with-freetype --with-jpeg \
  && \
 docker-php-ext-enable imagick redis \
  && \
 docker-php-ext-install -j${NPROC} \
  bcmath \
  ctype \
  curl \
  exif \
  json \
  xml \
  gd \
  intl \
  mbstring \
  tokenizer \
  mysqli pdo_mysql \
  pgsql pdo_pgsql

RUN a2enmod authn_socache cache deflate expires headers http2 proxy proxy_fcgi rewrite socache_shmcb ssl && \
 a2dissite 000-default

RUN mkdir -p /etc/apache2/certs && \
 openssl req \
  -x509 \
  -newkey rsa:2048 \
  -keyout /etc/apache2/certs/localhost.key \
  -out    /etc/apache2/certs/localhost.crt \
  -days 365 \
  -nodes \
  -subj "/C=JP/ST=Tokyo/L=Minato-ku/O=None/OU=Org/CN=localhost" && \
 chmod 644 -R /etc/apache2/certs

# COPY ./vhosts /etc/apache2/sites-enabled
# MEMO: used context for docker-compose.yml
COPY ./containers/apache24/sites-enabled /etc/apache2/sites-enabled

RUN touch /etc/msmtprc && \
 chmod 777 /etc/msmtprc

WORKDIR /var/www/html
