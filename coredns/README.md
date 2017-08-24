# Lampiris Docker Swarm Sample


## Vote-App

#### Install CoreDNS local
```
docker run -d -p "53:53/udp" -v $(pwd)/Corefile:/Corefile -v $(pwd)/activation.swarm.hosts:/activation.swarm.hosts coredns/coredns
```

### Switch DNS to 127.0.0.1
