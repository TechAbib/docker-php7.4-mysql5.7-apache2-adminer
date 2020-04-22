# PHP 7.4 Project

#### Install the project with Docker
```sh
$ docker-compose --build -d
$ docker exec -i ${APP_NAME}_mysql sh -c 'exec mysql -uroot -p"$MYSQL_ROOT_PASSWORD" < /docker-entrypoint-initdb.d/init.sql'
$ docker exec -it ${APP_NAME}_application bash
```