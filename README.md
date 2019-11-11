# DockerCommands

- [DockerCommands](#dockercommands)
  - [1. Start container](#1-start-container)
  - [2. Going on container](#2-going-on-container)
  - [3. Network](#3-network)
  - [4. Images](#4-images)
  - [Test labo section](#test-labo-section)

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

## 3. Network

Remember: publishing ports is always in **-p** (--publish) **HOST**:**CONTAINER** format.  

| Commands : | Description : |
| :--------- | :------------ |
| docker container **port** _[cont_id]_ | Get the port used by the container |
| docker container **inspect** --format '{{ .NetworkSetings.IPAddress }}' _[cont_id]_ | Get the ip address used by the container |

Virtual network bridge/docker0 by default for all container  

| Commands : | Description : |
| :--------- | :------------ |
| docker **network ls \|show** | Default 3 (bridge'nat', host'**Default Switch**', none) |
| docker network **inspect \|inspect** | Inspect |
| docker network **create --driver** | Create |
| docker network **connect** | Connect |
| docker network **disconnect** | Disconnect |
| docker network inspect 'Default Switch' <br> docker network inspect nat | Inspect |

- **Example to create a new network in windows container context**

>docker network create my_app_net  
Error response from daemon: could not find plugin bridge in v1 plugin registry: plugin not found  
-d, --driver string Driver to manage the Network (default "bridge")  
docker network create -d nat my_app_net  

- **Example to connect an application to a network**

>docker container run -d --name new_nginx --network my_app_net nginx  
docker network inspect my_app_net  
docker network --help  
docker network connect my_app_net nginx  
docker network disconnect my_app_net nginx  

## 4. Images

What is?

- App binaries/dependencies
- Metadata about the image data and how to run the image
- no OS, no kernel
- small one file (your app binary) or big file (Ubuntu distro with apt)

| Commands : | Description : |
| :--------- | :------------ |
| docker **pull nginx:1.16** | pull the [stable version of nginx](https://hub.docker.com/_/nginx) |
| docker **image ls** | List images |

- Image layers
- union file system
- history
- inspect
- copy on write

| Commands : | Description : |
| :--------- | :------------ |
| docker **image history** | Show the history of an image |
| docker **image inspect** | [METADATA] Display detailed information on one or more images |
| docker **image inspect** --format '{{ .ContainerConfig.ExposedPorts }}' cont_id | Get the exposed port of a image |

## Test labo section

| Commands : | Description : |
| :--------- | :------------ |
| code . (in a repo) | Open Visual Studio Code |

- **How to run a windows server core container ??**  

Basic: docker run [mcr.microsoft.com/windows/servercore](https://hub.docker.com/_/microsoft-windows-servercore?tab=description):ltsc2019
Image size: 4.79GB... **wtf ??**

To run a container with Hyper-V isolation, simply add the tag --isolation=hyperv to your docker run command.  
Last command tested but seems close the container directly:  
docker run **--isolation=hyperv** mcr.microsoft.com/windows/servercore:ltsc2019 powershell

- **How to install onto ubuntu-18.04.3-desktop-amd64**

sudo apt install curl  
curl -fsSL get.docker.com -o get-docker.sh  
sh get-docker.sh  

**Warning about security** but ok on local machine:  
sudo usermod -aG docker charles  
sudo docker version  

**Upgrade Compose**: https://github.com/docker/compose/releases  
>curl -L https://github.com/docker/compose/releases/download/1.25.0-rc4/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose

**Upgrade Machine**: https://github.com/docker/machine/releases  
>curl -L https://github.com/docker/machine/releases/download/v0.16.2/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine &&
    chmod +x /tmp/docker-machine &&
    sudo cp /tmp/docker-machine /usr/local/bin/docker-machine  

**Remark: get of root** with **sudo -i**  

**Check: docker-machine version**
docker-machine version 0.16.2, build bd45ab13  

**Check: docker-compose version**  
docker-compose version 1.25.0-rc4, build 8f3c9c58  
docker-py version: 4.1.0  
CPython version: 3.7.4  
OpenSSL version: OpenSSL 1.1.0l  10 Sep 2019  

**How to customize your Shell** look at [bretfisher shell](https://www.bretfisher.com/shell/)  