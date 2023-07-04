# Creación y compilación de Docker Image de Nagios Core

Cree un directorio donde se copiaran los archivos necesarios

`mkdir /opt/nagios-core-docker`

`cd /opt/nagios-core-docker/`

`wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.9.tar.gz`

`tar xzf nagios-4.4.9.tar.gz`

`wget https://github.com/nagios-plugins/nagios-plugins/releases/download/release-2.4.2/nagios-plugins-2.4.2.tar.gz`

`tar xzf nagios-plugins-2.4.2.tar.gz`

`wget https://github.com/NagiosEnterprises/nrpe/releases/download/nrpe-4.1.0/nrpe-4.1.0.tar.gz`

`tar xzf nrpe-4.1.0.tar.gz`


El archivo Dockerfile permitirá compilar e instalar Nagios y sus complementos en una imagen de Ubuntu 22.04.

También copia las credenciales de autenticación básicas de Nagios definidas en las variables de entorno (archivo .env)
Modifique dicho archivo segun las credenciales de authenticación que necesite utilizar.

> NAGIOSADMIN_USER=nagiosadmin`
> NAGIOSADMIN_PASSWORD=password`

También se puede anular las credenciales de Nagios usando las variables de entorno NAGIOSADMIN_USER_OVERRIDEy NAGIOSADMIN_PASSWORD_OVERRIDE durante la ejecución del comando "docker run".

Para construir la imagen:

`docker build -t nagios-core:4.4.9 .`

Cree y ejecute el contenedor de Nagios-Core utilizando el siguiente comando:

`docker run --name nagios-core-4.4.9 -dp 80:80 nagios-core:4.4.9`

Para anular las credenciales definidas en el archivo .env, use el comando;

> docker run \
> -e NAGIOSADMIN_USER_OVERRIDE=monadmin \
> -e NAGIOSADMIN_PASSWORD_OVERRIDE=password \
> --name nagios-core-4.4.9 -dp 80:80 nagios-core:4.4.9

Acceso a la interfaz web principal de Nagios
Para verificar si todo está bien, ahora puede acceder a la interfaz web de Nagios Core;

`http://docker-host-IP-or-hostname/nagios/`

