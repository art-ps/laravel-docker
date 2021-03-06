FROM php:7.3-alpine

# Install dev dependencies
RUN apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS \
    curl-dev \
    imagemagick-dev \
    libtool \
    libxml2-dev
#    postgresql-dev \
#    sqlite-dev

# Install production dependencies
RUN apk add --no-cache \
    bash \
    curl \
    g++ \
    gcc \
    git \
    imagemagick \
    libc-dev \
    libpng-dev \
    make \
    mysql-client \
    nodejs \
    nodejs-npm \
    #    yarn \
    openssh-client \
    #    postgresql-libs \
    rsync \
    zlib-dev \
    libzip-dev \
    libmcrypt-dev

# Install PECL and PEAR extensions
RUN pecl install \
    imagick \
    mcrypt-1.0.2 \
    exif

# Install and enable php extensions
RUN docker-php-ext-enable \
    imagick \
    mcrypt

RUN docker-php-ext-configure zip --with-libzip
RUN docker-php-ext-install \
    curl \
    iconv \
    mbstring \
    pdo \
    pdo_mysql \
    #    pdo_pgsql \
    #    pdo_sqlite \
    pcntl \
    tokenizer \
    xml \
    gd \
    zip \
    bcmath \
    sockets \
    opcache \
    exif

# Install composer
RUN curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer
ENV COMPOSER_ALLOW_SUPERUSER=1
ENV PATH="./vendor/bin:$PATH"

# Install PHP_CodeSniffer
RUN composer global require "squizlabs/php_codesniffer=*"

# install hirak/prestissimo
RUN composer global require hirak/prestissimo

# Cleanup dev dependencies
RUN apk del -f .build-deps

# Setup working directory
WORKDIR /var/www
