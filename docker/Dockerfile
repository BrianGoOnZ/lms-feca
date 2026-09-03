FROM php:8.3-apache

# Dependencias del sistema para compilar las extensiones de PHP
RUN apt-get update && apt-get install -y --no-install-recommends \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libzip-dev \
    libicu-dev \
    libxml2-dev \
    libcurl4-openssl-dev \
    libonig-dev \
    libsodium-dev \
    libwebp-dev \
    unzip \
    git \
    cron \
    ghostscript \
    graphviz \
    && rm -rf /var/lib/apt/lists/*

# Extensiones PHP requeridas por Moodle
RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp \
    && docker-php-ext-install -j$(nproc) \
    gd \
    zip \
    intl \
    mysqli \
    opcache \
    exif \
    soap \
    sodium

# Apache: mod_rewrite es obligatorio para las URLs de Moodle
RUN a2enmod rewrite headers expires

# Moodle 5.1+ sirve desde la subcarpeta public/
ENV APACHE_DOCUMENT_ROOT=/var/www/html/public
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf \
    && sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

WORKDIR /var/www/html
