# Práctica CLI

## Administración de Wordpress con la utilidad WP-CLI

Para esta práctica se usa un script el cual ejecuta la instalación de una pila LAMP seguido de WP-CLI, una herramienta de instalación de Wordpress a través de comandos. Para ello se usan los siguientes comandos:

- Primero cambiamos al directorio /var/www/html para que se ejecute todo en ese directorio:

    `cd /var/www/html`

- Descargamos y damos permisos de ejecución al archivo de WP-CLI:

    ```
    curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
    chmod +x wp-cli.phar
    ```

- Le cambiamos el nombre al archivo para poder usar los comandos:

    `mv wp-cli.phar /usr/local/bin/wp`

- Eliminamos el index.html para no crear conflictos:

    `rm -rf index.html`

- Ahora descargamos los archivos necesarios para la instalación de Wordpress y creamos el archivo de configuración. --allow-root nos permite ejecutar estos comandos con el usuario root:

    ```
    wp core download --path=/var/www/html --locale=es_ES --allow-root
    wp config create --dbname=$DBNAME --dbuser=$DBUSER --dbpass=$DBPASS --allow-root
    ```

- Cambiamos los permisos de la carpeta html:

    `chown -R www-data:www-data /var/www/html`

- Instalamos los paquetes:

    `wp core install --url=$URL --title=$TITLE --admin_user=$USER --admin_password=$PASS --admin_email=$EMAIL --allow-root`

Todas las variables están declaradas al principio del script.