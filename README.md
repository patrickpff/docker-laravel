
# Docker-Laravel

A fast and simplified way to prepare docker to run Laravel/PHP multiple applications with Nginx. This project is focused on old Laravel projects, and It is being tested  with Laravel Framework 5.5.50.
With these files, you can create a project with the following specifications:
  
- PHP 7.2.34
- MYSQL 5.7.22
- NGINX

... or modify and create your own project with the required speficications.

## Instalation
After downloading the project, run the following commands to build and start your Docker project:
```
docker compose build
docker compose up -d
```
This code will create the needed docker container. In MYSQL, it will create a database named "Laravel", but if you want use this only one copy of this project to more than one Laravel project, or if you need to consult data in another local database, it might be interesting to create another database inside Docker.

## Run

You can run any Artisan command with specifying the path:

```
docker-compose exec -w /var/www/html/project-name php *your artisan command here*
```

So, to generate the key for your application, you can run:

```
docker-compose exec -w /var/www/html/project-name php php artisan key:generate
```

To serve the application, just create or clone the application to the /src folder and run the following lines:

```
docker-compose exec -w /var/www/html/project-name php php artisan serve
```

It might be possible to change the permissions of your /storage folder. In orther to do that, you might run:

```
docker-compose exec -w /var/www/html/project-name php chmod o+w ./storage/ -R
```