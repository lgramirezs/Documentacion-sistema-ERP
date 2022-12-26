# Instalación del Sistema
*************************

    Entorno: Desarrollo
    Usaremos $ para describir los comandos que se ejecutaran con usuario regular.
    Usaremos # para describir los comandos que se ejecutaran con superusuario.

## Requisitos

Se requiere de un Sistema Operativo de 64 bits y la instalación de algunos paquetes para el correcto funcionamiento de la aplicación:

    php >= 7.4.x
    php-gd
    php-mbstring
    php-xml
    php-tokenizer
    php-zip
    php-pgsql
    php-cli
    php-curl
    composer
    zip
    unzip
    nodejs
    postgresql

Para poder ejectutar la instalación es importante contar con el paquete [composer](https://getcomposer.org/) el cual permite gestionar las distintas dependencias y/o paquetes requeridos por el sistema y una conexión externa a Internet. Cabe destacar que para mejores resultados, se debe tener instalado composer de manera global.

Una vez instalado composer comprobamos la correcta instalación con el siguiente comando:

    $ composer --version

Por otro lado, se requiere contar con los paquetes NodeJS y NPM para gestionar los paquetes requeridos para la reactividad en la gestión de datos de algunos procesos.

Se recomienda seguir la documentación disponible desde: https://linuxconfig.org/how-to-install-node-js-on-ubuntu-16-04-xenial-xerus-linux-server pero para este manual recomendamos los siguientes pasos:

Procedimiento de instalación mediante el script nativo de node **nvm** el cual permite más
control en cuanto a la versión de **node** y **npm** a ser instalada.

Instalar los prerequisitos del S.O. mediante el siguiente comando:

    $ sudo apt install build-essential libssl-dev

Descargar el script de instalación más reciente mediante **curl**, para ello
se requiere ejecutar el comando:

    $ sudo curl -o- https://raw.githubusercontent.com/creationix/nvm/{version}/install.sh | bash

Se debe sustituir la número de versión con la más reciente publicada la
cual se puede encontrar [aquí](https://github.com/nvm-sh/nvm/releases), ejemplo:

    $ sudo curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash

Lo siguiente es configurar el acceso del nuevo script **NVM** con el siguiente comando:

    $ . ~/.profile

Esto permitira acceder al comando nvm desde cualquier ruta, una vez realizada
la configuración, se procederá a verificar el listado de versiones de **node**
disponibles en el repositorio para lo cual se require ejecutar el comando:

    $ nvm ls-remote | grep -i lts

Esto debe mostrar un listado de versiones de node que correspondan
a las versiones **LTS**, ejemplo:

v10.15.3   (LTS: Dubnium)
v10.16.0   (LTS: Dubnium)
v10.16.1   (LTS: Dubnium)
v10.16.2   (LTS: Dubnium)
v10.16.3   (Latest LTS: Dubnium)

Ahora procedemos a la instalación de la versión de node más actualizada que presente la lista, para lo cual se ejecutará el comando:

    $ nvm install 10.16.3

Una vez instalado NodeJS comprobamos la correcta instalación con el siguiente comando:

    $ node -v

Los comandos anteriores nos instalaran NodeJS y también npm, por lo cual comprobamos su correcta instalación con el siguiente comando:

    $ npm -v

Ahora se deben instalar las dependencias de php de la aplicación, por lo cual los siguientes comando se deben ejecutar dentro del directorio base de la aplicación:

    $ composer install

Una vez instaladas las dependencias, ejecuta el comando:

    $ php artisan key:generate

Esto generará un identificador único para la aplicación y creará (si no existe), el archivo de configuración .env, en caso de que no se genere dicho archivo se debe ejecutar el comando:

    $ cp .env.example .env

Luego se debe repetir el paso anterior.

Luego, en el archivo .env, localizado en la raíz del sistema, se deben establecer los parámetros de configuración necesarios bajo los cuales se ejecutará la aplicación.

    APP_NAME
    APP_ENV
    APP_KEY
    APP_DEBUG
    APP_LOG_LEVEL
    APP_URL
    APP_DEMO
    APP_TESTING
    APP_TESTING_URL

    AUDIT_LIMIT

    LOG_CHANNEL
    LOG_SLACK_WEBHOOK_URL

    DB_CONNECTION
    DB_HOST
    DB_PORT
    DB_DATABASE
    DB_USERNAME
    DB_PASSWORD

    BROADCAST_DRIVER
    CACHE_DRIVER
    SESSION_DRIVER
    SESSION_LIFETIME
    QUEUE_CONNECTION

    REDIS_HOST
    REDIS_PASSWORD
    REDIS_PORT
    REDIS_CLIENT
    REDIS_DB

    MAIL_DRIVER
    MAIL_HOST
    MAIL_PORT
    MAIL_USERNAME
    MAIL_PASSWORD
    MAIL_ENCRYPTION

    AWS_ACCESS_KEY_ID
    AWS_SECRET_ACCESS_KEY
    AWS_DEFAULT_REGION
    AWS_BUCKET

    PUSHER_APP_ID
    PUSHER_APP_KEY
    PUSHER_APP_SECRET
    PUSHER_APP_CLUSTER
    PUSHER_APP_TLS

    WEBSOCKETS_HOST
    WEBSOCKETS_PORT
    WEBSOCKETS_SSL_LOCAL_CERT
    WEBSOCKETS_SSL_LOCAL_PK
    WEBSOCKETS_SSL_PASSPHRASE

    MIX_APP_URL
    MIX_APP_ROOT
    MIX_PUSHER_APP_KEY
    MIX_PUSHER_APP_CLUSTER
    MIX_WEBSOCKETS_HOST
    MIX_WEBSOCKETS_PORT
    MIX_PUSHER_APP_TLS

De igual manera se debe instalar los paquetes necesarios para la gestión reactiva de datos, para lo cual se debe ejecutar el siguiente comando (teniendo en cuenta que se debe contar con nodejs y npm previamente instalados):

    $ npm install

El comando anterior instala todas las dependencias de node requeridas por el sistema.

## Configuración de variables

Dentro del archivo **.env** se encuentran algunas variables que deben ser configuradas previamente para el correcto funcionamiento de la aplicación las cuales se describen a continuación:

APP_NAME | Esta variable almacena el nombre de la aplicación cuyo valor por defecto es KAVAC.

APP_ENV | Establece el entorno bajo el cual se ejecuta la aplicación. Para un entorno en producción se debe establecer el valor a **production**.

APP_KEY | El valor de esta variable se establece al ejecutar el comando php artisan key:generate.

APP_DEBUG | Establece si la aplicación se ejecuta en modo de desarrollo si el valor es establecido en **true**, mostrando detalles de los eventos que se generan en la aplicación así como la barra de de desarrollo **debugbar**. Para entornos en producción esta variable debe establecerse en **false**.

APP_LOG_LEVEL | Indica el nivel de detalle para el cual se genera la bitácora de eventos y su valor por defecto es **debug** el cual establece el nivel de detalle mas amplio.

APP_URL | El valor establecido en esta variable es de importancia en otros procesos del sistema y en ella se indica el **dominio** o **IP** de la aplicación incluyendo el protocolo **http** o **https**.

APP_DEMO | El valor de esta variable determina si la aplicación se esta ejecutando en modo de demostración cuando es establecida como **true**, su valor por defecto es **false**.

APP_TESTING | Indica si la aplicación se encuentra en mnodo de prueba para lo cual se debe establecer el valor en **true**. Su valor por defecto es **false**.

APP_TESTING_URL | Establece el **dominio** o **IP** de la aplicación para pruebas incluyendo el protocolo **http** o **https**, esta variable es opcional.

AUDIT_LIMIT | Indica el límite de registros a almacenar por cada modelo de la aplicación para la auditoria.

## Notificaciones por correo

Para el correcto funcionamiento de las notificaciones del sistema mediante la gestión de correo electrónico, se deben establecer los valores necesarios del servidor de correo a utilizar por la aplicación. Estas variables son:

    MAIL_DRIVER
    MAIL_HOST
    MAIL_PORT
    MAIL_USERNAME
    MAIL_PASSWORD
    MAIL_ENCRYPTION

Donde,

MAIL_DRIVER | Es el driver de conexión al servidor de correo saliente que gestionará las notificaciones.

MAIL_HOST | Es el dominio del host de correo saliente.

MAIL_PORT | Es el puerto del servidor de correo saliente.

MAIL_USERNAME | Es el nombre del usuario con atributos para enviar correo electrónico.

MAIL_PASSWORD | Es la contraseña del usuario que gestiona el correo saliente.

MAIL_ENCRYPTION | Define el protocolo de cifrado usado por el gestor de correo electrónico. Los valores a establecer pueden ser: **ssl**, **tls** o **null**.

## Compilar archivos js y css de cada modulo de la aplicación:

    $ php artisan module:compile -s -i -p

## Base de datos

KAVAC puede ser ejecutado con diferentes gestores de Base de datos tales como PostgreSQL, MySQL, SQLite, entre otros, sin embargo se recomienda el uso del gestor de Base de datos PostgreSQL por su capacidad en la gestión de información.

Debe crear una base de datos en el gestor de su preferencia y configurarlo en el archivo .env con los datos de acceso.

Ejemplo de configuración de una base de datos de PostgreSQL:

    DB_CONNECTION=pgsql
    DB_HOST=localhost
    DB_PORT=5432
    DB_DATABASE=kavac
    DB_USERNAME=kavac
    DB_PASSWORD=kavac

Una vez configurado el gestor de base de datos, se deben ejecutar los siguientes comandos:

    $ php artisan migrate

Lo anterior creará la estructura de tablas de la base de datos necesaria para comenzar a gestionar la información.

## Registros iniciales

KAVAC, cuenta con información inicial requerida para la gestión de la aplicación, para lo cual se debe ejecutar el comando:

    $ php artisan db:seed

El anterior comando ejecutara las acciones necesarias para ingresar al sistema los datos inicialmente requeridos por la aplicación base como son: usuario, roles, permisos, localidades, estados civiles, profesiones, sectores de organizaciones y tipos de organizaciones.

La aplicación cuenta con una cantidad de módulos independientes que permiten expandir sus funcionalidades, cada uno de estos módulos cuentan con sus registros iniciales por lo que es necesario ejecutar un comando adicional que permita registrar información de cada módulo instalado y habilitado en el sistema, para ello se ejecuta el siguiente comando:

    $ php artisan module:seed

Esto revisará que módulos del sistema estan habilitados y procederá a registrar la información requerida, inicialmente, por cada uno de ellos.

Una vez que hayan sido registrado los datos iniciales del sistema, se puede autenticar en el mismo con los siguientes datos de acceso como administrador (es recomendable modificar la contraseña en el primer acceso al sistema):

    usuario: admin
    clave: 123456

El primer paso, para el correcto funcionamiento del sistema, es registrar información básica de la organización que llevará a cabo la gestión de información dentro de la aplicación, para ello se debe ingresar al menú

    Configuración > General

Y allí, en el panel **"CONFIGURAR ORGANIZACIÓN"** se deben indicar los datos de la organización. Una vez configurada, se mostrarán todas las opciones de los módulos disponibles en el sistema.

## Probar la aplicación

Para identificar si la aplicación se encuentra correctamente instalada, puedes ejecutar el comando de artisan que te permite levantar un servidor en entornos de desarrollo de la siguiente forma:

    $ php artisan serve

Este comando levanta un servidor en la dirección ip 127.0.0.1 o localhost y en el puerto 8000, para verificarlo puedes acceder a el enlace **127.0.0.1:8000**

Puedes, de igual forma asignarle una dirección IP o dominio a este comando y un puerto en donde atenderá las peticiones para lo cual se puede agregar las opciones --host y/o --port, un ejemplo de su uso sería:

    $ php artisan serve --host=192.168.1.1 --port 9000

## Procesamiento de colas

Ciertos procedimientos del sistema permiten y requieren establecer colas de trabajo para peticiones y registros con grandes cantidades de información.
Para entornos de producción se recomienda realizar una configuración previa antes de iniciar la aplicación, la descripción de esta configuración se encuentra en la sección 'Configuración extra para entornos de producción > Procesamiento de colas' de este archivo. Para activar los workers en un entorno de desarrollo, se debe ejecutar el siguiente comando, el cual debe quedar iniciado y mantenerse en una consola de comandos:

    $ php artisan queue:work

Llegado a este punto ya se debe contar con la aplicación funcional en un entorno local de desarrollo, a continuación se describen configuraciones para entornos de producción.

## Configuración extra para entornos de producción

    Entorno: Producción
    Usaremos $ para describir los comandos que se ejecutaran con usuario regular.
    Usaremos # para describir los comandos que se ejecutaran con superusuario.

Se requiere la instalación de algunos paquetes para el correcto funcionamiento de la aplicación:

    servidor de aplicaciones nginx, apache, etc
    supervisor

## Glosario

**(ruta-absoluta-de-instalacion)**: Es la ruta en donde se va a instalar la aplicación, colocando la misma sin los (), por ejemplo:

    /srv/kavac/

**(version-php-instalada)**: Es la versión del o los paquetes de PHP instalados, colocando la misma sin los (), por ejemplo: 7.4

## Configuración del servidor de aplicaciones

En esta documentación se explica como configurar un servidor de aplicaciones Nginx (para otro tipo de servidor se debe consultar la documentación pertinente para una configuración óptima en aplicaciones basadas en PHP).

### Instalar Nginx

Lo primero que se debe realizar es la instalación del servidor de aplicaciones con el comando

    # apt install nginx

Una vez completada la instalación, inicie el servicio nginx y agréguelo para que se inicie automáticamente con sistema operativo mediante el comando systemctl.

    # systemctl start nginx
    # systemctl enable nginx

El servidor Nginx se ejecutará en el puerto 80, para verificar si se ejecutó correctamente debe ejecutar el comando

    # sudo systemctl status nginx

o

    # netstat -plntu

Si todo lo muestra correctamente, nginx estará instalado y en ejecución.

### Instalar PHP-FPM

Para instalar la extensión FPM (FastCGI Process Manager) de la versión de PHP instalada en el sistema operativo se debe ejecutar el comando

    # apt install php-fpm

El próximo paso es configurar el archivo php.ini de FPM, para lo cual se deve acceder a la ruta en donde fue instalado, por lo general esta ruta se encuentra en /etc/php/(version-php-instalada)/fpm/, para esto se debe editar ejecutando

    # nano /etc/php/(version-php-instalada)/fpm/php.ini

donde (version-php-instalada) es la versión de php instalada en el servidor, Ej. 7.3

la subcarpeta **/fpm/** puede variar de acuerdo a la distribución linux utilizada por lo que puede estar presente o no.

En el contenido del archivo se debe buscar y descomentar la variable cgi.fix_pathinfo=1 y cambiar el valor a 0

    cgi.fix_pathinfo=0

A su vez, se deben realizar algunos ajustes adicionales para optimizar las peticiones para la carga d archivos por lo que es necesario establecer los siguientes valores a las variables descritas:

    upload_max_filesize = 10M

    max_file_uploads = 50

    post_max_size = 40M

Guarda las modificaciones realizadas e inicializa el servicio FPM con los comandos

    # systemctl start php(version-php-instalada)-fpm

    # systemctl enable php(version-php-instalada)-fpm

El primer comando inicializa el servicio y el segundo lo habilita para que se ejecute automáticamente al arrancar el servidor.

Por defecto en sistemas operativos como Ubuntu el servicio PHP-FPM se ejecuta bajo un archivo socket, para verificar que el servicio PHP-FPM se haya inicializado correctamente deberá escribir el comando netstat de la siguiente forma

    $ netstat -pl | grep php(version-php-instalada)-fpm

Con lo anterior, el servidor virtual para la aplicación fue creado, solo queda reiniciar el servidor nginx para que las modificaciones tengan efecto

    # systemctl restart nginx

### Configurar el servidor virtual de Nginx

Para que la aplicación se ejecute en el servidor de aplicaciones Nginx, se debe realizar una configuración adicional creando para ello un archivo que contendrá dicha configuración, para esto se ejecutara el siguiente comando

    # nano /etc/nginx/sites-available/kavac

y se agregara el siguiente contenido:

    server {
        proxy_busy_buffers_size   256k;
        proxy_buffers   4 256k;
        proxy_buffer_size   128k;
        fastcgi_buffers 16 16k;
        fastcgi_buffer_size 32k;
        fastcgi_busy_buffers_size 32k;

        listen 80;
        # Descomentar si las peticiones solo aceptan el protocolo ipv6
        # listen [::]:80 ipv6only=on;

        # Log files for Debugging
        access_log /var/log/nginx/kavac-access.log;
        error_log /var/log/nginx/kavac-error.log;

        # Webroot Directory for kavac project
        root (ruta-absoluta-de-instalacion)/public;
        index index.php index.html index.htm;

        # Your Domain Name
        server_name (nombre-de-dominio-que-atiende-las-peticiones);

        location / {
            try_files $uri $uri/ /index.php?$query_string;
        }

        # PHP-FPM Configuration Nginx
        location ~ \.php$ {
            try_files $uri =404;
            fastcgi_split_path_info ^(.+\.php)(/.+)$;
            fastcgi_pass unix:/run/php/php(version-php-instalada)-fpm.sock;
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include fastcgi_params;
        }
    }

guarda las modificaciones y cierra el archivo

Ahora para activar el servidor virtual se debe crear un enlace símbolico al archivo de configuración de la siguiente forma

    # ln -s /etc/nginx/sites-available/kavac /etc/nginx/sites-enabled/

Para que estos cambios tengan efecto se debe reiniciar el servidor de aplicaciones

    # systemctl restart nginx

## Procesamiento de colas

El sistema cuenta con procedimientos que permiten establecer colas de trabajo para peticiones y registros con grandes cantidades de información, por tal motivo es necesario realizar una configuración previa antes de iniciar la aplicación.

Dentro del archivo config/queue.php se encuentra las distintas variables a configurar para el uso de colas, por lo que se deben configurar el driver a usar para la gestión de las colas y posteriormente configurar los datos necesarios del servidor seleccionado.

Lo primero es configuar dentro del archivo de entorno (.env) la variable **QUEUE_CONNECTION** para el uso del driver a implementar en la gestión de colas, por defecto esta configurado para hacer uso del driver mediante base de datos de la siguiente manera:

    QUEUE_CONNECTION=database

Si se desea configurar otro driver para la gestión de colas se puede obtener información en la documentación oficial del framework [Laravel](https://docs.laravel.com).

Una vez configurado el servidor de colas es necesario realizar los procedimientos necesarios para que los
**workers** que procesan las colas de trabajo esten activo en todo momento, para esto es recomendable configurar a supervisorctl  de la siguiente forma:

Crear un archivo llamado **kavac-worker.conf** en la ruta **/etc/supervisor/conf.d/** con el siguiente contenido:

    [program:laravel-worker]
    process_name=%(program_name)s_%(process_num)02d
    command=/usr/bin/php <ruta-de-la-aplicacion-kavac>/artisan queue:work sqs --sleep=3 --tries=3
    autostart=true
    autorestart=true
    user=<usuario-del-sistema>
    numprocs=1
    redirect_stderr=true
    stdout_logfile=<ruta-de-la-aplicacion-kavac>/storage/logs/worker.log
    stopwaitsecs=3600

Donde:

    /user/bin/php es la ruta en donde se encuentra el comando php.

    <ruta-de-la-aplicacion-kavac> es la ruta en donde se encuentra instalada la aplicación.

    <usuario-del-sistema> es el usuario del sistema operativo en donde se encuentra la aplicación, el cual tendrá los permisos necesarios para ejecutar los distintos procesos.

Actualizar y ejecutar supervisorctl de la siguiente forma:

    $ sudo supervisorctl reread

    $ sudo supervisorctl update

    $ sudo supervisorctl start kavac-worker:*

## Websockets

La aplicación viene con un sistema de notificaciones en tiempo real con websockets por lo que es necesario iniciar y mantener el servidor que atiende y despacha estas peticiones, además de establecer algunos valores en el archivo **.env** de la siguiente forma:

    PUSHER_APP_ID=<API_ID>
    PUSHER_APP_KEY=<API_KEY>
    PUSHER_APP_SECRET=<API_SECRET>
    PUSHER_APP_CLUSTER=mt1
    PUSHER_APP_TLS=false

    WEBSOCKETS_HOST=<WEBSOCKET_IP>
    WEBSOCKETS_PORT=<WEBSOCKET_PORT>
    WEBSOCKETS_SSL_LOCAL_CERT=null
    WEBSOCKETS_SSL_LOCAL_PK=null
    WEBSOCKETS_SSL_PASSPHRASE=null

    MIX_APP_URL="${APP_URL}"
    MIX_APP_ROOT="${APP_ROOT}"
    MIX_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
    MIX_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"
    MIX_WEBSOCKETS_HOST="${WEBSOCKETS_HOST}"
    MIX_WEBSOCKETS_PORT="${WEBSOCKETS_PORT}"
    MIX_PUSHER_APP_TLS="${PUSHER_APP_TLS}"

Luego de realizada la configuración en el archivo de entorno **.env** se requiere tener instalado en el servidor de aplicaciones una aplicación que monitoree y ejecute este servicio para lo cual se utiliza la aplicación ***supervisor***.

Una vez instalado ***supervisor***, se requiere agregar y configurar un nuevo proceso que permita mantener la ejecución de los websockets de la aplicación, para lo cual se debe crear un nuevo archivo con el nombre **websockets.conf** dentro del directorio /etc/supervisor/conf.d (en Debian/Ubuntu) ó /etc/supervisord.d (en RedHat/CentOS).

El archivo creado deberá contener la siguiente información:

    [program:websockets]
    command=/usr/bin/php <ruta-de-la-aplicacion-kavac>/artisan websockets:serve
    numprocs=1
    autostart=true
    autorestart=true
    user=<usuario-del-sistema>

Donde:

    /user/bin/php es la ruta en donde se encuentra el comando php

    <ruta-de-la-aplicacion-kavac> es la ruta en donde se encuentra instalada la aplicación

    <usuario-del-sistema> es el usuario del sistema operativo en donde se encuentra la aplicación, el cual tendrá los permisos necesarios para ejecutar los distintos procesos

Con la configuración anteriormente descrita, se debe reiniciar el **supervisor** para que tome en cuenta la nueva configuración, para lo cual se ejecutan los siguientes comandos:

    $ supervisorctl update

    $ supervisorctl start websockets

Para verificar que la configuración es correcta y el servicio se este ejecutando, se puede indicar el siguiente comando:

    $ supervisorctl status

El último paso en el proceso de instalación es modificar los usuarios y permisos para el acceso del servidor a la aplicación KAVAC, para lo cual le indicamos la permisología y usuario correspondiente

    # chown -R www-data:root (ruta-absoluta-de-instalacion)

    # chmod 755 (ruta-absoluta-de-instalacion)/storage

## Laravel ER Diagram Generator

Este paquete permite generar diagramas de entidad relación inspeccionando las relaciones definidas en sus archivos de modelo. Por defecto busca los modelos en la carpeta app. Para agregar los modelos que se encuentran en cada módulo hay que hacer lo siguiente:

    // Editar en el archivo
    vendor/beyondcode/laravel-er-diagram-generator/config/config.php

    // Esta sección en la linea 9
    'directories' =[
        base_path('app'),
        // Carpeta agregada para el módulo Payroll
        base_path('modules/Payroll/Models'),
    ],

En ese ejemplo genera el diagrama del sistema base y del módulo Talento Humano.

Comando para generar el diagrama:

    $ php artisan generate:erd kavac.svg --format=svg

Para un mejor rendimiento de la aplicación en entornos de producción se recomienda utilizar el comando:

    $ composer install --optimize-autoloader --no-dev

Esto permitirá una carga más optimizada de los componentes del sistema.

## Probar la aplicación

Para identificar si la aplicación se encuentra correctamente instalada, puedes ejecutar el comando de artisan que te permite levantar un servidor en entornos de desarrollo de la siguiente forma:

    $ php artisan serve

Este comando levanta un servidor en la dirección ip 127.0.0.1 o localhost y en el puerto 8000, para verificarlo puedes acceder a el enlace **127.0.0.1:8000**

Puedes, de igual forma asignarle una dirección IP o dominio a este comando y un puerto en donde atenderá las peticiones para lo cual se puede agregar las opciones --host y/o --port, un ejemplo de su uso sería:

    $ php artisan serve --port 192.168.1.1 --port 9000

## Comandos básicos laravel-modules

Ejecutar las migraciones laravel-modules

    $ php artisan module:migrate

Crea un nuevo modelo para el módulo especificado junto con su migración

    $ php artisan module:make-model -m ModuleNameModelName ModuleName

Genera nuevo controlador restful para el módulo especificado

    $ php artisan module:make-controller ModuleNameModelName ModuleName

Genera nuevo seeder para el módulo especificado (nombre del modelo en plural)

    $ php artisan module:make-seed ModuleNameModelName ModuleName
## Licencia

Kavac es una aplicación de código abierto y se distribuye estrictamente bajo la licencia [LICENCIA DE SOFTWARE CENDITEL](http://conocimientolibre.cenditel.gob.ve/licencia-de-software-v-1-3/).
