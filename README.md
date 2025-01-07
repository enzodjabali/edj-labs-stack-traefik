# Stack Traefik

1. Change the values of `email` in traefik.yml and `traefik.http.routers.api.rule` in docker-compose.yml

2. Create the `traefik-public` network:
```
docker network create --driver overlay traefik-public
```

3. Change the `acme.json` permission:
```
sudo chmod 600 acme.json
```

4. Deploy the stack using Docker Swarm:
```
docker stack deploy -c docker-compose.yml traefik
```

Access the Traefik dashboard at: https://traefik.your-domain.com
