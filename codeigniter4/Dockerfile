FROM php:8-apache
EXPOSE 80
WORKDIR /var/www/html

RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev libicu-dev libpq-dev zip git \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-configure intl \
	&& docker-php-ext-install -j$(nproc) gd intl pgsql

RUN sed -i 's!/var/www/html!/var/www/html/public!g' /etc/apache2/apache2.conf /etc/apache2/sites-available/000-default.conf

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

RUN php composer-setup.php

RUN php -r "unlink('composer-setup.php');"

RUN mv composer.phar /usr/bin/composer

RUN a2enmod rewrite

RUN service apache2 restart

CMD ["apache2-foreground"]


