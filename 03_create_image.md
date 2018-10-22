# Create Image

In this lab, you will inherit from an existing image to create a custom nuez-db MySQL image.

## Create Mysql image.

1. In an empty directory, create a Dockerfile (the name of the file is Dockerfile with an upper case D and no file extension).

2. Edit the Dockerfile to contain the Docker instructions to inherit from an existing mysql image.

```
FROM mysql:5.5.45

RUN echo America/New_York | tee /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata
RUN echo "lower_case_table_names = 1" >> /etc/mysql/my.cnf

ENTRYPOINT ["/entrypoint.sh"]
CMD ["mysqld"]
```

FROM identifies which image to inherit from.
RUN runs any valid linux commands to configure the image.
ENTRYPOINT specifies what application or script to run when the container starts.
CMD are parametes passed the ENTRYPOINT.

So this creates a new mysql images based on 5.5.45 with the timezone set to EST with lower case table name enabled and runs a script enabling mysql as a deamon.

3. In the directory with the Docker file, build the image.

```
docker build -t nuez-db .
```

This command builds the image giving it the name nuez-db using the Dockerfile from the current directory.

4. List the images so you can see the images has been created.

```
docker images
```

5. Run custom MySQL container.

```
docker run --name nuez-db -e MYSQL_USER=nuez-app -e MYSQL_PASSWORD=nuez+1 -e MYSQL_DATABASE=nuez -e MYSQL_ROOT_PASSWORD=root+1 -p 3306:3306 -d nuez-db
```

The runs the nuez-db images as a containers with the same name as nuez-db. It sets some optional environment variables inherited from the base image such as MYSQL_USER, MYSQL_PASSWORD and MYSQL_DATABASE to create a new user and database/schema. It also sets the required MYSQL_ROOT_PASSWORD to set a password for the root user. Finally it exposes the internal container port of 3306 externally as 3306 too and runs the container in the detached mode which I like to think about as a deamon mode since it will run in the background until you stop it.

6. List running containers.

```
docker ps
```