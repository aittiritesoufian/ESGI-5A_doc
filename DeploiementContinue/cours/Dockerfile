FROM php:7.2-apache

RUN docker-php-ext-install pdo pdo_mysql \
 && a2enmod rewrite \
 && sed -i 's!/var/www/html!/var/www/html/deployment/current!g' /etc/apache2/sites-available/*.conf

ADD . /var/www/html

WORKDIR /var/www/html