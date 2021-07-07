#Desde la imagen de php 7.4 nos basamos para hacer una pequeña modificacion
FROM php:7.4-apache
#Exponemos el puerto 80 para gestionar las conexiones entrantes
EXPOSE 80
#El directorio de trabajo se mantiene tal cual como esta
WORKDIR /var/www/html
#Instalamos las extensiones requeridas para ejecutar el framework
RUN docker-php-ext-install -j$(nproc) mysqli
#Modificamos el document Root 000-default con la carpeta public para que el framework inicie
RUN sed -i 's!/var/www/html!/var/www/html/public!g' /etc/apache2/apache2.conf \
  /etc/apache2/sites-available/000-default.conf 
#Iniciamos el servidor apache
CMD ["apache2-foreground"]