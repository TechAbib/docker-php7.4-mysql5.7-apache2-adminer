# PHP 7.4 Project

##### Used images:

* [php:7.4-fpm] - php 7.4
* [mysql:5.7] - mysql
* [adminer:4.7.6-standalon] - adminer
* [webdevops/apache:ubuntu-18.04] - apache2

- https://hub.docker.com/

#### 1. Copy / Git Pull your project files into the app folder.

#### 2. Copy the .env.example file, and rename it to .env

#### 3. Modify the .env file as you want

```sh
###########################################################
###################### General Setup ######################
###########################################################

### APPLICATION ###########################################

APP_NAME=docker

### PATHS #################################################

APP_DOCUMENT_ROOT=/var/www/public

# Point to the path of your applications code on your host
APP_CODE_PATH_HOST=/var/www

# Point to where the `APP_CODE_PATH_HOST` should be in the container. You may add flags to the path `:cached`, `:delegated`. When using Docker Sync add `:nocopy`
APP_CODE_PATH_CONTAINER=/var/www:cached

###########################################################
################ Containers Customization #################
###########################################################

### APACHE ################################################

APACHE_HOST_HTTP_PORT=80
APACHE_HOST_HTTPS_PORT=443
APACHE_HOST_LOG_PATH=./logs/apache2
APACHE_SITES_PATH=./apache2/sites
APACHE_PHP_UPSTREAM_CONTAINER=app
APACHE_PHP_UPSTREAM_PORT=9000
APACHE_PHP_UPSTREAM_TIMEOUT=60
APACHE_DOCUMENT_ROOT=${APP_DOCUMENT_ROOT}

### MYSQL #################################################

MYSQL_VERSION=5.7
MYSQL_DATABASE=docker
MYSQL_USER=root
MYSQL_ROOT_PASSWORD=root
MYSQL_PASSWORD=root
MYSQL_PORT=3306
MYSQL_ENTRYPOINT_INITDB=./docker/mysql/scripts
```

#### 4. Install the project with Docker
```sh
$ docker-compose --build -d
$ docker exec -i ${APP_NAME}_mysql sh -c 'exec mysql -uroot -p"$MYSQL_ROOT_PASSWORD" < /docker-entrypoint-initdb.d/init.sql'
$ docker exec -it ${APP_NAME}_application bash
```

#### 5. It should be run on http://localhost