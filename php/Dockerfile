FROM php:8.1-fpm

# Copy ./composer.lock and composer.json
# COPY composer.lock composer.json /var/www/

# Set working directory
WORKDIR /var/www

# Install dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libonig-dev \
    libgd-dev \
    libmagickwand-dev \
    libmagic-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libssl-dev \
    zlib1g-dev \
    libpq-dev \
    libxml2-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    nodejs \
    npm \
    wget \
    libzip-dev 

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Custom 
RUN pecl install imagick
RUN docker-php-ext-enable imagick

# Install extensions
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl bcmath
RUN docker-php-ext-configure gd
RUN docker-php-ext-install gd

# RUN echo "extension=bcmath.so" > /usr/local/etc/php/conf.d/bcmath.ini

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Add user for laravel application
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# Copy existing application directory contents
COPY . /var/www

# Copy existing application directory permissions
COPY --chown=www:www . /var/www

# Change current user to www
USER www

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]