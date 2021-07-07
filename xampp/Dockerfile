#Imagen Base
FROM ubuntu:20.04
#PUerto a exponer
EXPOSE 80
#Directorio de trabajo
WORKDIR /opt/lampp/htdocs
#Instalamos los paquetes requeridos
RUN apt-get update && apt-get install -y --no-recomends wget nano curl
#Bajamos la version de xampp 7.4
RUN wget https://www.apachefriends.org/xampp-files/7.4.20/xampp-linux-x64-7.4.20-0-installer.run && chmod +x xampp-linux-x64-7.4.20-0-installer.run &&  ./xampp-linux-x64-7.4.20-0-installer.run --mode unattended
#Levantamos el servidor apache de xampp unicamente
CMD ["/opt/lampp/bin/apachectl", "-D FOREGROUND"]