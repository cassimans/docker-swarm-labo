# Lampiris Docker Swarm Sample


## Vote-App

#### Install Vote-App
```
docker stack deploy -c docker-compose.yml vote-app
```


#### Vote-App Suppression
```
docker service ps vote-app
docker stack ls
docker stack rm vote-app
```
