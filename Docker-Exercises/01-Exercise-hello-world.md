### Run Hello World Image in a new container
### hello-world image documentation : https://hub.docker.com/_/hello-world

```
# Let us first pull the image
docker pull hello-world

# Check if the image has been downloaded & also check its 'tag'
docker image ls

# Spin up a new container and run hello-world image in it
docker run hello-world

# List running containers - Check all attributes - name, cmd, image, status, creation timestamp & name
docker ps

# List all containers - running & exited
docker ps -a

# Clean up hello-world container by specifying either container-id or container-name
docker rm <container-id>

```
