# Create Image

In this lab, you will inherit from an existing image to create your own custom image.

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

4. List the images so you can see the images has been created.

```
docker images
```