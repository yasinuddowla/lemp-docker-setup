# Use the PHP image
FROM php:8.3-fpm
# Install required packages for building extensions
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    curl \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install mysqli pdo pdo_mysql \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
    
# Copy the application
COPY . /var/www/html

# Set ownership to www-data for the web server
RUN chown -R www-data:www-data /var/www/html

# Set correct permissions
RUN chmod -R 755 /var/www/html

# Set working directory
WORKDIR /var/www/html

# Expose port 9000 for PHP-FPM
EXPOSE 9000
