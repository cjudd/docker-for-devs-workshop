# Docker Machine (Docker Toolbox only)

If you are using Docker Toolbox, you have one or more machines that are represented by virtual machines in Virtual Box. A machine may or may not have been created for you during the installation process. But to make sure the labs are run in a sandbox and to make sure you don't accidently cause any problem with a machine you are using for work, you should create a separate lab machine.

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

5. Determine the ip address of your machine so you can use deployed web applications.

```
docker-machine ip lab
```