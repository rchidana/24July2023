### Exercise to store data outside the container using Volumes
### Docker Documentation : https://docs.docker.com/storage/volumes/
### Docker CLI Reference : https://docs.docker.com/engine/reference/commandline/volume_create/ 
### Bind Mount Documentation : https://docs.docker.com/storage/bind-mounts/ 

```
# Any folder from the host machine can be bind mounted to a container
# Note : In few cases, folder permissions will have to be addressed appropriately

# Let us bind mount a local folder (which is in home directory) by name 'local-folder' to a container by name 'container1'

docker run -itd --name container1 -v ~/local-folder:/local-folder alpine bin/sh
docker ps

# Get into 'container1' and write some data to '/local-folder'
docker attach container1
cd local-folder

echo "hello, from container1" >> ctr1-data.txt

# Let us spin up another new container called 'container2' which will user --containers-from option

docker run -itd --name container2 -volumes-from container1 alpine bin/sh

# Attach to container2 and check the contents of '/local-folder'
docker attach container2
ls /local-folder

# Check if you can write/edit contents of '/local-folder'

# Let us spin up another container - 'container3' but mount the volume in read-only mode
docker run -itd --name container3 -volumes-from container1:ro alpine bin/sh

# Attach to container3 and check if you can write/edit contents in '/local-folder'

```

