# Lampiris Docker Swarm 

## Install 

##### Requisites
```
sudo apt-get install curl
```

##### Install : DOCKER
```
curl -fsSL get.docker.com -o get-docker.sh
sh get-docker.sh
sudo docker run hello-world
```

##### Install : SWARM
```
sudo docker swarm init --advertise-addr 10.20.130.11

sudo docker info
sudo docker node ls
sudo docker swarm join-token manager
```

## Demos

##### Simple SERIVCES (nginx)
```
sudo docker service create -p 80:80 --name web nginx
sudo docker service ls
sudo docker service ps web
sudo docker ps

sudo docker service scale web=2
```

