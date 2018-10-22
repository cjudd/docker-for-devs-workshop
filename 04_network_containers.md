# Create Network

In this lab, you will create a new network and then network a MySQL client container and then create a custom application image and network it together.

## Create new network.

1. List current networks.

```
docker network ls
```

2. Create new nuez-network.

```
docker network create nuez-network
```

3. List the networks to make sure the nuez-network was added.

```
docker network ls
```

4. Connect the running nuez-db container to the network.

```
docker network connect nuez-network nuez-db
```

## Run another container in the network

Now you will run another MySQL container so you can connect to the MySQL database in the nuez-db.

1. Run another mysql image.

```
docker run -it --network nuez-network --rm mysql:5.5.45 bash
```

This will run bash in a new mysql container that is appart of the neuz-network in an interactive terminal mode so you can run sql commands against the database.

2. In bash, run the mysql command-line to connect to the database in the nuez-db container.

```
mysql -h nuez-db -u nuez-app -pnuez+1 nuez
```

The network creates a dns using the containers name so you can specify the host with the container name.

3. At the mysql command prompt, run any valid MySQL commands.

```
show databases;
```

4. After running MySQL commands, type exit and press enter to exit mysql command prompt.

5. On the bash prompt, type exit and press enter to exit the bash prompt, remove the temporary container and return to your host prompt.

## Build and run application

Now you will build and run an image containing the nuez application that will connect to the nuez-db.

1. Create a new Dockerfile in an empty directory for the nuez application. Populate the file with the following:

```
FROM tomcat:7.0-jre7

RUN rm -rf $CATALINA_HOME/webapps/ROOT
RUN rm -rf $CATALINA_HOME/webapps/ROOT.war
RUN rm -rf $CATALINA_HOME/webapps/docs
RUN rm -rf $CATALINA_HOME/webapps/examples
RUN rm -rf $CATALINA_HOME/webapps/manager
RUN rm -rf $CATALINA_HOME/webapps/host-manager

ENV CATALINA_OPTS -Dgrails.env=docker

ADD https://s3.amazonaws.com/cmj-presentations/docker-for-devs/nuez.war $CATALINA_HOME/webapps/ROOT.war

CMD ["catalina.sh", "run"]
```

This inherits from an existing tomcat images. For security best practices, it removes unnecessary applications running in Tomcat. It then sets an envoronment variable putting the application into a mode that uses environment variables to configure database connections. Finally it copies the war file to the root and runs tomcat.

2. In the directory containing Dockerfile, build the nuez application image.

```
docker build -t nuez .
```

3. Run the nuez application image configuring the database with environment variables.

```
docker run --name nuez --network nuez-network -d -e DB_SERVER=nuez-db -e DB_PORT=3306 -e DB_DB=nuez -e DB_USER=nuez-app -e DB_PASSWORD=nuez+1 -p 80:8080 nuez
```

Sometimes for debugging purposes, it is easier to run it in a temperary interactive mode before running it as a deamon.

```
docker run --name nuez --network nuez-network -it --rm -e DB_SERVER=nuez-db -e DB_PORT=3306 -e DB_DB=nuez -e DB_USER=nuez-app -e DB_PASSWORD=nuez+1 -p 80:8080 nuez
```

4. In a browser go to http://localhost to make sure it is running.

## Other helpful commands

Equivilant to SSHing into the running container:

```
docker exec -it nuez bash
```

See files that have been created, deleted or changed in a running container:

```
docker diff nuez
```

View standard out of entrypoint application/script for debugging purposes.

```
docker logs
```
