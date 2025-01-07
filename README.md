# Stack Traefik

1. Create the `traefik-public` network:
```
docker network create --driver overlay traefik-public
```

2. Change the `acme.json` permission:
```
sudo chmod 600 acme.json
```

3. Deploy the stack using Docker Swarm:
```
docker stack deploy -c docker-compose.yml traefik
```
