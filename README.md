# Docker-Cheat-Sheet
Some commands to manage docker

## General
### Pull images from DockerHub
`docker pull <image-name>`

### Build image
`docker build --tag <name>:<version> <path-to-dockerfile>`

### List images
`docker image ls` OR `docker images`

### Delete image
`docker image rm <image-id or ids>`

### List containers
1) Running containers: `docker ps`
2) All conatiners: `docker ps -a`

### View logs
`docker logs <container-id>`

### Delete logs
1) `echo "" > $(docker inspect --format='{{.LogPath}}' <container_name_or_id>)`
2) `: > $(docker inspect --format='{{.LogPath}}' <container_name_or_id>)`
3) `truncate -s 0 $(docker inspect --format='{{.LogPath}}' <container_name_or_id>)`

## Management
### Shell in container:
`docker exec -it <conatiner-id> bash` use bash or `sh`

### Stop container
`docker stop <container-id>`

### Start container
`docker start <container-id>`

### Restart containeer
`docker restart <container-id or ids>`

### Delete container
`docker rm <container-id>`<br>
Force delete: `docker rm --force <container-id>`

### Copy file IN container
`docker cp <file-name> <container-id>:</path>

### Run container
`docker run --name <own-name> -d -e <ENV-Var> --restart always <docker-image>`<br>
`--name`-Flag to set own container name<br>
`-d`-Flag used for detached start<br>
`-e`-Flag used for environment variables<br>
`--restart`-Flag used to set if container shall restart (Values: `always`, `no`, `on-failure`, `unless-stopped`)<br>
`-i`-Flag used for interactive<br>
`-t`-Flag for terminal<br>
`-p <port-on-host>:<port-in-container>/<udp | tcp>` Used to expose port<br>
  
More flags see: [Docker-Docs](https://docs.docker.com/engine/reference/commandline/run/)

## Networking
### List networks
`docker network ls`

### IPs of all Containers
`docker ps -q | xargs -n 1 docker inspect --format '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}} {{ .Name }}' | sed 's/ \// /'`

### Create a network
`docker network create --driver bridge --subnet <subnet e.g. 172.22.5.0/24> <network-name>`

### Connect container to network
`docker network connect <network-name OR network-id> <container-name OR container-id>`

### Disconnect container from network
`docker network disconnect <network-name OR network-id> <container-name OR container-id>`

## Dockerfile
Stuff about `Dockerfile`<br>

## Docker-Compose
Stuff about `docker-compose.yml`<br>

### Compose up
`docker-compose up -d`<br>
`-d`-Flag used for detached

### Compose down
`docker-compose down`
