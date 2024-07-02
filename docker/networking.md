# Docker Network



If you would like to make your docker container run on an IP address on your local subnetwork you will have to create a new network as follows.


Creating an ipvlan allows the docker container to access your network directly. 
``` sh
docker network create -d ipvlan --subnet 192.168.0.0/24 --gateway 192.168.1.1 -o parent=<network card> <network name>
```

Run Docker Container in IPVLAN
``` sh
docker run -itd --network ipvlan --ip <IP Address> --name <container name> <image to use>
```

List Current network

``` sh
docker network ls
```
