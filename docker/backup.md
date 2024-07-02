# Docker Backup

## Image

Backup a image
``` sh
docker image save -o <image.tar> <image to backup>
```

Restore Image
``` sh
docker image load -i <image.tar>
```


Backup a docker container to a image

``` sh
docker commit <container name> <image name>
```