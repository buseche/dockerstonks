FROM php:7.4-apache
EXPOSE 80
WORKDIR /var/www/html

RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev libicu-dev libpq-dev zip git 
RUN apt-get install -y libc-client-dev libkrb5-dev && rm -r /var/lib/apt/lists/*
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl && docker-php-ext-install imap
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-configure intl 
RUN docker-php-ext-install -j$(nproc) gd mysqli imap zip intl pgsql pdo pdo_mysql pdo_pgsql

RUN cp "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

RUN service apache2 restart 