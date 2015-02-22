# TEMA 2

Ya habremos hecho 2 instalaciones en el Virtualbox, tanto debian como fedora, para poder continuar el tema.


## Paqueteria

### Gestor RPM

Los paguetes RPM se componen de:

* *nombre-versión-edición.arquitectura.rpm*

#### Instalación

* *rpm -i nombredepaquete.rpm*

#### Actualización

* *rpm -Uvh nombredepaqueteactualizar.rpm*
* *rpm -Fvh *.rpm*

#### Borrado

* *rpm -e nombredelpaquete*
 * --force (en caso de conflicto)
 * --nodeps  (forzar instalación obviando dependencias) 

#### Consultas

* *rpm -a* (lista todos los paquetes)
* *rpm -i* (información general del paquete)
* *rpm -l* (lista de ficheros instalados)
* *rpm -f nombre* (encuentra el paquete con lo que se le proporciona)
* *rpm -p nombre* (busqueda en el fichero con lo que se le proporciona)
* *rpm --requieres* (dependencias del paquete)
* *rpm --provides* (proporción del paquete)
* *rpm --scripts* (scripts que se ejecutan en la instalación y borrado)
* *rpm --changelog* (historico del paquete)

#### Verificación

* *rpm -v nombredelpaquete* ( Esto da una salida del tipo:   *"S.5.... c /ruta/nombredelfichero"*)
 * 5 (la suma del MD5 no es válida)
 * s (Modificacíon del tamaño del fichero)
 * T (La fecha de modificación se ha cambiado)
 * U (Modificación del propietario)
 * G (Modificación del grupo)
 * L (Modificación del vínculo simbólico)
 * M (Modificación del los permisos o el tipo de fichero)
 * D (Modificación del periférico)
* *gpg --import RPM-GPG-KEYVALIDA*
* *rpm --import RPM-GPG-KEYVALIDA*
* *rpm --checksig nombredelfichero.rpm*

#### Dependencias

* *rpm -ivh --aid nombredelpaquete.rpm* (solo funciona con paqueteria oficial)

#### Actualizaciones automatizadas

* *up2date*

### YUM

Yum es un programa de gestión de paquetes de rpm


#### Configuración de repositorios

* */etc/yum.repos.d*
 * name (nombre del repo, detallado)
 * baseurl (Url del repo)
 * gpgcheck (verificación del GPG del repo)
 * enabled (0 ausente, 1 activo)
 * gpgkey (ruta de la clave pública)
* */etc/yum.conf*

#### Utilización de repositorios

* ##### Refresco de caché
 * *yum makecache*
 * *yum clear all*

* ##### Listado de paquetes
 * *yum list*
  	* all (listado primero de paquetes instalados y después los disponibles para instalar)
  	* available (disponibles para instalar)
  	* updates (disponbles para actualizar)
  	* installed (actualizados)
  	* obsoletes (paquetes obsoletos debido a las nuevas versiones)
  	* recent (ultimos paquetes añadidos en los repos)
  	* repolist (repos configurados desde config de fichero)

 * *yum info nombredelpaquete*

* ##### Instalación de paquetes

 * *yum install nombredelpaquete*

* ##### Actualizaciones
 * *yum check-update*
 * *yum update* (Actualización de un paquete o todos si no se especifica)
 * *yum upgrade* (Actualización de la distribución completa)
 *  *yum list --exclude=kernel\ update* (para evitar la actualización de paquetes, esto se puede meter directamente a fichero de configuración) 

* ##### Busqueda de un paquete

 * *yum search nombredelpaquete*

* ##### Supresión de un paquete

  * *yum remove nombredelpaquete*

### Gestor DEB

#### dpkg: El gestor de Debian

 * *dpkg* (suele estar la base de datos en */var/lib/dpkg* y los estados de los paquetes en */var/lib/dpkg/status*)
 * *Gdebi* (interfaz gráfica)

#### Instalación

 * *dpkg -i nombredelpaquete.deb*


#### Actualización

 * *dpkg -r directorio* (actualiza todos los .deb que haya en el directorio)

#### Supresión

 * *dpkg -r nombredelpaquete*
 * *dpkg -P nombredelpaquete* (purga todo, ficheros config, etc)
 * *dpkg --force-all --purge nombredelpaquete* (fuerza toda la desinstalación completa)

#### Ejemplos rápidos con dpkg

* ##### Listar paquetes

  * *dpkg -l* (se puede jugar con *grep* para encontrar el paquete exacto)
  * *dpkg --get-selections* (se puede jugar con *grep* para encontrar el paquete exacto)

* ##### Encontrar un paquete que contiene un fichero

 * *dpkg -S /usr/bin/base64* (encontrará que es del paquete "coreutils")

* ##### Listar el contenido de un paquete

  * *dpkg -L coreutils | grep usr*

* ##### Conversión de paquetes
  * *alien -d nombredelpaquete.rpm*
  * *alien --scripts -d nombredelpaquete.rpm* (no incluye los scripts de pre y post instalación)
  * *dpkg -I nombredepaqueteconvertido.deb*

#### Dselect

 * Herramienta obsoleta para gestión de paquetes, ahora se usa APT debido a que es mucho mejor herramienta.

### APT

#### Que es APT

  * Es un gestor de paquetes que instala y busca los paquetes faltantes en una instalación.

#### Repositorios

* ##### Configuración

  *  * */etc/apt/sources.list* (la distribución dentro del fichero es *deb uri distribución componente1 componente2 ...* )

* ##### Actualización de bases de datos

 * *apt-get update*

* ##### Actualización de distribución

 * *apt-get upgrade* (actualiza la paqueteria)
 * *apt-get dist-upgrade* (actualiza la paqueteria a nueva distribución completa)

* ##### Buscar e instalar un paquete individual

 * *apt-cache search nombredelpaquete*

* ##### Cliente gráfico

 * *synaptic*

#### Instalación desde fuentes

* ##### Obtener fuentes

 * Se baja un tar.gz o tar.bz2 cualquiera para la instalación
 * Se descomprime *tar zxvf nombredelprograma.tar.gz* o *tar xvjf nombredelprograma.tar.bz2*

* ##### Requisitos y dependencias

 * */configure*
  * *--help* (se buscan los parámetros para ver que opciones de configuración hay disponibles)

* ##### Instalación

 * *make* (compila el programa)
 * *make install* (instala el programa compilado en el sistema)

* ##### Borrado

 * *make uninstall*

* ##### Makefile
 * Normalmente el makefile tiene todos los comandos gcc o para la compilación del paquete.

### Gestión de librerias compartidas

#### Que son las librerias compatidas

* Son un conjunto de funciones, API, accesible por cualquier programa. En linux se llaman Shared Objects (.so). Puede tener varias versiones, no compatible entre si.

#### Almacenamiento

* */lib/* (Librerias básicas, vitales)
* */usr/lib/* (librerias básicas)
* */usr/local/lib/* (librerias locales)
* *usr/X11R6/lib/* (Librerias X)
* */opt/gnome3/lib* (librerias GNOME 3)

#### Librerias vinculadas

 * *ldd nombredelprograma*

#### cache de ediror de vínculos

 * *ldconfig*
   * *-v* (Modo Verbose)
   * *-N* (No vuelve a hacer la caché)
   * *-X* (No actualiza los vínculos)
   * *-p* (Lista el contenido de la caché)