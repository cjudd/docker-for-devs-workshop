# Compose

In this lab, you learn how to compose multiple images into a single group that can be started and stopped as one unit.

## Create a Docker composition.

1. Create a docker-compose.xml file and enter the following text:

```
version: "3"
services:
  db:
    image: javajudd/nuez-db:1.0
    ports:
      - "3306:3306"
    environment:
       MYSQL_USER: ${DB_USER}
       MYSQL_PASSWORD: ${DB_PASSWORD}
       MYSQL_DATABASE: ${DB_DB}
       MYSQL_ROOT_PASSWORD: ${DB_ROOT_PASS}
  web:
    image: javajudd/nuez:1.0
    ports:
      - "80:8080"
    environment:
       DB_USER: ${DB_USER}
       DB_PASSWORD: ${DB_PASSWORD}
       DB_DB: ${DB_DB}
       DB_SERVER: db
       DB_PORT: 3306
```

2. Create a .env file to contain environment specific values and enter the following:

```
DB_USER=nuez-app
DB_PASSWORD=nuez+1
DB_DB=nuez
DB_ROOT_PASS=root+1
```

3. In the directory with the docker-compose.xml and .env file run the following to start the composition:

```
docker-compose up -d
```

This starts the continers in a daemon mode.

4. Visit [http://localhost](http://localhost) to make sure very thing came up.

5. View running containers & network.

```
docker ps
docker network ls
```

6. In the same directory as the docker-compose.xml shut everything down by running the following:

```
docker-compose down
```