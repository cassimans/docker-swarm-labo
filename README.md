# Docker Swarm 

## Install SWARM Host

#### Requisites
```
apt-get install curl
```
#### Install : DOCKER
```
curl -fsSL get.docker.com -o get-docker.sh
sh get-docker.sh
docker run hello-world
docker info
docker system info
```
#### Install : SWARM
```
docker swarm init --advertise-addr 10.20.130.15
docker node ls
```
#### Join Existing SWARM
```
docker swarm join-token manager
docker swarm leave --force
docker swarm join --token ...
docker node promote node-3 node-2
docker node demote node-3 node-2
```

## Configure to exclude TLS security

#### edit service
```
systemctl status docker
vim /lib/systemd/system/docker.service
```
#### Add -H tcp like follow 
```
ExecStart=/usr/bin/dockerd -H fd:// -H tcp://0.0.0.0:2375
```
#### Restart
```
systemctl daemon-reload
service docker restart
```

## Configure SWARM With Services

#### Install : TRAEFIK (https://docs.traefik.io/#get-it), PORTAINER IO (https://portainer.io)
```
export DOCKER_HOST=tcp://10.20.130.15:2375
docker stack deploy -c traefik/docker-compose.yml traefik
docker stack deploy -c portainer/docker-compose.yml portainer
```


# Tips commands

## Container access
```
docker service ls     # find service name
docker service ps xxx # find node
docker ps             # On node, find NAMES
docker volume prune --force
docker exec -it el2-adm_backend.1.g6suznnrwe5iko5ybt1kpq2jo /bin/bash
apt-get update
apt-get install vim
```

## Use Environment File

### With env file
```
env $(cat .env | grep ^[A-Z] | xargs) docker stack deploy -c docker-stack-deploy.yml el2-adm  --with-registry-auth
docker volume prune
docker exec -it el2-adm_backend.1.g6suznnrwe5iko5ybt1kpq2jo /bin/bash
```

### Without env file
```
env ADM_DB_HOST=database \
ADM_DB_PORT=5432 \
ADM_DB_NAME=el2adm \
ADM_DB_USER=el2adm \
ADM_DB_PASSWORD=el2adm \
PROJECT_VERSION=features-eltwoadm-2993 \
docker stack deploy --compose-file=docker-stack-deploy.yml el2-adm --with-registry-auth
```


# Demos

#### Create SERIVCES (nginx)
```
docker service create -p 80:80 --name web nginx
docker service ls
docker service ps web
docker ps
```
#### Scale SERIVCES (nginx)
```
docker service scale web=2
```
#### Remove SERIVCES (nginx)
```
docker service ls
docker service rm web
```


### Stack (Vote-App)

#### Install STACK (Vote-App)
```
docker stack deploy --compose-file=docker-compose.yml stackdemo
```
#### Go to STACK (Vote-App)
```
http://host:5000
http://host:5001
```
#### Remove STACK (Vote-App)
```
docker stack ls
docker stack rm stackdemo
```

## Run Images SWARM Without Services (NOT RECOMMENDED)

#### Install : TRAEFIK (https://docs.traefik.io/#get-it)
```
wget -O /var/local/bin/docker-compose  https://github.com/docker/compose/releases/download/1.15.0/docker-compose-Linux-x86_64 
cp traefik/docker-compose.yml .
docker-compose -p traefik up -d 
```
#### Install : PORTAINER IO (https://portainer.io)
```
sudo docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer
docker stack deploy -c portainer/docker-compose.yml portainer
```
