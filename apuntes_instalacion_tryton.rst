=====================
Tryton and GNU Health
=====================
=============
Linux Mint 14
=============


Tryton
Modulo GNU Health
Referencias externas para el diseño del presente tutorial:
http://en.wikibooks.org/wiki/GNU_Health


Sobre el Entorno Virtual
========================

Notas iniciales sobre métodos de instalación:

:apt-get:		Instalador standard de Linux
:easy_install:	Instala paquetes Python última versión
:pip:			Versión mejorada de easy_install. Brinda la
posibilidad de desinstalar.
:virtualenv:	Crea entornos virtuales (carpetas) donde con pip
instalamos.


Indice General
==============

* Herramienta pip
* PostgreSQL (Capa 3)
* Virtualenv
* Dependencias de Tryton
* Emisión de reportes en otros formatos
* Pythonbrew
* Geany IDE
* Configuración de PostgreSQL
* Localización
* Tryton Servidor (Capa 2)
* Tryton Cliente (Capa 1)



Dependencias generales:

.. code-block:: bash

   $ sudo apt-get install build-essential python-dev
   $ sudo apt-get install bzip2-dev libbz2-dev curl
   $ sudo apt-get install libsqlite3-dev


Herramienta pip para la instalación de paquetes Python
------------------------------------------------------

Instalamos el meta-paquete que contiene la herramienta easy_install que
utilizaremos para obtener la versión más actualizada de pip:

.. code-block:: bash

   $ sudo apt-get install python-setuptools

Instalamos pip:

.. code-block:: bash

   $ sudo easy_install pip


Instalación de motor de bases de datos PostgreSQL
=================================================

Instalación del motor de base de datos PostgreSQL:

.. code-block:: bash

    $ sudo apt-get install postgresql-9.1

Para controlar PostgreSQL desde una interfaz de cliente:

.. code-block:: bash

    $ sudo apt-get install pgadmin3


Configuración de PostgreSQL
---------------------------




Manejo de entorno virtuales con Virtualenv
==========================================

Instalación de la herramienta en la carpeta del usuario:

.. code-block:: bash

    $ pip install --user virtualenv

Agregamos al PATH la carpeta donde pip instala los paquetes Python del usuario
($HOME/.local/bin):

.. code-block:: bash

    $ echo “export PATH=$HOME/.local/bin:$PATH” >> $HOME/.bashrc
    $ source $HOME/.bashrc

Preparamos un lugar donde agrupar entornos virtuales:

.. code-block:: bash

    $ mkdir -p $HOME/src/virtualenvs
    $ cd $HOME/src/virtualenvs

Creamos el entorno:

.. code-block:: bash

    $ virtualenv TRYTON
    New python executable in $HOME/src/virtualenvs/TRYTON/bin/python
    Installing setuptools............done.
    Installing pip...............done.

Para activar el entorno, cualquiera de las siguientes líneas de comando será
válido:

.. code-block:: bash

    $ . $HOME/src/virtualenvs/TRYTON/bin/activate

.. code-block:: bash

    $ source $HOME/src/virtualenvs/TRYTON/bin/activate

Verificamos de la siguiente manera:

.. code-block:: bash

    (TRYTON) $ which python
    $HOME/src/virtualenvs/TRYTON/bin/python

Esta es la ruta al intérprete Python de nuestro entorno virtual activo.

Para desactivar/salir del entorno:

.. code-block:: bash

    (TRYTON)$ deactivate


Ahora podemos comprobar que regresamos al entorno Python global:

.. code-block:: bash

    $ which python
    /usr/bin/python


Instalación de dependencias de Tryton
-------------------------------------

Dependencias a instalar para la posterior compilacioń del paquete Python lxml:

.. code-block:: bash

    $ sudo apt-get install libxml2-dev libxslt1-dev

.. code-block:: bash

    (TRYTON)$ pip install lxml==2.3.6 relatorio python-dateutil pytz polib vobject pywebdav

Para la posterior compilación del paquete psycopg2, debemos proceder a agregar
las siguientes librerías relacionadas con el repositorio empleado durante la
instalación de PostgreSQL:

.. code-block:: bash

    $ sudo apt-get install libpq-dev libpq5

En el caso de haber instalado PostgreSQL desde algún backports, dichas
librerías deberán instalarse de la misma forma:

.. code-block:: bash

    $ sudo apt-get install -t squeeze-backports libpq-dev libpq5

Instalamos el paquete que nos servirá de conexión a la base de datos:

.. code-block:: bash

    (TRYTON)$ pip install psycopg2

Dependencias e instalación del paquete python-ldap:

.. code-block:: bash

    $ sudo apt-get install libldap2-dev libsasl2-dev
    (TRYTON)$ pip install python-ldap


Emisión de reportes en otros formatos
-------------------------------------

.. code-block:: bash

    $ sudo apt-get install python-uno unoconv
    $ sudo apt-get install openoffice.org


Validación del CUIT de Argentina en Tryton
==========================================

Instalación de Mercurial
------------------------

.. code-block:: bash

    $ sudo apt-get install mercurial

Vatnumber
---------
http://pypi.python.org/pypi/vatnumber/
https://code.google.com/p/vatnumber/

El paquete Python ** vatnumber ** es una herramienta que nos permite validar
VAT’s (Value Added Tax) de varios países. En el caso de Argentina, los códigos
CUIT/CUIL.

Mediante 

esde su repositorio de fuentes. Proyecto Python

.. code-block:: bash

    $ hg clone https://code.google.com/p/vatnumber

Luego de obtener 

.. code-block:: bash

    destination directory: vatnumber
    requesting all changes
    adding changesets
    adding manifests
    adding file changes
    added 73 changesets with 125 changes to 12 files
    updating to branch default
    resolving manifests
    getting .hgtags
    getting CHANGELOG
    getting COPYRIGHT
    getting INSTALL
    getting LICENSE
    getting MANIFEST.in
    getting README
    getting setup.py
    getting vatnumber/__init__.py
    getting vatnumber/tests.py
    10 files updated, 0 files merged, 0 files removed, 0 files unresolved

Revisando el contenido de la carpeta *** vatnumber *** que hemos descargado:

.. code-block:: bash

    $ cd vatnumber
    $ ls -a
    .  ..  CHANGELOG  COPYRIGHT  .hg  .hgtags  INSTALL  LICENSE  MANIFEST.in  README  setup.py  vatnumber

Antes de proceder a instalar, debemos recordar activar el entorno virtual:

.. code-block:: bash

    $ . $HOME/src/virtualenvs/TRYTON/bin/activate
    (TRYTON)$ python setup.py install




    (TRYTON)$ pip freeze | grep vatnumber
    vatnumber==1.0


Manejo de versiones de Python en $HOME mediante Pythonbrew
----------------------------------------------------------

Instalar Pythonbrew en $HOME:

.. code-block:: bash

    $ pip install --user pythonbrew
    $ echo "[[ -s $HOME/.pythonbrew/etc/bashrc ]] && source $HOME/.pythonbrew etc/ bashrc" >> $HOME/.bashrc
    $ source .bashrc
    $ pythonbrew_install --verbose 2.7.3
    $ cd $HOME/.pythonbrew/

Comandos más comunes http://pypi.python.org/pypi/pythonbrew:

.. code-block:: bash

    $ pythonbrew list
    $ pythonbrew list -k

Activación temporal de una versión de Python instalada con Pythonbrew:

.. code-block:: bash

    $ pythonbrew use 2.7.3

Activación permanente de una versión de Python instalada con Pythonbrew:

.. code-block:: bash

    $ pythonbrew switch 2.7.3

Desactivar pythonbrew:

.. code-block:: bash

    $ pythonbrew off

Si falta algún paquete que necesita Python, se debería desinstalar la versión
de Python relacionada:

.. code-block:: bash

    $ pythonbrew uninstall 2.7.3

Instalar librerías faltantes, y luego volver a compilar Python con Pythonbrew:

.. code-block:: bash

    $ pythonbrew install --verbose 2.7.3


Geany IDE
=========

.. code-block:: bash

    $ sudo apt-get update && sudo apt-get upgrade -f
    $ sudo apt-get install libgtk2.0-dev intltool

Descargar Geany y Plugins de la página oficial y compilarlos:

.. code-block:: bash

    $ ./configure
    $ make
    $ sudo make install

Paquetes para chequear códigos python
-------------------------------------

http://pypi.python.org/pypi/pep8
http://pypi.python.org/pypi/pyflakes

.. code-block:: bash

    $ pip install --user pep8 pyflakes


Configuración de PostgreSQL
---------------------------

Agregar clave al usuario postgres

.. code-block:: bash

    $ sudo passwd postgres

Encriptar password creado:

.. code-block:: bash

    $ psql -c "ALTER USER postgres WITH ENCRYPTED PASSWORD '$Mandrake8419';"
    ALTER ROLE

-e: Muestra el comando SQL
-s: Convierte al usuario en SUPERUSER

.. code-block:: bash

    $ createuser -e -s -P anonymous
    CREATE ROLE anonymous SUPERUSER CREATEDB CREATEROLE INHERIT LOGIN;

En caso de haber usado “createuser -e -s anonymous” sin el parametro “-P”,
usamos:

.. code-block:: bash

    $ psql -c "ALTER USER anonymous WITH ENCRYPTED PASSWORD '$Mandrake8419';"

Reiniciamos PostgreSQL:

.. code-block:: bash

    $ sudo service postgresql restart

Iniciamos el cliente Tryton:

.. code-block:: bash
    
    $ cd tryton/bin
    $ ./tryton

Script para la ejecución del demonio automático:
http://debian.tryton.org/gitweb/?p=packages/tryton-server.git;a=blob_plain;f=debian/tryton-server.init;hb=HEAD

http://code.google.com/p/tryton/wiki/InstallationOnDebian

Cambiar solamente el user:

.. code-block:: bash

    DAEMONUSER="tryton"

Agregar el demonio a /etc/init.d y darle permiso de ejecución.


Localización
============

Agregaremos la traducción es_ES en Tryton.

Desde el cliente Tryton, navegamos al menú ** Administración > Localización > 
Idiomas ** y seleccionando el idioma de código ** es_ES ** para marcarlo como 
“Traducible”. Y guardamos desde la barra de herramientas (o pulsando CTRL + s):

Para que los términos en Español (España) se inserten en la base de datos, es
necesario correr el servidor en modo actualización de la siguiente manera:

.. code-block:: bash

    $ . $HOME/src/circulo/ENV/TRYTON_24/activate
    (TRYTON_24)$ ./trytond -c $HOME/src/circulo/trytond.conf -d circulo243 -u all


Instalar Tryton Servidor (Capa 2)
=================================

Descargamos el paquete desde la pagina oficial

Los siguientes pasos son a modo de recomendación en cuanto a organización de
carpetas, archivos...

.. code-block:: bash

    $ mkdir /home/usuario/proyecto
    $ cd /home/usuario/proyecto/tryton-server
    $ wget http://downloads1.tryton.org/2.4/trytond-2.4.3.tar.gz


Instalar Tryton Cliente (Capa 1)
=================================

.. code-block:: bash

    $ mkdir /home/usuario/proyecto
    $ cd /home/usuario/proyecto/tryton-cliente
    $ wget http://downloads1.tryton.org/2.4/tryton-2.4.2.tar.gz


Traducción del módulo Health al Español =======================================

Link de ayuda: http://en.wikibooks.org/wiki/GNU_Health/Localization

Crear una cuenta personal en Transifex:

https://www.transifex.com/projects/p/GNU_Health/language/es/


GNU Health core Module

.. code-block:: bash

    mv archivo.po /trytond/modules/health/locale
    nano /trytond/modules/health/__tryton__.py


.. code-block:: python

	'translation': [
	],


.. code-block:: python

    'locale/es_AR.po',
        'translation': [
        'locale/es_AR.po',
    ],


