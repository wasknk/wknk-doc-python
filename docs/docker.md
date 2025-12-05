# Docker Usage

## Install
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
docker ps
```

## Docker Compose
```
# use default file ./docker-compose.yml
docker compose up

# or  specify the  yml file
docker compose -f docker-compose-monitor.yml up
``` 