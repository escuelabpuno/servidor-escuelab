# Guía de instalación no automatizada

## Requisitos

* Un Servidor decente
* Acceso a Internet veloz (no necesariamente donde vaya a estar el servidor)
* Conocimientos de GNU/Linux

### Servidor Recomendado

* Intel Core i7
* \> 8 GB RAM
* \> 2 TB HDD RAID
* 128 GB SSD
* UPS

### Mínimo Requerido

* Intel Core i3
* 4 GB RAM
* 1 GB HDD

## Instalación

### Instalación estandar de Ubuntu Server

### Instalar Servicios

~~~.bash
sudo apt-get update
sudo apt-get install tasksel
sudo tasksel install standard openssh-server server lamp-server
sudo apt-get install libapache2-mpm-itk
~~~

### Instalar Paquetes extra

#### Emby

~~~.bash
echo "deb http://download.opensuse.org/repositories/home:/emby/xUbuntu_16.04/ /" | sudo tee /etc/apt/sources.list.d/emby.list
sudo apt-key add emby.key
sudo apt-get update
sudo apt-get install emby-server
~~~

#### Webmin

~~~.bash
echo "deb http://download.webmin.com/download/repository sarge contrib" | sudo tee /etc/apt/sources.list.d/webmin.list
sudo apt-key add webmin.key
sudo apt-get update
sudo apt-get install webmin
~~~

#### Certbot

~~~.bash
echo "deb http://ppa.launchpad.net/certbot/certbot/ubuntu xenial main" | sudo tee /etc/apt/sources.list.d/certbot.list
sudo apt-key add certbot.key
sudo apt-get update
sudo apt-get install python-certbot-apache
~~~

#### KaLite

~~~.bash
echo "deb http://ppa.launchpad.net/learningequality/ka-lite/ubuntu xenial main" | sudo tee /etc/apt/sources.list.d/kalite.list
sudo apt-key add kalite.key
sudo apt-get update
sudo apt-get install ka-lite
~~~

#### Webupd8

~~~.bash
echo "deb http://ppa.launchpad.net/nilarimogard/webupd8/ubuntu xenial main" | sudo tee /etc/apt/sources.list.d/webupd8.list
sudo apt-key add webupd8.key
sudo apt-get update
sudo apt-get install youtube-dl
~~~
