# How to Install Docker Engine and Docker-Compose on Ubuntu VPS

*by Blog Edu Tech, January 10, 2022*

## Intro

Docker is an incredible software that simplifies the installation of various software with just a few clicks. In this guide, I'll explain how to install Docker on a VPS. I'm utilizing the Oracle Cloud VPS server, which is free forever. Follow these steps to install Docker on your VPS. Once Docker is installed, you can set up WordPress with just one click.


### Connect the VPS server

Use the following commands step by step:

```bash
sudo apt update
sudo apt upgrade
```

### Create swap memory on the VPS (optional):

```bash

free -m
sudo su
sudo dd if=/dev/zero of=/mnt/swap.0 bs=5024 count=1048576 && sudo mkswap /mnt/swap.0 && echo "/mnt/swap.0 swap swap defaults 0 0" >> /etc/fstab && swapon /mnt/swap.0 && sudo swapon -s
```

### Remove the old version of Docker if any:

```bash

sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt-get update
sudo apt-get upgrade
```

### To install Docker on Ubuntu VPS

bash

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

sudo docker version
docker compose version

sudo groupadd docker
sudo usermod -aG docker ubuntu [ubuntu is name of the user of VPS server]

logout

docker status

Uninstall Docker

bash

sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd

Ref: Docker

After installing Docker, you can install Portainer. It is a GUI for docker containers. If you install Portainer on Docker, follow this tutorial How to Install Portainer on Docker.
Conclusion
