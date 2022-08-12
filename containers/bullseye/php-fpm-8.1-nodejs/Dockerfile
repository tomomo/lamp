FROM node:bullseye as node
FROM php:8.1-fpm-bullseye

RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

RUN apt-get update && \
  apt-get install -y \
    git git-lfs git-flow \
    unzip zip \
    libbz2-dev \
    zlib1g-dev \
    libpng-dev \
    libtidy-dev \
    libgmp-dev \
    libicu-dev \
    libc-client2007e-dev \
    libc-client-dev libkrb5-dev \
    libldap2-dev \
    libpq-dev \
    libxml2-dev \
    libpspell-dev \
    libxslt-dev \
    libzip-dev \
    libfreetype6-dev libjpeg62-turbo-dev libpng-dev \
    imagemagick libmagickwand-dev \
  && \
    apt-get autoremove && \
    apt-get autoclean
RUN pecl install redis imagick
RUN \
  docker-php-ext-configure gd --with-freetype --with-jpeg && \
  docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
  docker-php-ext-enable redis imagick && \
  docker-php-ext-install -j$(nproc) \
    bcmath \
    bz2 \
    calendar \
    dba \
    exif \
    gd \
    tidy \
    gettext \
    gmp \
    intl \
    imap \
    ldap \
    mysqli pdo_mysql \
    pgsql pdo_pgsql \
    soap \
    sockets \
    pcntl \
    pspell \
    opcache \
    sysvmsg \
    sysvsem \
    sysvshm \
    xsl \
    zip

COPY --from=composer /usr/bin/composer /usr/bin/composer

COPY --from=node /usr/local/bin /usr/local/bin
COPY --from=node /usr/local/lib /usr/local/lib
RUN rm -f /usr/local/bin/yarn /usr/local/bin/yarnpkg && corepack enable yarn

RUN cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini && \
#  sed -i -E 's/^(;| )*date\.timezone( )*=.*$/date.timezone = Asia\/Tokyo/g' /usr/local/etc/php/php.ini && \
  sed -i -E 's/^(;| )*ffi\.enable( )*=.*$/ffi.enable = true/g' /usr/local/etc/php/php.ini && \
  sed -i -E 's/^(;| )*upload_max_filesize( )*=.*$/upload_max_filesize = 20M/g' /usr/local/etc/php/php.ini && \
  sed -i -E 's/^(;| )*post_max_size( )*=.*$/post_max_size = 20M/g' /usr/local/etc/php/php.ini && \
# sed -i -E 's/^(;| )*memory_limit( )*=.*$/memory_limit = 128M/g' /usr/local/etc/php/php.ini && \
  sed -i -E 's/^(;| )*security.limit_extensions( )*=.*$/security.limit_extensions = .php .html/g' /usr/local/etc/php-fpm.d/www.conf

RUN { \
    echo 'export PS1="\[\e[0;36m\][\u@\h \W]\\$ \[\e[m\]"'; \
  } >> "$HOME/.bashrc"
