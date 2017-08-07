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
docker swarm init --advertise-addr 10.20.130.11
docker info
docker system info
docker node ls
docker swarm join-token manager
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
service docker restart
```


## Demos

#### Simple SERIVCES (nginx)
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

