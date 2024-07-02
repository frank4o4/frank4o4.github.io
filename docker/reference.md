# Docker Reference Commands

Pull a image
``` sh
docker pull alpine
docker pull itzg/minecraft-server
```


Delete a image
``` sh
docker image rm IMAGE
```


List Images

``` sh
docker images
```

Create a container
``` sh
docker container create -i -t --name mycontainer alpine
```

Create and run

``` sh
docker run -d -p 25565:25565 --name mc itzg/minecraft-server
```

Start Container

``` ls
docker start <container name>
```

List Containers

``` sh
docker container ls -a
```

See docker running

``` sh
docker ps
```

Connect to a container

``` sh
docker exec -it mycontainer bash
```


See Container Logs, maybe container wont start
``` ls
docker logs minecraft_survival
```


Minecraft Container
``` sh
docker run -itd --network ipvlan --ip 192.168.1.5 -e EULA=TRUE --name minecraft_survival itzg/minecraft-server:latest
```


### Prune volumes 
Volumes can be used by one or more containers, and take up space on the Docker host. Volumes are never removed automatically, because to do so could destroy data.
``` sh
docker volume prune
```

### Prune containers
``` sh
docker container prune
```

### Prune images
``` sh
docker image prune
```