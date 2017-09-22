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

~~~.bash
sudo apt-get install standard^ openssh-server^ server^
echo "deb http://archive.zentyal.org/zentyal 5.0 main" | sudo tee /etc/apt/sources.list.d/zentyal.list
sudo apt-key add zentyal.key
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get install zentyal language-pack-zentyal-es
~~~

### Instalar Servicios

~~~.bash
sudo apt-get update
sudo apt-get install lamp-server^
sudo apt-get install libapache2-mpm-itk
sudo apt-get install language-pack-es thunderbird-locale-es thunderbird-locale-es-ar libreoffice-help-en-gb wspanish libreoffice-help-es thunderbird-locale-en-gb thunderbird-locale-en-us mythes-es mythes-en-au thunderbird-locale-en thunderbird-locale-es-es wbritish hyphen-en-us hyphen-en-gb hunspell-en-gb libreoffice-l10n-es hunspell-en-za hunspell-es hunspell-en-au libreoffice-help-en-us hunspell-en-ca firefox-locale-es mythes-en-us libreoffice-l10n-en-gb openoffice.org-hyphenation hyphen-es libreoffice-l10n-en-za
sudo apt-get install graphviz aspell-es php-pspell php-curl php-gd php-intl  php-mysql php-xml php-xmlrpc php-ldap php-zip php-cli php-json  php-opcache php-readline php-mbstring php-mcrypt php-imagick php-soap
~~~

### Instalar Paquetes extra

~~~.bash
echo "deb http://download.opensuse.org/repositories/home:/emby/xUbuntu_16.04/ /" | sudo tee /etc/apt/sources.list.d/emby.list
sudo apt-key add emby.key

echo "deb http://ppa.launchpad.net/certbot/certbot/ubuntu xenial main" | sudo tee /etc/apt/sources.list.d/certbot.list
sudo apt-key add certbot.key

echo "deb http://ppa.launchpad.net/learningequality/ka-lite/ubuntu xenial main" | sudo tee /etc/apt/sources.list.d/kalite.list
sudo apt-key add kalite.key

echo "deb http://ppa.launchpad.net/nilarimogard/webupd8/ubuntu xenial main" | sudo tee /etc/apt/sources.list.d/webupd8.list
sudo apt-key add webupd8.key

sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
sudo apt-get install emby-server python-certbot-apache ka-lite youtube-dl

sudo systemctl stop ka-lite.service
sudo usermod -d /home/kalite -m kalite
#sudo mv /var/kalite /home/
sudo systemctl start ka-lite.service

sudo mkdir ../emby
sudo chown emby:emby ../emby

sudo adduser --system --home /home/campus --ingroup www-data campus
sudo adduser --system --home /home/sitios --ingroup www-data sitios
sudo adduser --system --home /home/nube --ingroup www-data nube
sudo adduser --system --home /home/kiwix --ingroup nogroup kiwix

~~~

# Apendice

## Anotaciones
~~~.bash
cd /tmp
curl -L https://download.kiwix.org/library/library_zim.xml -o library_zim.xml
for i in 19 20 21 22 23 24 25 ; do grep _es_ library_zim.xml | cut -d \" -f $i | grep http ; done | sed 's/.meta4//' | sort -r | grep -v -e venezuela -e ecured | while read file ; do echo $file | tee -a dl.list ; wget --spider $file |& grep -e Longitud -e Length | cut -d ' ' -f 1,2,3 ; done
wget -c -i dl.list -P $HOME/content/
cd ~
curl -L "https://download.kiwix.org/nightly/`date --date=yesterday +%Y-%m-%d`/kiwix-tools_linux64_`date --date=yesterday +%Y-%m-%d`.tar.gz" | tar xj

ls content/*.zim | while read line ; do echo $line ; bin/kiwix-manage library.xml add ./$line ; done
kiwix-serve --library --port=8080 ~/library.xml


wget http://pantry.learningequality.org/downloads/ka-lite/0.17/content/contentpacks/es.zip
wget https://pepe.escuelabpuno.org/descargas/en.zip
~~
