#FROM composer:1.9.3 AS composer
FROM php:7.2.5-fpm-alpine

ENV PHP_OPCACHE_ENABLE=1 \
 PHP_OPCACHE_ENABLE_CLI=0 \
 PHP_OPCACHE_VALIDATE_TIMESTAMPS=1 \
 PHP_OPCACHE_REVALIDATE_FREQ=1 \
 PHP_OPCACHE_MAX_ACCELERATED_FILES="10000" \
 PHP_OPCACHE_MAX_WASTED_PERCENTAGE="10"

RUN apk update && apk upgrade && \
    apk add --no-cache bash git sudo openssh libxml2-dev autoconf gcc g++ \ 
        make freetype-dev libjpeg-turbo-dev libpng-dev

RUN apk add --no-cache --update \
  bzip2-dev \
  libpng-dev \
  gmp-dev \
  imap-dev \
  icu-dev \
  openldap-dev \
  freetds-dev \
  postgresql-dev \
  aspell-dev \
  net-snmp-dev \
  libxml2-dev \
  libxslt-dev 
  

RUN docker-php-source extract
# PHP: Install php extensions
RUN pecl channel-update pecl.php.net
#RUN pecl install pcov ssh2
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install \
  bcmath \
  bz2 \
  calendar \
  dba \  
  exif \
  gd \
  gmp \
  imap \
  intl 

  RUN docker-php-ext-install \
  ldap \
  mysqli \
  opcache \
  pcntl \
  pdo_dblib \
  pdo_mysql \
  pdo_pgsql \
  pgsql \
  pspell \
  shmop \
  snmp \
  soap \
  sockets \
  sysvmsg \
  sysvsem \
  sysvshm \  
  xsl \  
  zip

RUN docker-php-ext-install mbstring xml pdo 
RUN docker-php-ext-enable mbstring xml pdo bcmath \
  bz2 \
  calendar \
  dba \  
  exif \
  gd \
  gmp \
  imap \
  intl \
  ldap \
  mysqli \
  opcache \
  pcntl \
  pdo_dblib \
  pdo_mysql \
  pdo_pgsql \
  pgsql \
  pspell \
  shmop \
  snmp \
  soap \
  sockets \
  sysvmsg \
  sysvsem \
  sysvshm \  
  xsl \  
  zip

#RUN curl -sS https://getcomposer.org/installer​ | php -- --install-dir=/usr/local/bin --filename=composer

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN chmod 2775 /var/www/html
#RUN chmod o+w /var/www/html/storage/ -R
RUN rm -rf /var/www/html/public/storage

WORKDIR /var/www/html/

#CMD ["php", "artisan", "key:generate"]
#CMD ["php", "artisan storage:link"]
#CMD ["php", "artisan config:cache"]
#CMD ["php", "artisan route:cache"]
#CMD ["php-fpm", "artisan optimize"]

