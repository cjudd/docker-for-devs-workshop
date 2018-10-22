# Docker Machine (Docker Toolbox only)

In this lab, if you are using Docker Toolbox, you will create a new Docker Machine to sandbox the workshop labs from any Docker Machines you may be using for work.

## List existing Docker Machines.

1. Determine if there are any existing machines already on your computer using the docker-machine command-line and it's ls command.

```
docker-machine ls
```

## Create a new lab Docker Machine.

1. Create a new virtualbox based Docker Machine on your computer.

```
docker-machine create --driver=virtualbox lab
```

2. List the Docker Machines again and notice you have a new lab machine and none of them are active.

```
docker-machine ls
```

3. Make the lab machine the active machine so all docker command-line commands in that terminal will be sent to lab machine.

NOTE: Any new terminals will also need to run this command.

```
docker-machine env lab
eval "$(docker-machine env lab)"
```

On Windows you will have to specify the shell as either cmd or powershell.

```
docker-machine env --shell cmd lab
docker-machine env --shell powershell lab
docker-machine env --shell powershell lab | Invoke-Expression
```

4. Validate the lab is the active machine by listing Docker Machines again and determining the lab machine has an asterisk next to it in the active column.

```
docker-machine ls
```

## Determine ip address of Docker Machine

1.  Determine the ip address of your machine so you can use deployed web applications.

```
docker-machine ip lab
```

## Removing the lab Docker Machine after the workshop

Upon completing the workshop, you may want to reclaim the disk space consumed by the lab machine.

```
docker-machine rm lab
```