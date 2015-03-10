# meran-unlp-en-debian7
 Esto es un intento de correr Meran UNLP en Debian wheezy (7) https://github.com/Desarrollo-CeSPI/meran

Vamos a tener que mover todos los módulos de perl 5.14 a 5.10 que es la plataforma donde esta probado qeu funciona MERAN.
Para ello hay que:

Agregar en apt.sources:

deb http://ftp.debian.org/debian/ squeeze main contrib non-free
deb http://security.debian.org/ squeeze/updates main contrib non-free

Setear las preferencias del apt:

En /etc/apt/preferences.d/preferences

Package: perl*
Pin: release a=oldstable
Pin-Priority: 700

Package: libapache2-mod-perl2
Pin: release a=oldstable
Pin-Priority: 700

Package: *-perl
Pin: release a=oldstable
Pin-Priority: 700

Package: *
Pin: release a=stable
Pin-Priority: 600

Una vez hecho esto:

apt-get update
PERL=$(dpkg -l|grep perl|awk '{print $2}')
apt-get install --reinstall $PERL

Recien una vez allí ejecutar el instalador

Problemas que fui encontrando además en el instalador:

Problema con permisos de la tabla sugerencia- > reportado en issue al proyecto padre

Problemas de dependencias (aún no reportado):

apt-get install libmysqlclient18 libssl0.9.8 libjpeg62
