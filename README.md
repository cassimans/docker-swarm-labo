# Lampiris Docker Swarm 

## Install 

#### Requisites
```
apt-get install curl
```
#### Install : DOCKER
```
curl -fsSL get.docker.com -o get-docker.sh
sh get-docker.sh
docker run hello-world
```
#### Install : SWARM
```
docker swarm init --advertise-addr 10.20.130.15
docker info
docker system info
docker node ls
docker swarm join-token manager

#### Join SWARM
```
docker swarm leave --force
docker swarm join --token ...
docker node promote node-3 node-2
docker node demote node-3 node-2
```

#### Install : PORTAINER IO (https://portainer.io)
```
sudo docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer
```


#### Install : TRAEFIK (https://docs.traefik.io/#get-it)
```
wget -O /var/local/bin/docker-compose  https://github.com/docker/compose/releases/download/1.15.0/docker-compose-Linux-x86_64 
cp traefik/docker-compose.yml .
docker-compose -p traefik up -d 
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


## Demos


### Services (nginx)

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
