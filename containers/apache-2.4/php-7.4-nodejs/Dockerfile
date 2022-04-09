FROM node:16 as node
FROM php:7.4-apache

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
  libc-client-dev libkrb5-dev \
  libpspell-dev \
  && pecl install redis-5.3.7 xdebug-3.1.3 imagick-3.7.0 swoole-4.8.7 \
  && apt-get autoremove \
  && apt-get autoclean \
  && rm -rf /var/lib/apt/lists/*

RUN NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
  && docker-php-ext-enable redis xdebug imagick swoole \
  && docker-php-ext-install -j${NPROC} \
  bcmath \
  bz2 \
  ctype \
  curl \
  exif \
  gd \
  intl \
  mbstring \
  mysqli pdo_mysql \
  pgsql pdo_pgsql \
  pspell \
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

RUN echo 'xdebug.mode=coverage' >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

COPY --from=composer /usr/bin/composer /usr/bin/composer
COPY --from=node /usr/local/bin/node /usr/local/bin/
COPY --from=node /usr/local/lib/node_modules/ /usr/local/lib/node_modules/
COPY --from=node /opt/yarn* /opt/yarn
RUN \
  ln -s /usr/local/bin/node /usr/local/bin/nodejs && \
  ln -s /usr/local/lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm && \
  ln -s /usr/local/lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npx && \
  ln -s /opt/yarn/bin/yarn /usr/local/bin/yarn && \
  ln -s /opt/yarn/bin/yarnpkg /usr/local/bin/yarnpkg

RUN \
  { \
    echo 'if [ $PS1 ]; then'; \
    echo '    PS1="\[\e[1;32m\][\u@\h \W]\\$ \[\e[m\]"'; \
    echo 'fi'; \
  } >> /var/www/.bashrc \
 && \
  { \
    echo 'if [ -f ~/.bashrc ]; then'; \
    echo '    . ~/.bashrc'; \
    echo 'fi'; \
  } >> /var/www/.bash_profile

ARG UID=33
RUN usermod -u ${UID} www-data \
 && chsh -s /bin/bash www-data

# MEMO: used context for docker-compose.yml
COPY ./containers/apache-2.4/sites-enabled /etc/apache2/sites-enabled
