# P05 - Despliegue de escenarios multicontenedor con Docker Compose

_La tarea consiste en desplegar las aplicaciones con Docker Compose._

## Comenzando ✏️

_Estas instrucciones te permitirán obtener una copia del proyecto en funcionamiento en tu máquina local para propósitos de desarrollo y pruebas._

Mira **Deployment** para conocer como desplegar el proyecto.


### Pre-requisitos 📝

_Para poder configurar y desplegar todas las aplicaciones necesitas tener los siguientes elementos:_

```
- Docker Desktop
- Visual Studio Code
- Consola de Windows
```

### 1.Despliegue del Servidor Web Apache  💫

_Realizaremos los siguientes pasos:_

```
Creamos una carpeta con el nombre apache y dentro de ahí, añadimos un fichero llamado docker-compose.yml, donde definiremos el escenario.
```

_Documento docker-compose.yml_

```
version: '3.1'

services:
  apache:
    image: httpd:latest
   
    ports:
      - '80:8080'
    volumes:
      - ${PWD}/website:/usr/local/apache2/htdocs/
```



## Pruebas realizadas 📌

_Para lanzarlos, nos ubicamos dentro de la carpeta creada donde tenemos el fichero docker-compose.yml y lanzamos el siguiente comando:_

```
docker-compose up -d
```
_Comprobamos que la instalación se realice correctamente_

### Comprobación final ⭐

_Procedemos a ir a nuestro navegador y en la url poner lo siguiente:_

```
localhost:80
```

### 2.Mediawiki  💫

_Realizaremos los siguientes pasos:_

```
Creamos una carpeta con el nombre mediawiki y dentro de ahí, añadimos un fichero llamado docker-compose.yml, donde definiremos el escenario.
```

_Documento docker-compose.yml_

```
version: '3.1'

services:
  mediawiki:
    image: mediawiki
    restart: always
    ports:
      - 8080:80
    links:
      - database
    volumes:
      - images:/var/www/html/images
      - #./LocalSettings.php:/var/www/html/LocalSettings.php
  database:
    image: mariadb
    restart: always
    environment:
      
      MYSQL_DATABASE: my_wiki
      MYSQL_USER: wikiuser
      MYSQL_PASSWORD: example
      MYSQL_RANDOM_ROOT_PASSWORD: 'yes'
    volumes:
      - db:/var/lib/mysql

volumes:
  images:
  db:
```

## Pruebas realizadas 📶

_Para lanzarlos, nos ubicamos dentro de la carpeta creada donde tenemos el fichero docker-compose.yml y lanzamos el siguiente comando:_

```
docker-compose up -d
```
_Comprobamos que la instalación se realice correctamente_

## Procedimiento primero ❗

_Después de instalación vamos a nuestro navegador y seguimos las instrucciones para poder registrarnos, para obtener los datos tenemos que inspeccionar el fichero mariadb_

```
IP -- 172.25.0.2
user-- wikiuser
password -- example
```


## Procedimiento segundo ❗

_Cuando terminamos de configurar nuestra BBDD, nos aparecerá que tenemos que descargar el fichero LocalSettings.php, ese fichero tenemos que colocarlo en la misma carpeta_

## Procedimiento tercero ❗

_Yolvemos a nuestro fichero docker-compose.yml, donde tenemos que descomentar la línea LocalSettings.php y reiniciamos el docker compose_

```
docker-compose up -d
```


### Comprobación final ⭐

_Seguimos los pasos siguientes de la configuración, hasta que nos muestre el final del proceso_


### 3.Guestbook  ⭕

_Realizaremos los siguientes pasos:_

```
Creamos una carpeta con el nombre guestbook y dentro de ahí, añadimos un fichero llamado docker-compose.yml, donde definiremos el escenario.
```

_Documento docker-compose.yml_

```
version: '3.1'

services:

  adminer:
    image: adminer
    restart: always
    ports:
      - 8080:8080

  db:
    image: mysql:5.6
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: example
```



## Pruebas realizadas ⌛

_Para lanzarlos, nos ubicamos dentro de la carpeta creada donde tenemos el fichero docker-compose.yml y lanzamos el siguiente comando:_

```
docker-compose up -d
```
_Comprobamos que la instalación se realice correctamente_

### Comprobación final ⭐

_Procedemos a ir a nuestro navegador y en la url poner lo siguiente:_

```
localhost:80
```

_Nos debe aparecer lo siguiente: It's works_


### 4.Wordpress  💫

_Realizaremos los siguientes pasos:_

```
Creamos una carpeta con el nombre apache y dentro de ahí, añadimos un fichero llamado docker-compose.yml, donde definiremos el escenario.
```

_Documento docker-compose.yml_

```
version: '3.1'

services:

  wordpress:
    image: wordpress
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: exampleuser
      WORDPRESS_DB_PASSWORD: examplepass
      WORDPRESS_DB_NAME: exampledb
    volumes:
      - wordpress:/var/www/html

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: exampledb
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - db:/var/lib/mysql

volumes:
  wordpress:
  db:
```



## Pruebas realizadas 📶

_Para lanzarlos, nos ubicamos dentro de la carpeta creada donde tenemos el fichero docker-compose.yml y lanzamos el siguiente comando:_

```
docker-compose up -d
```
_Comprobamos que la instalación se realice correctamente_

### Comprobación final ⭐

_Procedemos a ir a nuestro navegador y en la url poner lo siguiente:_

```
localhost:80
```

### 5.Adminer  💫

_Realizaremos los siguientes pasos:_

```
Creamos una carpeta con el nombre apache y dentro de ahí, añadimos un fichero llamado docker-compose.yml, donde definiremos el escenario.
```

_Documento docker-compose.yml_

```
version: '3.1'

services:

  wordpress:
    image: wordpress
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: exampleuser
      WORDPRESS_DB_PASSWORD: examplepass
      WORDPRESS_DB_NAME: exampledb
    volumes:
      - wordpress:/var/www/html

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: exampledb
      MYSQL_USER: exampleuser
      MYSQL_PASSWORD: examplepass
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - db:/var/lib/mysql

volumes:
  wordpress:
  db:
```



## Pruebas realizadas 📶

_Para lanzarlos, nos ubicamos dentro de la carpeta creada donde tenemos el fichero docker-compose.yml y lanzamos el siguiente comando:_

```
docker-compose up -d
```
_Comprobamos que la instalación se realice correctamente_

### Comprobación final ⭐

_Procedemos a ir a nuestro navegador y en la url poner lo siguiente:_

```
localhost:80
```



## Wiki 🎉

Puedes encontrar mucho más de cómo utilizar este proyecto en nuestra [Docker](https://hub.docker.com)
* [Wordpress](https://hub.docker.com/_/wordpress)
* [Adminer](https://hub.docker.com/_/adminer)


## Autores ✒️

* **Sara Arias Menéndez** - *Trabajo* - [sara7arias](https://github.com/sara7arias)




