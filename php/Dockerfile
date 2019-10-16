FROM php:7.2-fpm-alpine
#### PHP Common stuff + XDebug ####
RUN apk update \
&& apk upgrade \
&& apk add --no-cache bzip2-dev libpng libpng-dev gettext gettext-dev openldap-dev freetype-dev \
&& apk add --no-cache php7-pear php7-dev gcc musl-dev make build-base \
&& apk add --no-cache zlib-dev g++ icu icu-dev \
&& apk add --no-cache php-openssl \
&& apk add --no-cache php-mbstring \
&& docker-php-ext-install bcmath \
&& docker-php-ext-install bz2 \
&& docker-php-ext-install calendar \
&& docker-php-ext-install exif \
&& docker-php-ext-install gd \
&& docker-php-ext-install gettext \
&& docker-php-ext-install ldap \
&& docker-php-ext-install mysqli \
&& docker-php-ext-install pdo \
&& docker-php-ext-install sockets \
&& docker-php-ext-install opcache \
&& docker-php-ext-install zip \
&& docker-php-ext-install pdo_mysql \
&& docker-php-ext-install intl \
&& apk add --no-cache pcre-dev ${PHPIZE_DEPS} \
&& pecl install xdebug \
&& docker-php-ext-enable xdebug \
&& apk del pcre-dev ${PHPIZE_DEPS} \
&& apk add --no-cache php-mysqlnd \
&& apk add --no-cache composer \
&& apk update \
&& apk upgrade \
#### PHP Project-specific stuff, e.g. cache engines, NoSQL or different from MySQL databases, MQ brokers etc. ####
#### PHP-Memcached ####
&& apk add --no-cache libmemcached libmemcached-dev \
&& curl -L -o /tmp/memcached.tar.gz "https://github.com/php-memcached-dev/php-memcached/archive/php7.tar.gz" \
&& mkdir -p memcached \
&& tar -C memcached -zxvf /tmp/memcached.tar.gz --strip 1 \
&& ( \
    cd memcached \
    && phpize \
    && ./configure \
    && make -j$(nproc) \
    && make install \
) \
&& rm -r memcached \
&& rm /tmp/memcached.tar.gz \
&& docker-php-ext-enable memcached \
#### Finally clean cache ####
&& rm -rf /var/cache/apk/*
#### Dummy sendmail with logging ####
COPY ./copy/phpsendmail /usr/local/bin
CMD ["php-fpm"]