FROM php:8.3-fpm-bookworm

# Arguments for UID/GID matching host system
ARG UID=1000
ARG GID=1000

# Install essential system utilities
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    curl \
    zip \
    unzip \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# Install official PHP extension installer helper
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

# Install PHP extensions required by Krayin CRM
RUN install-php-extensions \
    calendar \
    pdo_mysql \
    mbstring \
    exif \
    pcntl \
    bcmath \
    gd \
    intl \
    zip \
    imap \
    opcache

# Set Composer cache directory and environment
ENV COMPOSER_HOME=/tmp/composer

# Install Node.js 20.x (LTS) & NPM for asset building
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y nodejs \
    && rm -rf /var/lib/apt/lists/*

# Get Composer 2
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Synchronize www-data UID & GID with host user and ensure home directory ownership
RUN groupmod -o -g ${GID} www-data && \
    usermod -o -u ${UID} -g www-data www-data && \
    mkdir -p /var/www/.npm /var/www/.composer && \
    chown -R www-data:www-data /var/www

# Set working directory
WORKDIR /var/www/html

USER www-data

EXPOSE 9000

CMD ["php-fpm"]
