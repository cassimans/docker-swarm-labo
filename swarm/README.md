# Lampiris Docker Swarm Sample


## Vote-App

#### Install Vote-App
```
docker stack deploy --compose-file=docker-compose.yml stackdemo
```

#### Go to Vote-App
```
http://host:5000
http://host:5001
```

#### Vote-App Suppression
```
docker stack ls
docker stack rm stackdemo
```
