# DockerCommands

All command i learn for docker

## 1. Start container

Format of new command: **docker \<command> \<sub-command>**

**Image**: binaries + libraries + source code; that all make up your application  
**Container**: is the running instance of the **image**

| Commands : | Description : |
| :--------- | :------------ |
| docker **version** | See client and server |
| docker **info** | Display system-wide information |
| docker **+ enter** | get the a list of most common command for docker |
| docker container **--help** | Help must use all the time needed |
| docker **container run** --publish 80:80 nginx <br> **ctrl-c** (stop the server)| Create a new container NGINX (est un logiciel libre de serveur Web) |
| docker **container run** --publish 80:80 **--detach** nginx | Same but detached container |
| docker **container ls** <br> old command: docker ps| Shows by default running containers |
| docker container **ls -a** | Shows all containers |
| docker container **start** <**first digit of the container to be unique**> | Start one container|
| docker container **stop** <**first digit of the container to be unique**> | Stop one container|
| docker container run --publish 80:80 --detach **--name charles** nginx | Create a container with a specific name |
| docker container **logs charles** | Fetch the logs of a container |
| docker **top charles** | Display the running processes of a container <br> (not working for me) |
| docker container **rm 8a7 2a1 c72** | Remove multiple containers |
| docker container **rm -f 8a7** | Force the removal of a running container (uses SIGKILL) |

## 2. Going on container

| Commands : | Description : |
| :--------- | :------------ |
| docker container **inspect** --help | Display detailed information on one or more containers |
| docker container **stats** --help <br> **Ctrl+c** to quit the view | Display a live stream of container(s) resource usage statistics |
| docker container run **-it** --name proxy nginx **bash** <br>exit | Start a new container interactively |

- Example of interactive container update:

>docker container run -it --name ubuntu ubuntu
apt-get update
apt-get install -y curl
exit

>docker container start -ai ubuntu
curl google.com
exit

| Commands : | Description : |
| :--------- | :------------ |
| docker container **exec** -it | Run a command in a running container |
Example: docker container exec -it mysql bash

| Commands : | Description : |
| :--------- | :------------ |
| docker pull alpine | Pull an image or a repository from a registry |
| docker image ls | List images |
Example: docker container run -it alpine **sh**  
>bash not provide with alpine, i need to install them

















## Test labo section

- **How to run a windows server core container ??**  

Basic: docker run [mcr.microsoft.com/windows/servercore](https://hub.docker.com/_/microsoft-windows-servercore?tab=description):ltsc2019

To run a container with Hyper-V isolation, simply add the tag --isolation=hyperv to your docker run command.  
Last command tested but seems close the container directly:  
docker run **--isolation=hyperv** mcr.microsoft.com/windows/servercore:ltsc2019 powershell

