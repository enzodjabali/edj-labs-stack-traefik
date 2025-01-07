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

--

### Adding authentification to the Traefik dashboard

1. Download htpasswd:
```
sudo apt-get update -y && sudo apt-get install apache2-utils -y
```

2. Generate your credentials:
```
echo $(htpasswd -nb username password) | sed -e s/\\$/\\$\\$/g
```

3. In the `docker-compose.yml` file, add the following lines to your `labels:` and replace the username and password by the prompt you got from the htpasswd command:

```yaml
- "traefik.http.routers.api.middlewares=auth"
- "traefik.http.middlewares.auth.basicauth.users=username:$$apr1$$KqzcYMHA$$IkgDTvldUa7pj337TIMM21"
- "traefik.http.middlewares.auth.basicauth.removeheader=true"
```

4. Update the `traefik` stack:
```
docker stack deploy -c docker-compose.yml traefik
```
