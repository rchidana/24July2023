### Exercise to store data outside the container using Volumes
### Docker Documentation : https://docs.docker.com/storage/volumes/
### Docker CLI Reference : https://docs.docker.com/engine/reference/commandline/volume_create/ 

```
# Let us first create a docker managed volume called 'my-data' and then mount it to container

docker volume create my-data
docker volume ls
docker volume inspect my-data

# Let us mount this volume to a container called 'my-container'

docker run -itd --name my-container -v my-data:/my-data alpine /bin/sh
docker ps

# Check if there is a folder by name - 'my-data' inside 'my-container'
docker attach my-container

# Any data written to this folder will get persisted in our volume

cd my-data
echo "hello world" >> hello.txt
echo "hi" >> hi.txt
ls 

```

### Outside the container, check if the files are present in the folder mapped to our volume

```
docker volume inspect my-data
sudo ls /var/lib/docker/volumes/my-data/_data

# Try to edit these files from outside the container and check if the modifications reflect inside the container
```

### Even if the container gets deleted/removed, the volume contents will persist