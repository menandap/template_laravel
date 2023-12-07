# Use the php:8.2-apache image as base
FROM php:8.2-apache

# Set working directory
WORKDIR /var/www/html

# Copy Laravel files into the container
COPY framework_files/app_files/ ./

# Install dependencies and enable necessary extensions if needed
# For Laravel, you may need to install additional PHP extensions or packages.
# For example, if you're using MySQL, you might need to install the pdo_mysql extension.
# RUN docker-php-ext-install pdo_mysql

# Set permissions if needed
RUN chown -R www-data:www-data storage bootstrap

# Install composer if not already installed
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install PHP dependencies using Composer
RUN composer install --no-scripts --no-autoloader

# Expose port 80 (default for Apache)
EXPOSE 80

# Start Apache server
CMD ["apache2-foreground"]
