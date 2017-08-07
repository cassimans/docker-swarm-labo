# Lampiris Docker Swarm Sample


## Vote-App

#### Install Vote-App
```
sudo docker deploy --compose-file=docker-compose.yml stackdemo
```

#### Go to Vote-App
```
http://host:5001
```

#### Vote-App Suppression
```
sudo docker stack rm stackdemo
```
