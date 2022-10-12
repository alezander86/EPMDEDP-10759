FROM php:8.0-apache
RUN sed -i "s/\#ServerName www.example.com/\ServerName localhost/g" /etc/apache2/sites-available/000-default.conf && rm /etc/apache2/sites-available/default-ssl.conf
COPY ./php-mysql-crud/ /var/www/html/
WORKDIR /var/www/html
