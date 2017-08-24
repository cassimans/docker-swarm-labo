# Lampiris Docker Swarm : whoami

#### Install App
```
docker stack deploy -c docker-compose.yml whoami
```

#### App Suppression
```
docker service ps whoami_whoami
docker stack ls
docker stack rm whoami
```
