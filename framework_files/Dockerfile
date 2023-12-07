# Use the base image with PHP and other necessary configurations
FROM docker.io/library/php:8.1-fpm

# Set the working directory in the container
WORKDIR /var/www/html

# Copy the application files into the container
COPY app_files /var/www/html

# Install necessary dependencies
RUN apt-get update && apt-get install -y \
    libzip-dev \
    zip \
    curl \
    git \
    unzip

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Copy .env.example and rename it to .env
RUN cp .env.example .env

# Run Composer commands
RUN composer install --no-scripts --no-autoloader
RUN composer dump-autoload

# Clear cache and configuration
RUN php artisan cache:clear
RUN php artisan config:clear

# Generate the application key
RUN php artisan key:generate

# Expose port 8080
EXPOSE 8080

# Start the Laravel application on port 8080
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8080"]