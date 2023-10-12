**Docker commands**

```
docker run busybox ls -ltr
```
```
docker run --> docker create + docker start 
```
```
docker system prune
will delete: stopped containers, networks not used, dangling images, and **build cache (ALL DOWNLOADED IMAGES)**
```

```
docker stop --> sigterm terminate signal, to give some time to shut itself down and do clean up, save file, or send message. gives 10 seconds, then it kills
```
```
docker kill --> sigkill kill signal, shutdown immediately, no time for anything else
```
```
docker exec -it <container id> <second command to execute in running container like bin\bash>

Same as "docker exec -i -t" -i anything I type gets redirected to docker standard in, -t helps displays my inputs and container's output in a nice formatted manner 
```  

```
Other uses for docker "exec" command
docker exec -it <container id> sh
sh | bash | zsh -> command processor for terminal access
```

```
create empty container and get inside shell (container not running any process)
docker run -it busybox sh
```

```
build image from Dockerfile
docker build .
will build image from Dockerfile in current directory. Can be used to rebuild

docker uses cached image for unchanged first portion of dockerfile. **Order of operations matters**
```


```
add tag to docker build
docker build -t dockertest/redis:latest .
convention <docker id> / <repo or project name> : <version>
```

```
Buildkit in newer docker versions hides some steps by default, to see this output use progress flag
docker build --progress=plain .

docker build --no-cache --progress=plain .
```

```
Create a new modified image from inside a container
- run the image to create container:

$ docker run -it alpine sh

- then make modifications inside this running container.
- open a second terminal, to run a docker command to take a snapshot of running container, this will create a new image with the changes made and a new default command

to get container id
$ docker ps

create new image
docker commit -c 'CMD ["redis-server"]' <container id>
```

```
run docker container with port mapping
redirect request from local machine port : to container port
docker run -p 5000:8080 mlopdocker/simpleweb
```

```
Set working directory. All run, copy, etc. commands will execute from this directory
WORKDIR /usr/app
```  

```
-d or --detach flag to run in detach mode, background
docker run -d 
```

<br/><br/>

**Docker Compose commands**

- separate CLI to gets installed along with docker. 
- used to start up multiple docker containers at the same time.
- automates long arguments we were passing to 'docker run'.
- commands are written in special syntax in yml file 'docker-compose.yml'

```
this look in current working dir for docker compose file
docker compose up  -> equal to docker run myimage

docker build .      __
docker run myimage  -- > docker-compose up --build
```

```
start group of containers in background
docker-compose up -d
```

```
stop group of containers
docker-compose down
```

```
docker compose restart policy
restart: 'no'  // quotes needed bc no in yml files means false
restart: always
restart: on-failure
restart: unless-stopped
```

```
see running containers from docker-compose. Must run is same dir as docker-compose file
docker-compose ps
```