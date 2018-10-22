# Run Docker Container

In this lab, you will pull a Tomcat 7 images and run it as a container.

## Pull image and Run container.

1. Using the run command to pull the image and run a container.

```
docker run -it --rm -p 8080:8080 tomcat:7.0-jre7
```

-it runs a container in an interactive terminal mode meaning standard in and out in the terminal will go to the container. --rm means when you press Ctrl+C to terminate the container, the container will be removed reclaiming diskspace. The -p maps a port on your computer to an internal container port. tomcat:7.0-jre7 represents the image you want to run as a container.

2. Validate Tomcat is running by opening up a browser and going to [http://localhost:8080](http://localhost:8080).

You should see the standard Tomcat congradulations page.

## Determine container details

1. In a separate terminal, determine the container name and id.

```
docker ps
```

NOTE: You can see all containers regardless if they are running or not using the docker ps command as well with the -a option.

```
docker ps -a
```

## Shut down container

1. Use Ctrl+C to shut down container.
2. Restart container again to see how quickly it starts up after the image is cached.
3. Use Ctrl+C again to shut down the container.
