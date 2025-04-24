ARG PHP_VERSION=8.3

FROM php:${PHP_VERSION}-fpm-alpine

# Install system dependencies
RUN apk add --no-cache \
    git \
    curl \
    libpng-dev \
    libxml2-dev \
    zip \
    unzip \
    oniguruma-dev \
    libzip-dev

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www/html

# Copy startup script
COPY startup.sh /usr/local/bin/startup.sh
RUN chmod +x /usr/local/bin/startup.sh

# Create Laravel directory if it doesn't exist
RUN mkdir -p /var/www/html

# Set permissions
RUN chown -R www-data:www-data /var/www/html

# Switch to non-root user
USER www-data

# Expose port 9000 (PHP-FPM)
EXPOSE 9000

# Start PHP-FPM and run the startup script
CMD ["/usr/local/bin/startup.sh"]