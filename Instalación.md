instalar cosas
sudo apt-get install wget build-essential apache2 php libapache2-mod-php php-gd libgd-dev
![](Imagen/1.png)


crear usuario y grupo
sudo useradd nagios
sudo groupadd nagcmd
sudo usermod -a -G nagcmd nagios
sudo usermod -a -G nagios,nagcmd www-data
![](Imagen/2.png)


descargar y instalar nagios
wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.2.0.tar.gz
![](Imagen/3.png)


tar -xzf nagios-4.2.0.tar.gz
![](Imagen/4.png)


cd nagios-4.2.0
sudo ./configure --with-nagios-group=nagios --with-command-group=nagcmd
![](Imagen/5.png)


compilar
sudo make all
![](Imagen/6.png)


sudo make install
![](Imagen/7.png)


sudo make install-init
![](Imagen/8.png)


sudo make install-commandmode
![](Imagen/9.png)


sudo make install-config
![](Imagen/10.png)


generar archivo de ejemplo
sudo /usr/bin/install -c -m 644 sample-config/httpd.conf /etc/apache2/sites-available/nagios.conf
![](Imagen/11.png)


activar módulos en apache2
sudo a2enmod rewrite
sudo a2enmod cgi
![](Imagen/12.png)


darle permisos al usuario nagios
sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
qwe
![](Imagen/13.png)


reiniciar servicios
sudo /etc/init.d/apache2 restart
sudo /etc/init.d/nagios restart
![](Imagen/14.png)


luego ver IP de la máquina y ya el cliente
![](Imagen/15.png)


Antes de probar nagios no podrias ya que no esta enlazado


Enlazar
sudo ln -s /etc/apache2/sites-available/nagios.conf /etc/apache2/sites-enabled
![](Imagen/16.png)


para que se nos enlace reiniciamos el servicio
sudo /etc/init.d/apache2 restart
![](Imagen/17.png)
![](Imagen/18.png)
![](Imagen/19.png)


Ya tenemos acceso a nuestro nagios pero no tiene ningún complemento funcionando


descargar plugins81.88.48.71
wget https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz
![](Imagen/20.png)


descomprimir
tar -xvzf nagios-plugins-2.3.3.tar.gz
![](Imagen/21.png)


cd nagios-plugins-2.3.3
![](Imagen/22.png)


sudo ./configure
![](Imagen/23.png)


sudo make
![](Imagen/24.png)


sudo make install
![](Imagen/25.png)


cd /usr/local/nagios/etc/objects 
![](Imagen/26.png)


una vez en esta carpeta accedemos a un fichero 
sudo nano windows.cfg
![](Imagen/27.png)


81.88.48.71
poner otro con esa ip para probarlo
AQUÍ PARA LA WEB DEL CENTRO CREÓ OTRO HOST CON LA IP DE LA PÁGINA DEL CENTRO PARA MONITOREARLO
![](Imagen/28.png)
![](Imagen/29.png)


Una vez terminado esto vamos a descomentar windows


cd /usr/local/nagios/etc
sudo nano nagios.cfg
![](Imagen/30.png)
![](Imagen/31.png)
![](Imagen/32.png)


para que coja el fichero de configuración de nagios 
sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
![](Imagen/33.png)


sudo /etc/init.d/nagios restart
![](Imagen/34.png)
