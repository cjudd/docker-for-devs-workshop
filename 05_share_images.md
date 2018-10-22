# Share Images

In this lab, you will share images with your family and friends.

## Create a Docker Hub account.

1. If you don't have one already, create an account at [https://hub.docker.com/](https://hub.docker.com/).

2. On the command-line, loggin into Docker Hub.

```
docker login
```

## Share the images

1. From the directory containing the nuez-db Docker file, run a build tagging the image and push the container.

```
docker build -t javajudd/nuez-db:1.0 .
docker push javajudd/nuez-db
```

NOTE: Replace javajudd with your docker id.

2. From the directory containing the nuez app Docker file, run a build tagging the image and push the container.

```
docker build -t javajudd/nuez:1.0 .
docker push javajudd/nuez
```

3. Visit your docker account and see if the two images are listed.