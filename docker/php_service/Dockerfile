FROM php:7.4-fpm

# Install dependencies
RUN apt-get update \
    && apt-get install -y zlib1g-dev \
    && apt-get install -y libicu-dev \
    && apt-get install -y g++ \
    # postgres
    && apt-get install -y libpq-dev \
    # xdebug
    && pecl install xdebug

# Install Docker's PHP extensions
    # xdebug
RUN docker-php-ext-enable xdebug \
    # php internationalization functions
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    # opcache
    && docker-php-ext-install opcache \
    # pdo
    && docker-php-ext-install pdo \
    # postgres pdo
    && docker-php-ext-install pdo_pgsql

# Install tools
RUN apt-get install -y wget \
    && apt-get install -y git \
    && apt-get install -y vim

# Remove and clean unused packs
RUN apt-get autoremove -y \
    && apt-get autoclean -y

#  Copying php.ini and xdebug.ini
COPY php.ini-development-modified /usr/local/etc/php/php.ini
COPY xdebug.ini /usr/local/etc/php/xdebug.ini

# Setting your git user
RUN git config --global user.email "user@domain.com"
RUN git config --global user.name "User Name"

# Composer installation
COPY composer-install.sh /tmp
RUN chmod +x /tmp/composer-install.sh \
    && /tmp/./composer-install.sh

# Symfony installation
RUN wget https://get.symfony.com/cli/installer -O - | bash \
    && mv /root/.symfony/bin/symfony /usr/local/bin/symfony

# Set working directory
WORKDIR /var/www/app