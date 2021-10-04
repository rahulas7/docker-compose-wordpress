Wordpress with docker compose

Here docker compose is used to set up wordpress in a docker container using docker volumes and bridge network.

services:
  database:
    image: mysql:5.7
    container_name: database
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: password123
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
    networks:
      - wp-net

  wordpress:
    depends_on:
      - database
    image: wordpress:latest
    volumes:
      -  wp_data:/var/www/html
    ports:
      - "80:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: database
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
    networks:
      - wp-net

## Environment Variables

#### MYSQL_ROOT_PASSWORD
 * Mysql root password  
#### MYSQL_DATABASE
 * Name of the database  
#### MYSQL_USER
 * Mysql username  
#### MYSQL_PASSWORD
 * Password of mysql user  

#### WORDPRESS_DB_HOST
 * Specify wordpress database host  
#### WORDPRESS_DB_USER
 * Database user  
#### WORDPRESS_DB_PASSWORD
 * Password of database user  
#### WORDPRESS_DB_NAME
 * Name of wordpress database

#### Networks
 * wp-net

#### Volumes
 * db_data
 * wp_data

