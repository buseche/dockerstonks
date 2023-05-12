FROM php:5.6-apache
EXPOSE 80
WORKDIR /var/www/html
COPY php.ini $PHP_INI_DIR/php.ini
RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev libicu-dev libpq-dev zip git \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-configure intl \
	&& docker-php-ext-install -j$(nproc) gd mysqli zip intl pgsql pdo pdo_mysql pdo_pgsql
RUN service apache2 restart